# React Codestyle Guide

This guide will guide us to write with the best practices for better performance and maintenance for the future. Feel free to suggest new changes to this guide.

## ESLINT

We will have our own version of ESLINT for all the projects. Create the following file in your root file.


`` .eslintrc ``

```
{

  // The eslint file will go here once it's done.

}
```

## CSS
- Use CSS Modules for everything.
- Avoid !important word.

## Folder Structure.

The project should be separated in at least three directories:

```
blackstone-project/
|
|--- assets/
|
|--- pages/
|
|--- components/
|
|--- utils/

```

### assets/
Images, fonts, icons ,anything that will be static in the page and we can import it wherever we can use it.

### components/
Components folder. Any shared component (It is used in at least two other components) will be here. The structure will be explained below in this doc.

### pages/
Pages are the highest level of application's components. They represent the application routes and most times are displayed by a router.

### utils/
Any helper functions that are common across the project, like number/string comparision or something related to the business logic.

## Component Definitions.

- Components should have 200 lines maximum.
- Destruct the props of the component in the component declaration.
- Do not declare more than one component per file. If you need more components, you should nest a folder like it is explained below.
- One Style page for each component.
- One line per prop when you have more than 1.

### Import / Export Structure
```
Component
|
└── Component.jsx/Component.tsx
|
|-- Component.module.css // In neccesary cases.
|
|__ index.js / index.ts

```
The Component file you should do something like this.
```js
const Component = ({...propsDesctructured}) => {
  // component content
}

export default Component
```

And in the index file something like this:

```js
import Component from './Component'

export default Component.
```

If your component has one or more nested components, the folder structure should be like this:

```
Component
|
|-- NestedComponent1
|  |-- NestedComponent1.jsx / NestedComponent1.tsx
|  |
|  |-- index.js / index.tsx
|
|-- NestedComponent2
|  |-- NestedComponent2.jsx / NestedComponent2.tsx
|  |
|  |-- index.js / index.tsx
|
└── Component.jsx/Component.tsx
|
|-- index.js / index.ts
```


## More advices.

- Use Explanatory variables:

```js
const onlyNumbersRegex = /^\d+$/
const getNumberValidation = message => value => !onlyNumbersRegex.test(value) && message

const isNumber = getNumberValidation('error message')

isNumber(1)
```

- Use Searchable Names:

```js
const DAY_IN_MILLISECONDS = 86400000

setTimeout(doSomething, DAY_IN_MILLISECONDS)
```

- Disallow the use of 2+ empty lines in the middle of the code.

