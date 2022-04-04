# NestJS Best Practices

Version 1.0.0
<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Validation Pipes](#2-validation-pipes)
  - [2.1 Global Pipe](#21-global-pipe)
    - [2.1.1 Whitelist](#211-whitelist)
    - [2.1.2 Exception Factory](#212-exception-factory)
    - [2.1.3 Others](#213-others)
  - [2.2 Validations](#22-validations)
- [3. Dictionaries](#3-dictionaries)
  - [3.1 Success](#31-success)
  - [3.2 Error](#32-error)
- [4. Structures](#4-structures)
  - [4.1 Controller](#41-controller)
    - [4.1.1 Guards](#411-guards)
    - [4.1.2 Swagger](#412-swagger)
      - [4.1.2.1 DTO's](#4121-dtos)
      - [4.1.2.2 Errors Responses](#4122-errors-responses)
  - [4.2 Service](#42-service)
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

#### 2.1.1 Whitelist

If set to true, validator will strip validated (returned) object of any properties that do not use any validation decorators.

It is highly recommended because all undesirable properties will be removed before reaching the controller. 

#### 2.1.2 Exception Factory

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

#### 2.1.3 Others

In addition to these recommendations there are a variety of [options](https://docs.nestjs.com/techniques/validation#using-the-built-in-validationpipe) that can be used in the `ValidationPipe` constructor such as `enableDebugMessages`, `skipUndefinedProperties`, `skipNullProperties`, etc.

### 2.2 Validations

Nest works well with the class-validator library. This powerful library allows you to use decorator-based validation. Decorator-based validation is extremely powerful, especially when combined with Nest's Pipe capabilities since we have access to the metatype of the processed property.

```javascript
import { ApiProperty, ApiPropertyOptional } from '@nestjs/swagger';
import {
  IsDateString,
  IsNotEmpty,
  IsOptional,
  IsString,
} from 'class-validator';

export class CreateTaskDto {
  @IsString()
  @IsNotEmpty()
  @ApiProperty()
  name: string;

  @IsString()
  @IsOptional()
  @ApiPropertyOptional()
  description?: string;

  @IsDateString()
  @IsOptional()
  @ApiPropertyOptional({ type: () => Date })
  completedAt?: Date;

  @IsString()
  @IsNotEmpty()
  @ApiProperty()
  userId: string;
}
```

---

## 3. Dictionaries

It is advisable to use the success and error dictionaries, so we can reuse them in API responses, error handling and swagger.

#### 3.1 Success:

```javascript
import { OmitType } from '@nestjs/swagger';
import { User } from 'src/modules/users/entities/user.entity';
import { ApiResponse } from './Response';

const Success: { [label: string]: ApiResponse } = {
  WELCOME_MESSAGE: {
    status: 200,
    description: 'Welcome message.',
  },
  REGISTER_SUCCESS: {
    status: 200,
    description: 'Register successfully.',
    type: OmitType(User, ['password']),
  },
};

export default Success;
```
#### 3.2 Error:

```javascript
import Response, { ApiResponse, ValidationError } from './Response';

function errorsType<T extends { [key: string]: ApiResponse & { exception?: unknown } }>(arg: T): T {
  return arg;
}

const Errors = errorsType({
  VALIDATION_ERROR: {
    status: 400,
    description: 'Validation error.',
    type: ValidationError,
  },
  UNKNOWN_ERROR: {
    status: 500,
    description: 'Unknown error.',
    type: Response,
  },
  UNAUTHORIZED: {
    status: 401,
    description: 'Unauthorized.',
    type: Response,
  },
  TASK_NOT_FOUND: {
    status: 404,
    description: 'The task does not exist.',
    type: Response,
  },
});

const NotTypeError = (error: ApiResponse) => {
  delete error.type;
  return error;
};

export { NotTypeError };
export default Errors;

```

---

## 4. Structures

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
  constructor(private prismaService: PrismaService) {}

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

### 4.1 Controller

```javascript

// HTTP request method decorator
@Post()
// Swagger Tags
@ApiBearerAuth()
@CommonErrorsResponses()
@ApiResponse(responses.TASK_SUCCESS)
@UseInterceptors(PermissionInterceptor)
// Guard - Validates the session and injects the user.. 
@UseGuards(JwtAuthGuard)
// DTO - This is important because the DTO must validate the data.
// Response - Use the express response, because you can control the response more efficiently than leaving it to NestJS.
async create(@Body() dto: CreateTaskDto, @Res() res: Response): Promise<void> {
  // It is very important to use a try/catch because this way you can control the response and not send unnecessary information to the client.
  try {
    const task = await this.service.create(dto);
    res.status(success.TASK_SUCCESS.status).json(task);
  } catch (error) {
    // It is very important to use a logger because this will give us information in the records to repair it later.
    this.logger.error(JSON.stringify(error));
    res.status(errors.UNKNOWN_ERROR.status).send();
  }
}
```
#### 4.1.1 Guards
[Guards](https://docs.nestjs.com/guards) have a single responsibility. They determine whether a given request will be handled by the route handler or not.
Guarding can be used with a decorator on endpoints/controllers or [globally](https://docs.nestjs.com/guards#binding-guards) using a decorator for a [public](https://docs.nestjs.com/security/authentication#enable-authentication-globally) endpoint/controller.

#### 4.1.2 Swagger

[Swagger](https://docs.nestjs.com/openapi/introduction) uses the [OpenAPI specification](https://swagger.io/specification/), which language-agnostic definition format used to describe RESTful APIs.
In the controller it is important to use the `@ApiResponse` [decorator](https://docs.nestjs.com/openapi/decorators) to show the possible success and error responses. It is also important to use the auth [decorator](https://docs.nestjs.com/openapi/decorators) (`@ApiBearerAuth()`) and necessarily add the decorator in the DTO's.

##### 4.1.2.1 DTO's

The decorators [`@ApiProperty()` and `@ApiPropertyOptional()`](https://docs.nestjs.com/openapi/types-and-parameters) are very important because they tell Swagger the type and other properties of the attribute.

```javascript
import { ApiProperty, ApiPropertyOptional } from '@nestjs/swagger';
import {
  IsDateString,
  IsNotEmpty,
  IsOptional,
  IsString,
} from 'class-validator';

export class CreateTaskDto {
  @IsString()
  @IsNotEmpty()
  @ApiProperty()
  name: string;

  @IsString()
  @IsOptional()
  @ApiPropertyOptional()
  description?: string;

  @IsDateString()
  @IsOptional()
  @ApiPropertyOptional({ type: () => Date })
  completedAt?: Date;

  @IsString()
  @IsNotEmpty()
  @ApiProperty()
  userId: string;
}
```

In addition, the `@CommonErrorsResponses()` decorator can be used to group the most common API errors.

##### 4.1.2.2 Errors Responses

Use `@CommonErrorsResponses()` custom decorator to add the responses of common errors.

```javascript

function CommonErrorsResponses() {
  return applyDecorators(
    SwaggerApiResponse(NotTypeError(Errors.VALIDATION_ERROR)),
    SwaggerApiResponse(NotTypeError(Errors.UNKNOWN_ERROR)),
    SwaggerApiResponse(NotTypeError(Errors.UNAUTHORIZED)),
  );
}
```

### 4.2 Service

The method in the service should only be concerned with its functionality and ignore where it will be used, usually the name describes this functionality.

For example, this method creates a task and passes the error responsibility to where it is used.

```javascript
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
```

The second example only clears the error because the email sent does not affect the user creation process.

```javascript
async create({ password, ...user }: Prisma.UsersCreateInput): Promise<User> {
  const hash = await this.bcrypt.getHash(password);
  const user =  this.prisma.users.create({
    data: { ...user, password: hash },
  });
  
  try {
    const verificationCode = Math.random().toString().substr(2, 4);
    const email: Envelope = {
      to: user.email,
      subject: 'verify your email account',
      text: `here is your verification code: ${verificationCode}`,
    };
    await this.parrot.sendEmail(email);
    } catch (error) {
      this.logger.error(error);
  }
  return user;
}
```

The third example creates a custom error so that when it is used you have specific information about what is happening, in the case of the controller you can reuse this same error to send it in the HTTP response.

```javascript
async create({ password, ...user }: Prisma.UsersCreateInput): Promise<User> {
  const userExistsPromise = this.prisma.user.findUnique({ where: { email: user.email } });
  const companyNameExistsPromise = this.prisma.organization.findUnique({
    where: { name: user.company.name },
  });

  const [userExists, companyNameExists] = await Promise.all([
    userExistsPromise,
    companyNameExistsPromise,
  ]);

  if (userExists) {
    throw new UserEmailRegisteredError(`the email ${user.email} is already registered`);
  } else if (companyNameExists) {
    throw new OrganizationRegisteredError(
      `the orgnization name ${user.company.name} is already registered`
    );
  }

  const hash = await this.bcrypt.getHash(password);

  return this.prisma.user.create({
    data: { ...user, password: hash },
  });
}
```

## 5. Request lifecycle
Nest applications handle requests and produce responses in a sequence we refer to as the request lifecycle. With the use of middleware, pipes, guards, and interceptors, it can be challenging to track down where a particular piece of code executes during the request lifecycle, especially as global, controller level, and route level components come into play. In general, the request lifecycle looks like the following:

1. Incoming request
2. Globally bound middleware
3. Module bound middleware
4. Global guards
5. Controller guards
6. Route guards
7. Global interceptors (pre-controller)
8. Controller interceptors (pre-controller)
9. Route interceptors (pre-controller)
10. Global pipes
11. Controller pipes
12. Route pipes
13. Route parameter pipes
14. Controller (method handler)
15. Service (if exists)
16. Route interceptor (post-request)
17. Controller interceptor (post-request)
18. Global interceptor (post-request)
19. Exception filters (route, then controller, then global)
20. Server response

---

## 6. References

Inspired by and based heavily on:

* [NestJS Documentation](https://docs.nestjs.com/)
* [Swagger](https://swagger.io/specification/)
