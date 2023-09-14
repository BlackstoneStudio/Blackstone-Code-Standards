# Control Structures and & Errors

Basics to keep your control structures clean:

- Avoid deep nesting
- Use factory functions and polymorphism 
- Prefer positive checks
- Utilize errors

### Guards and Fast Failing

They are ‘if’ statements used at the beginning of your code to rapidly end a function in case of an error.

Example:

| **Without Guards**                                                                            | **With Guards**                                                                                                                                           |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```typescript 
if(user.active) {
  if(user.hasPurchases()){
		// do something here
  }
}
```
 | ```typescript 
//Guard
if(!user.active){
	Return;  // Fail Fast
}
if(user.hasPurchases()){
	Return;
}

// if no error continue to do something here

```
 |

> This way you can **remove unnecessary nesting**!

### Throwing + handling errors

This can replace ‘if’ statements and lead to more focused functions.

> **SIMPLE RULE:** If something is an error -> Make it an error! 

A good practice is catching errors with the `tryCatch` statement.

Example: 

```typescript 
const example = () => {
  try {
      processTransactions(transactions)
  } catch {
      showErrorMessage(error.message);
  }
}

const processTransactions = (transaction) => {
	if(isEmpty(transactions)){
		const error = new Error(‘No transactions!!’)
		error.code = 1
		throw error; 
}	
}
```


