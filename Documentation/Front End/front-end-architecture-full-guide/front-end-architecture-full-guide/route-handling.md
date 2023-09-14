# Route handling


---

Here is a simple example on how to handle the routes on your project by using **react-router-dom**!

App.tsx

```typescript 
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import './styles/index.scss';
import { routes } from './routes';
import { RootLayout } from './components/templates';

const App = () => {
  return (
    <div>
      <Routes>
        {routes.map((route) => (
          <Route
            key={route.path}
            path={route.path}
            element={
              <RootLayout
                title={route.title}
                breadcrumbs={route.breadcrumbs}
                variant={route.variant}
              >
                {route.element}
              </RootLayout>
            }
          />
        ))}
      </Routes>
    </div>
  );
};

```

routes/index.tsx

```typescript 
import React from 'react';
import { PathRouteProps } from 'react-router-dom';

import {
  Home,
} from '../pages';

export const routes: PathRouteProps[] = [
  {
    path: '/',
    element: <Home />
  }
]
```

index.tsx

```typescript 
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);
root.render(
  <React.StrictMode>
    <BrowserRouter>
          <App />
    </BrowserRouter>
  </React.StrictMode>
);

```
