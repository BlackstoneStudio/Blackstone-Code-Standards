# NestJS Best Practices

Version 1.0.0
<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Validation Pipes](#2-validation-pipes)
  - [2.1 Global Pipe](#21-global-pipe)
    - [i. Whitelist](#i-whitelist)
    - [ii. Exception Factory](#ii-exception-factory)
    - [iii. Others](#iii-others)
  - [2.2 Validations](#22-validations)
- [3. Structures](#3-structures)
  - [3.1 Controller](#31-controller)
- [5. References](#5-references)

<!-- /MarkdownTOC -->

---

## 1. Introduction

Nest (NestJS) is a framework for building efficient, scalable Node.js server-side applications. Under the hood, Nest makes use of robust HTTP Server frameworks like Express (the default) and optionally can be configured to use Fastify as well!

This document attempts to cover issues related to the [documentation framework](https://docs.nestjs.com/), as well as practices learned through experience that are not documented.

---

## 2. Validation Pipes

A [Pipe](https://docs.nestjs.com/pipes) is a class that will transform or validate the provided information.
Pipes have two typical use cases:

- transformation: transform input data to the desired form (e.g., from string to integer)
- validation: evaluate input data and if valid, simply pass it through unchanged; otherwise, throw an exception when the data is incorrect

### 2.1 Global Pipe

The `ValidationPipe` makes use of the powerful [class-validator](https://github.com/typestack/class-validator) package and its declarative validation decorators. The `ValidationPipe` provides a convenient approach to enforce validation rules for all incoming client payloads, where the specific rules are declared with simple annotations in local class/DTO declarations in each module.

It is recommended to use the `ValidationPipe` globally as this will assume that all DTO's will comply with the requested validations.

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

It is recommended to use the whitelist and exceptionFactory properties, as they will help to reduce possible information injections and to format errors in a more readable way respectively. 

#### i. Whitelist

If set to true, validator will strip validated (returned) object of any properties that do not use any validation decorators.

It is highly recommended because all undesirable properties will be removed before reaching the controller. 

#### ii. Exception Factory

Takes an array of the validation errors and returns an exception object to be thrown.

This is a generic example to use. With this code a more detailed and clear error message will be shown to use in the fronted, when some property does not comply with the specified decorators.

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

Error Example:

```JSON

{
    "status": 400,
    "description": "Validation error.",
    "errors": [
        {
            "field": "name",
            "message": "name must be a string",
            "validation": "isString",
            "constraints": {
                "isString": "name must be a string"
            }
        },
        {
            "field": "description",
            "message": "description must be a string",
            "validation": "isString",
            "constraints": {
                "isString": "description must be a string"
            }
        }
    ]
}
```

#### iii. Others

In addition to these recommendations there are a variety of [options](https://docs.nestjs.com/techniques/validation#using-the-built-in-validationpipe) that can be used in the `ValidationPipe` constructor such as `enableDebugMessages`, `skipUndefinedProperties`, `skipNullProperties`, etc.

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

---

## 3. Structures

There are features that all classes should have, such as
- Types
  - Constructor.
  - Attributes.
  - Parameters.
  - Return.
- Comments (Optional - If the function/method is not clear)
  - JS Doc
  - Line comment

Example:

```javascript
@Injectable()
export class TasksService {
  private prisma: PrismaService;

  constructor(prismaService: PrismaService) {
    this.prisma = prismaService;
  }

  create({ userId, ...data }: CreateTaskDto): Promise<Task> {
    return this.prisma.tasks.create({
      data: {
        ...data,
        Users: {
          connect: { id: userId },
        },
      },
    });
  }
}
```

The basic structure of each function/method depends on the type of file it is in, these are the most used:

### 3.1 Controller

```javascript
@Post()
@UseGuards(JwtAuthGuard)
async create(@Body() dto: CreateTaskDto, @Res() res: Response): Promise<void> {
  try {
    const task = await this.service.create(dto);
    res.status(HttpStatus.CREATED).json(task);
  } catch (error) {
    this.logger.error(error.message);
    res.status(errors.UNKNOWN_ERROR.status).send();
  }
}
```

