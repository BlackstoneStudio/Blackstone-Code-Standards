# Classes and the SOLID principles

You should prefer many **small classes over** a flew **large classes**.

Classes should be **SOLID, **this means they should follow each of the next principles**:**

**S** - Single Responsibility Principle

**O** - Open-Closed Principle

**L** - Liskov Substitution Principle

**I** - Interface Segregation Principle

**D** - Dependency Intervention Principle

### The Single Responsibility Principle

Classes should have a single responsibility, they should not change for more than one reason.

Restricting classes to one core responsibility leads to smaller classes.

### The Open Closed Principle

A class should be open for extension but closed for modification.

Make **new sub classes extending the original class** rather than be adding new methods over and over again to the original class.

Extensibility ensures smaller classes instead of growing classes and can help **prevent code duplication (DRY - Don’t Repeat Yourself).**

### The Liskov Substitution Principle

Objects should be replaceable with instances of their sub classes without altering the behavior.

Example: 

```typescript 
// base class
class Bird {
  fly() {
    console.log('Flying...');
  }
}

// our sub class 'Eagle' extending our base class
class Eagle extends Bird {
  dive() {
    console.log('Diving...');
  }
}

const eagle = new Eagle();
// method from our base class
eagle.fly();
// method from our Eagle class
eagle.dive();
```

All good so far, but, what happens if we added a Penguin class? 

```typescript 
class Penguin extends Bird {
  // some penguin methods
}
```

This would be a mistake because we would be extending the ‘`fly()`' functionality from our base `Bird` class and **penguins can’t fly!**

The ideal thing to do here is not to delete the `fly()` method, but to instead have 2 super classes (or base classes) for birds that can fly and for those that can't. 

Example: 

```typescript 
// super class 1 
class Bird {
 // some bird methods here
}

// super class 2
class FlyingBird extends Bird {
  fly() {
    console.log('Flying...');
  }
}

class Eagle extends FlyigBird {
  dive() {
    console.log('Diving...')
  }
} 

class Penguin extends Bird {
  // some penguin methods
}

```

This way you can add the `fly()` functionality for the birds that need it without adding it for the birds that don’t. 

The principle actually **forces you to module your data correctly **which is an important part in writing good and extensible code.

### The Interface Segregation Principle

Many client-specific interfaces are better than one general purpose interface. 

### The Dependency Inversion Principle

You should depend on abstractions, not concretions.
