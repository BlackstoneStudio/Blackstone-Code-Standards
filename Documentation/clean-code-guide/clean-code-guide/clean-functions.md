# Clean Functions

Some points to have a clean function: 

- Functions should be **small** 
- Functions **should do one thing.**
- Do not write the same code in different places.
- Avoid functions that don't sound like they are doing what they are doing. **(Name them properly!)**
- **Minimize the number of parameters, **this will make them easy to understand and easy to call.

> 0 - 2 parameters (IDEAL)

> 3+ Parameters (PLEASE AVOID)



Things to have in consideration: 

### Use of objects

Using objects to send a function a set of parameters is very useful because you will be using **key identifiers for each value**. 

### Side Effects 

Is an operation that not only acts on function inputs and changes the function outputs but instead **it changes the overall system or program state.**

### Levels of abstraction

**High Level **

They are operations with a **descriptive name that tells you that that function is going to do something really specific**, you just call it.

Example: 

```typescript 
isEmail(email);
```

It is very descriptive and **we only care about the result.**

**Low level**

They are operations that **you actually need to know what they are doing and why or you need to control what they are doing and how**, like controlling how the email is being validated, for example:

``` 
email.includes(‘@’);
```

‘Includes’ doesn't really tell you anything other than the string ‘email’ has an ‘@’ in it, it doesn’t explicitly say the email is being validated.

This is why it is a Low Level, because **we need to add or interpret the meaning to that.**

> Levels of abstraction are important because it allows us modularizing the functions into smaller functions that handle one same functionality at a time and that are easier to read. 
