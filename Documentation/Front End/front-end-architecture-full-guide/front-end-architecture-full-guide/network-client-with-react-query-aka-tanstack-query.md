# Network Client with React Query, aka, TanStack Query.

This powerful library is a good solution to the challenges presented by long, complex, and sometimes repetitive code used to make API requests. 

It offers a powerful** asynchronous state manager** that can be used for many interesting tasks, such as:

- Cache handling
- Periodic updates
- Easy pagination creation
- Error and data control among other functionalities. 

| **Benefits**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | **Pros**                                                                                                                                                                                                                                                                                                                                                                                 | **Cons**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - Simplifies application status management.
- **Increases speed** and improves user experience by** reducing data loading time**.
- Automatically handles the retrying of unsuccessful requests.
- **Provides an easy-to-use API for queries and mutations.**
- Allows manual and programmatic cache invalidation for data updates.
- Configurable cache that allows customization of idle time and cache data lifetime.
- Local and global caching, allowing **reuse of data between different components**.
- Stale time management, which allows you to define how long the cache is considered fresh before it needs to be refreshed.
- **Refreshing cache data in the background without crashing the UI.**
 | - Provides a **common interface for cache data **and ongoing requests.
- Improves application scalability by reducing server load.
- Helps **keep code organized** and readable.
- Provides clear and comprehensive documentation.
- Supports extension and customization by creating c**ustom plugins and hooks**.
- Facilitates the implementation of pagination and infinite scroll.
 | - There can be a learning curve at first to fully understand the functionality and syntax of React Query.
- Caching can be a double-edged sword, as if not managed correctly, it can lead to out-of-date or incorrect data.
- In some cases, there can be an increase in code complexity when using React Query compared to simpler approaches.
- **Over-engineering can be a problem if React Query is used for simple tasks that could have been handled without it**.
- In situations of low connectivity or network latency, the React Query cache may not be useful and additional error handling logic would be required.
 |

### useQuery() hook

Used to handle our API queries. **It consists of 3 parts:**

**The first two are required: **

- **The name of the query**: It will be used to identify it within the QueryClient**.**

> It needs to be **enclosed in brackets**

- **An asynchronous function**: It will be responsible for making the HTTP request. 

**The third and optional:**

- **Object of configuration options**: It allows us to customize the behavior of the query, such as setting the data's cache lifetime or indicating whether the query should automatically refresh in the background.

example.ts 

```typescript 
  const query = useQuery(['name_of_query'], () => queryFunction(limit), {
    // Object of config options 
  });

```



> Let’s se an Example! 

### Integrating useQuery()

Let's begin by creating our **Axios instance to use our API** (highly recommended).

api.ts

```typescript 
import axios from 'axios';

export const pokeApi = axios.create({
  baseURL: 'https://pokeapi.co/api/v2',
});

interface ControlAxiosProps {
  url: string;
  method?: MethodType;
}

type MethodType = 'get' | 'post' | 'delete' | 'patch';

export const controlAxios = async <T>({
  url,
  method = 'get',
}: ControlAxiosProps): Promise<T> => {
  const { data } = await pokeApi[method]<T>(url);
  return data;
};
```

Next step is to make use of this instance in our `useQuery()` hook:

useQuery.ts

```typescript 
import { useQuery } from '@tanstack/react-query';
import { controlAxios } from '../api/pokeApi';
import { PokemonDetails } from '../interfaces';

// API endpoint call
const getPokemons = (limit: number) =>
  controlAxios<PokemonDetails>({ url: `pokemon?limit=${limit}` });

export const useQueryPokemons = (limit: number) => {
  // useQuery from react query
  const query = useQuery(['pokemons'], () => getPokemons(limit), {
    // Object of config options (listed below)
  });

  return { query };
};
```

And finally the component!

component.ts

```typescript 
import { useQueryPokemons } from '../hooks/useQueryPokemons';

export const ReactQuery = () => {
  const { query } = useQueryPokemons(50);

  if (query.isError) {
    return <h1>Error</h1>;
  }

  return (
    <div>
      {query.isLoading && <h1>...loagin</h1>}
      {query.data?.results.map(({ name, url }) => (
        <p key={url}>{name}</p>
      ))}
    </div>
  );
};
```



**The code is  clean and  readable isn’t it?**

Instead of dealing with the complexity of manually managing API data and state, you can **simply make use of **`useQuery()`**  from React Query.** This makes the process of creating API-consuming applications much more efficient and enjoyable.

### Properties

As you could see, besides getting the data from the query, we made use of other features like **manage loading and error handling.**

`useQuery()`** provides us with several other properties **to control the behavior of the component. 

We made you a list of the most important ones:

- `query.data`: contains the response from the API.
- `query.error`: contains the error if there was an error while making the request.
- `query.isError`: a boolean indicating if there was an error.query.
- `isFetching`: a boolean indicating if a request is currently being made.query.
- `isPaused`: a boolean indicating if the query is paused.query.
- `isSuccess`: a boolean indicating if the request was successful.query.
- `isLoading`: indicates if the request has finished.
- `loading.query.status`: indicates the HTTP status of the query.

### Configurations

There are plenty of configurations you can use to add certain functionality to your query, here are 2 of the most basic ones: 

`onSuccess()`, `onError()`:

As the name mentions, these functions are executed if the request is successful or if it fails.

```typescript 
const query = useQuery(['pokemons'], () => getPokemons(limit), {
    onSuccess: ()=> console.log('Success!!'),
    onError: ()=> console.log('Something went wrong!')
});
```

> We invite you to take a look to the full documentation about all the configurations you can use! [https://tanstack.com/query/v4/docs/react/reference/useQuery](https://tanstack.com/query/v4/docs/react/reference/useQuery) 



Now that we have the theory, let’s begin with the installation so you can start putting this in practice!

### Installation

``` 
$ npm i @tanstack/react-query
# or
$ pnpm add @tanstack/react-query
# or
$ yarn add @tanstack/react-query
```

> You can refer to [https://tanstack.com/query/v4/docs/react/installation](https://tanstack.com/query/v4/docs/react/installation) 

Also, installing **React Query Devtools** is completely optional, but it is highly recommended to use them as they are an essential tool for understanding the internal workings of the library and debugging potential errors.

``` 
$ npm i @tanstack/react-query-devtools
# or
$ pnpm add @tanstack/react-query-devtools
# or
$ yarn add @tanstack/react-query-devtools
```

> Your can refer to [https://tanstack.com/query/v4/docs/react/devtools](https://tanstack.com/query/v4/docs/react/devtools) 

### Set up

1. **Create an instance of QueryClient** 

```typescript 
const cliente= new QueryClient();
```

1. Wrap your application with the QueryClientProvider component

, passing the QueryClient instance as a prop:

```typescript 
<QueryClientProvider client={cliente}>
  // Your application content goes here
</QueryClientProvider>
```

1. 

**Place the ReactQueryDevtools component **inside the QueryClientProvider component:

``` 
<QueryClientProvider client={cliente}>
  <ReactQueryDevtools  />
  // Your application content goes here
</QueryClientProvider>
```

5.-Finally, **make sure your application is inside the QueryClientProvider component**. It should look like this:

``` 
import React from 'react';
import ReactDOM from 'react-dom/client';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

import { App } from './App';
import './index.css';

//tools react-query
const cliente = new QueryClient();

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <QueryClientProvider client={cliente}>
      <ReactQueryDevtools />
      <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

And that’s it, you are ready to start working!

> If you want to see the full code of this example please refer to [https://github.com/RunyShark/react-query](https://github.com/RunyShark/react-query)!




