# Formatting

## Vertical Formatting

- Code should be **readable like an essay**.
- Consider **splitting** a single file with multiple concepts like classes, **into multiple files.**
- **Different concepts or ‘areas’ should be divided by spacing,** areas can also mean same kind of operations like a bunch of console.log()’s 
- **Keep related methods in order**, by means, write them in the order they are needed to be called (methods calling other methods). 

Example: 

```typescript 
methodA(){
	//method A operations
}

methodB(){
    //method B operations
    // method A was defined before it was called;
    methodA();
}
```

## Horizontal formatting

- Sentences **should be readable without scrolling** (avoid very long sentences).
- **Always use indentation**
- **Break long statements** into multiple shorter ones
- Use** clear but no unreadable** long names
