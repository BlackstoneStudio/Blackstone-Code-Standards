# Understanding Reconciliation and Rendering In React.

![react-logo-2.png](./attachments/react-logo-2.png)
You probably already know what React is and what this library was made for (It is a Component-Based JavaScript library for building user interfaces, which renders elements on a web page. ***Maybe we already knew this, but do we really know how it does it?***).

Sometimes React may seem to be a super complicated library to understand. It may seem that way because we are probably not very familiar with the 2 most important concepts/processes of how React and Virtual DOM work: **Reconciliation & Rendering.**

- **Reconciliation:**
- Reconciliation is the process that React uses in which it takes the entire element node (components and elements) analyzes that content and makes a comparison with what is in the DOM and does a differentiation process. 
In essence, it calculates the difference that exists between your current components, their internal state, and properties with what exists in the DOM and it will output a difference. If there is no difference it is because the 2 are synchronized.
- **Rendering**:
- Consists of taking the differences that were calculated through the reconciliation process and making sure that they are applied in the DOM.

> This separation of steps in the React architecture allows us to create React applications that render in different environments (such as React native or Server Side Rendering).



The Virtual DOM is a very essential part of the reconciliation process. Suppose we have a React application, this component node once it is interpreted by the React library will return some kind of Object (obviously this is something internal to the library, not something that you as a developer will touch but it is important to understand it) this Object is itself the Virtual DOM, it is the representation of the page you want to render. 

But it itself does not have the knowledge of how to render, this is delegated entirely to part 2 which is rendering (In a nutshell: Reconciliation is inside React and Rendering is outside the React library).

We already know that the virtual DOM is created from the result of rendering components, but maybe we still don't know what is the purpose of the Virtual DOM. Maybe you have questions like: What was it created for? How does it behave? What is it for? Why is it necessary to have a real DOM and a Virtual DOM? What is the benefit? etc…

1. **Optimization:**
1. A modern React application requires to have a lot of changes constantly and very fast. The DOM is constantly changing and it is important that these changes do not degrade the user experience, i.e. are not slow, are optimal, and do not reflect some kind of wait. Therefore, these changes need to be optimized to render properly.
2. Because of this, React uses the Virtual DOM and abstracts the whole process of calculating the difference and rendering it so that you as a developer don't have to worry about these details. You focus on writing components and having those components interact with each other. All the logic of rendering it to the DOM is inside the library. If it is the case with other libraries that delegate all this work to the programmer, it is possible that this update is not performed in the most optimal way.
2. **Allows you to add a layer of abstraction and standardization:**
1. If you were to use native elements in the DOM you would realize that many of their properties do not have exactly the same name as they have in react, they are slightly different but different at the end of the day. So what React does is it creates standardized React elements with standardized names that are not going to change regardless of what happens in the native DOM elements and all those properties can be kept with standardized names. For example, all react elements have an "onChange" property and you can be sure that if you pass a function it will receive as its first parameter the instance of that Event (which is also standardized).
2. All this simplifies the development experience so that you don't have to deal with the small differences that may exist in elements in the browser. Especially if you come across some kind of browser that for some reason does not have the same support as another browser it would be a problem to deal with this case, but thanks to React you can standardize all those cases within the library, and you as a developer simply interact with the interface that React library is providing you with.
3. **Renderers:**
1. The rendering part can be abstracted to a separate library such as "react-dom". It allows you to not only mount a react application on a DOM element but also allows you to take a React application and render HTML in a string and this without the need for a browser, which allows you to have Server Side Rendering.
2. React Native allows you to take a node of elements and components and render them to an Android or iOS device.

> There are also other types of libraries that do not necessarily render to an environment, but for example allows you to have a testing environment for unit testing or any other type of testing of your components without the need to render the component in any environment.

> And remember, the user does not directly trigger changes in the UI but rather in the data / state of the application. Those changes are what trigger the UI update.
