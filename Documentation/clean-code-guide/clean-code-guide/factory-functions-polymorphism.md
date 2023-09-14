# Factory Functions & Polymorphism

### Objects

Hides its internals and properties, for example, making them private and just e**xposes a public an API which allows to make things with this objects** like with **getters** and **setters**; they also contain contain **business logic (in OOP)**.

### Data container / Data Structure

Simple objects with **properties** **and** **methods** are **public,** almost no API, almost no methods.** They store and transport data.**

### Polymorphism 

Polymorphism is one of the core concepts of object-oriented programming languages where:

- **poly:** means **many**
- **morphism:** means **transforming one form into another**. 

Polymorphism means the **same function with different signatures is called many times**. 

> In real life, for example, a boy at the same time may be a student, a class monitor, etc. So a boy can **perform different operations at the same time**. This is called polymorphism.

**Features of Polymorphism:**

- Programmers can use the same method name repeatedly.
- Polymorphism has the effect of reducing the number of functionalities that can be paired together.

Example: 

```javascript 
class firstClass {
    add() {
        console.log("First Method")
    }
}
class secondClass extends firstClass {
    add() {
        console.log(30 + 40);
    }
}
class thirdClass extends secondClass {
    add() {
        console.log("Last Method")
    }
}
let ob = new firstClass();
let ob2 = new secondClass();
let ob3 = new thirdClass();
ob.add();
ob2.add();
ob3.add();
```

The Code above shows how to implement **inheritance polymorphism in JavaScript**.

 In this code, we have a class and in this class, we have the “add” method, and we inherit this class in the Second Class. We create different classes with the same method name and different definitions of methods. This example shows us the same method will perform different operations depending on the object upon which it is called.

**Polymorphism with Functions and Objects:** 

It is also possible in JavaScript that we can **make functions and objects with polymorphism.** 

In the next example, **we will make two functions with the same name ‘area’.  **

1. We define the area function in `class A`. 
2. In this function, we have two parameters – x and y. 
3. `Class B` is created by **extending class A**. 

The area function in **class B invoked** the area** method in class A through super keyword** – passing parameters a and b. 

 To make the area method behave differently in class B, we are going to console log the name of the class inside the method.  This way, it will become clear that the area method will behave differently depending on the object upon which it is called.

### Cohesion

How much are your class methods using the class properties? 

| **Maximum Cohesion**                                                   | **Highly Cohesive classes**            | **No Cohesion**                            |
| ---------------------------------------------------------------------- | -------------------------------------- | ------------------------------------------ |
| All methods each use all properties leads to a  highly cohesive object | All methods use most of the properties | All methods don’t use any class properties |

### Law of Demeter

Principle of Least Knowledge: Don’t depend on the internals of “strangers“ (other objects which you don’t directly know).

Code in a method may only access direct internals (properties and methods) of: 

- The object it **belongs to**
- Objects that are **stored in properties of that object**
- Objects which are **received as method parameters**
- Objects which are **created in the method**
