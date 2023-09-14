# UI Patterns

### View - Models (Domain Objects) - Custom Hooks

One of the most common ways to modularize an information-rich program is to **separate it into three broad layers**: 

1. Presentation (UI)
2. Domain logic (aka business logic)
3. Data access.

The benefit of this separation is that** it allows you to make changes in the underlying domain logic without worrying too much about the surface views, or vice versa**. Also, it can increase the re usability of the domain logic in other places as they are not coupled to any other parts.

> Let’s work around an Authentication example

![Screen Shot 2023-04-03 at 15.16.58.png](./attachments/Screen%20Shot%202023-04-03%20at%2015.16.58.png)
### Domain Logic

Let’s begin by defining our **Domain Object** `'AuthStrategy'`, that will contain 2 methods: `getLocalUser()` and `saveLocalUser()`.

authStrategy.ts

```typescript 
class AuthStrategy {
  isSSR: boolean = typeof window === 'undefined' || true;

  public getLocalUser(): User | undefined {
    if (!this.isSSR) {
      const storedUser = localStorage.getItem('user');
      if (storedUser) {
        return JSON.parse(storedUser);
      }
    }
    return undefined;
  } 
  
  private saveLocalUser(user: User): User {
    if (!this.isSSR) {
      const storedUser = this.getLocalUser();
      if (storedUser) {
        return storedUser;
      }
      localStorage.setItem('user', JSON.stringify(user));
    }
    return user; 
  }
  
  public async login(user: User): Promise<void> {
    const { data } = await this.client.post('/login', user);
    if (!this.isSSR) {
      this.saveLocalUser(user);
    }
    return data;
  }

}
```

### Data Access

The next thing we want to do is to create the logic for us to use this **Domain Object **and share the `state` and the `logic`** ** to our **Presentational Component**. Luckily in React, we can **define our own hooks** so we can have easy access to the data while applying reusability.

useAuth.ts

```typescript 

import { useEffect, useState } from 'react';
import AuthStrategy from '../models/login.strategy';
import { User } from '../types';

// We first create an instance of our Domain Object
const authStrategy = new AuthStrategy();

const useAuth = () => {
  // our state
  const [isLoggedIn, setIsLoggedIn] = useState<boolean>(false);

  const onLogin = async (user: User): Promise<void> => {
    try {
      // Domain Object login method
      await authStrategy.login(user);
    } catch (error: any) {
      throw new Error(error);
    }
  }

  useEffect(() => {
    // Get user from our Domain Object
    const storedUser = authStrategy.getLocalUser();
    if (storedUser) {
      setIsLoggedIn(true);
      return;
    }
    setIsLoggedIn(false);
    return;
  }, [])

  // return states and mehtods for our component
  return {
    isLoggedIn,
    onLogin,
  }
}
```

### Presentation (UI)

Now that we are done with the logic is **time to set our component**!

Login.tsx

```javascript 
import { Form, Input, Button } from '..';
import { useFormik } from 'formik';
import useAuth from '../../hooks/useLogin';

const SignUpForm: React.FC = () => {
  // We call our method from our data access
  const { onLogin } = useAuth();
  const { handleSubmit, handleChange, values } = useFormik({
    initialValues: {
      username: '',
      email: '',
      password: '',
    },
    onSubmit: values => onLogin(values),
  });
  return (
    <Form onSubmit={handleSubmit}>
      <Input name="username" value={values.username} onChange={handleChange} />
      <Input name="email" value={values.email} onChange={handleChange} />
      <Input name="password" value={values.password} onChange={handleChange} />
      <Button type='submit'>
        Login
      </Button>
    </Form>
  );
}

export default SignUpForm;
```

And easy as that we can keep our logic separated from our components! This is a great practice to keep a cleaner code.

> If you want to see the full code of this example please refer to [https://github.com/Gabriel-Cz/React-UI-Patterns](https://github.com/Gabriel-Cz/React-UI-Patterns) !

#### Things to take in consideration.

- We should be aware that **not everything should be done by hooks**, because the overlook of this ones can lead to performance issues in our application. 
- **Small computations can be done through domain objects** and make the view access directly to it.

#### Keys to understand CC, PC, Domain Objects and Hooks relationships.

- Our Domain Objects should encapsulated the business logic. 
- **Our Custom Hooks **have the data access, and more importantly they **should manage the state wherever they can if necessary**.
- Our Presentational Components should be a **pure function without any states in it**.
- Our Container Components should manage the information between view layer and props. This ideally with the use of ours custom hooks and useState, or, if the states overpass by 3 we can make use of react hook `useReducer` and in case of Form's input, use libraries such as [https://formik.org/docs/overview](https://formik.org/docs/overview) .
