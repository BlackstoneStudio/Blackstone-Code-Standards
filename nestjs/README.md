# NestJS Best Practices

Version 1.0.0
<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Validation Pipes](#2-validation-pipes)
  - [2.1 Global Pipe](#2.1-global-pipe)
    - [i. Whitelist](#i-whitelist)
    - [ii. ExceptionFactory](#ii-exceptionFactory)
    - [iii. Others](#iii-others)
  - [2.2 Validations](#2.2-validations)
- [5. References](#5-references)

<!-- /MarkdownTOC -->

---

## 1. Introduction

Nest (NestJS) is a framework for building efficient, scalable Node.js server-side applications. 

---

## 2. Validation Pipes

A pipe is a class annotated with the `@Injectable()` decorator, which implements the `PipeTransform` interface.
Pipes have two typical use cases:

- transformation: transform input data to the desired form (e.g., from string to integer)
- validation: evaluate input data and if valid, simply pass it through unchanged; otherwise, throw an exception when the data is incorrect

You can read more details at https://docs.nestjs.com/pipes

### 2.1 Global Pipe

Since the `ValidationPipe` was created to be as generic as possible, we can realize it's full utility by setting it up as a global-scoped pipe so that it is applied to every route handler across the entire application.

```javascript
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { exceptionFactory } from './utils/exception.factory';

async function bootstrap(): Promise<void> {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      exceptionFactory,
    })
  );
  await app.listen(3000);
}
```

#### i. Whitelist

If set to true, validator will strip validated (returned) object of any properties that do not use any validation decorators.

#### ii. ExceptionFactory

Takes an array of the validation errors and returns an exception object to be thrown.

```javascript
import { BadRequestException, ValidationError } from '@nestjs/common';
import { MessageError } from '../entities/response.entity';
import Errors from './error.dictionary';

const getException = (exceptions: ValidationError[]): MessageError[] => {
  return exceptions.map(({ property, constraints, children }) => {
    if (children && children.length > 0) {
      return {
        field: property,
        children: getException(children),
      };
    }
    return {
      field: property,
      message: Object.values(constraints).join(', '),
      validation: Object.keys(constraints).join(', '),
      constraints,
    };
  });
};

const exceptionFactory = (exceptions: ValidationError[]): void => {
  throw new BadRequestException({
    status: Errors.VALIDATION_ERROR.status,
    description: Errors.VALIDATION_ERROR.description,
    errors: getException(exceptions),
  });
};

export { exceptionFactory };
```

#### iii. Others

https://docs.nestjs.com/techniques/validation#using-the-built-in-validationpipe

### 2.2 Validations

Nest works well with the class-validator library. This powerful library allows you to use decorator-based validation. Decorator-based validation is extremely powerful, especially when combined with Nest's Pipe capabilities since we have access to the metatype of the processed property.

```javascript
import {
  IsDateString,
  IsNotEmpty,
  IsOptional,
  IsString,
} from 'class-validator';

export class CreateTaskDto {
  @IsString()
  @IsNotEmpty()
  name: string;

  @IsString()
  @IsOptional()
  description?: string;

  @IsDateString()
  @IsOptional()
  completedAt?: Date;

  @IsString()
  @IsNotEmpty()
  userId: string;
}
```
