# Comments

- **Avoid them if your code is clear enough**, you don't want any redundancies. 

For example: 

```typescript 
private dbDriver: any: // the database engine to which we connect
```

In this case we could just name the variable `dbEngine` and avoid the comment.

- **Avoid** ‘dividers’ or ‘block markers’.

If you feel like you need them, consider **separating your file in different components or files.**

- **Avoid** misleading information
- **Avoid** commented out code 

### Good Comments

- Legal Information
- Information that can’t be described with the code itself like explaining what a regex does or accepts.
- Warnings 
- TODO’s 
- Documentation strings
