# Best Practice

### Dependency injection.-

Classes often require references to other classes. For example, a `Car` class might need a reference to an `Engine` class. These required classes are called *dependencies*, and in this example, the `Car` class is dependent on having an instance of the `Engine` class to run.

There are three ways for a class to get an object it needs:

1. The class constructs the dependency it needs. In the example above, `Car` would create and initialize its own instance of `Engine`.
2. Grab it from somewhere else. 
3. Has it supplied as a parameter? The app can provide these dependencies when the class is constructed or pass them into the functions that need each dependency. In the example above, the `Car` constructor would receive `Engine` as a parameter.

The third option is **dependency injection**! With this approach, you take the dependencies of a class and provide them rather than having the class instance obtain them itself.

Example with NestJS:

```typescript 
// car.module.ts
import { Module } from "@nestjs/common";
// Import service to inject
import { EngineService } from "src/modules/engine/engine.service.ts";
import { CarService } from "./car.service.ts";

@Module({
  // Add service in providers
  providers: [EngineService, CarService],
})
export class OrderModule {}


// car.service.ts
class CarService {
    private engine: EngineService;

    // Nestjs automatically injects it in the constructor.
    constructor(engine: EngineService) {
        this.engine = engine;
    }

    start() {
        engine.start();
    }
}
```

### Middleware.- 

Middleware is a function that is called **before** the route handler. Middleware functions have access to the [request](https://expressjs.com/en/4x/api.html#req) and [response](https://expressjs.com/en/4x/api.html#res) objects and functions can perform the following tasks:

- execute any code.
- make changes to the request and the response objects.
- end the request-response cycle.
- call the next middleware function in the stack.
- if the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.

[Example with NestJS](https://docs.nestjs.com/interceptors#interceptors):

```typescript 
import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('Before...');

    const now = Date.now();
    return next
      .handle()
      .pipe(
        tap(() => console.log(`After... ${Date.now() - now}ms`)),
      );
  }
}
```
