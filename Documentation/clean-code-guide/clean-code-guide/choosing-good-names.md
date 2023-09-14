# Choosing Good Names

Names should be descriptive and meaningful

### Variables and Constants

It is important to use **nouns or short phrases with adjectives** that describe what is being stored in that variable.

```typescript 
const userData = { ... };
```

### Functions and Methods

It is important to use **verbs or short phrases with adjectives **that describe what is being done with the function in question.

```typescript 
sendData();
```

### Classes

It is important to **use nouns or short phrases with nouns** that describe what ‘thing’ are we creating.

```typescript 
User {...}
```

### Name Casing Types

| **Casing**  | **Where to use**                 | **Languages that use it** | **Examples**  |
| ----------- | -------------------------------- | ------------------------- | ------------- |
| snake_case  | Variables, functions and methods | Python                    | is_valid      |
| camelCase   | Variables, functions and methods | JavaScript,Java           | isValid       |
| PascalCase  | Classes                          | Python,JavaScript,Java    | AdminRole     |
| kebab-case  | Custom HTML Elements             | HTML                      | <side-drawer> |


---

## Naming Variables, Constants & Properties

A good name may depend on what the type of your value is.

### Object

**Simply describe what the value is **like `'user'` or `'database'`. And maybe consider providing more **details without introducing redundancy** like `'authenticatedUser'` or `'sqlDatabase'.`

> By **redundancy** we can mean for example, using the word ‘data’ for object variables, it is kinda obvious that the object contains data.

### String

Same as an object, `'age'`, `'name'` or more specific `'firstName'` .

### Boolean

This is where things are different, **they need to express a small question that can only be answered with yes or no **(true or false), like `'isActive'`, `'loggedIn'`.

## Naming Functions / Methods

It is basically the same theory as variables, but something to consider by naming functions is that **you need to describe what operation is being performed rather than the value that is returned (if it’s the case)**. 

You only want to do this last thing when functions compute a Boolean.

```typescript 
// non-boolean example
saveUser();
//boolean example
isValid();
```

> **IMPORTANT** 
> - Avoid redundant information, do not describe everything.
> - Avoid funny names.
> - Avoid Unclear abbreviations.
> - Avoid using misinformation like using the word `'list'` for an Object, or `'allUsers'` for a function that actually filters them.
> - Use the same patterns for names like `getUsers()`, ` getApplicants()` **Instead of mixing the keys words (get,fetch,retrieve, etc)**
