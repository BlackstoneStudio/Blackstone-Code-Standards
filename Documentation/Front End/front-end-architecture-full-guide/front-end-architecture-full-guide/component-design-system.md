# Component Design System

In addition to our [folder-structure](../front-end-architecture-full-guide/folder-structure.md) , inside our 'Components' directory we should follow the **Atomic Design Methodology.**

If you haven’t heard of it, it is a design system created for us to be able to modularize our project from the smallest peaces of code to the most complex ones without the need of having really large files.

This leads us to five distinct levels (or directories) in our 'Components' folder:

### Atoms

Atoms are the basic building blocks of matter. Applied to web interfaces, atoms are our **HTML tags**, such as a **form label**, an **input** or a **button**.

![Screen Shot 2023-04-24 at 12.14.53.png](./attachments/Screen%20Shot%202023-04-24%20at%2012.14.53.png)
### Molecules

Molecules are groups of atoms bonded together. For example, a form label, input or button aren’t too useful by themselves, but combine them as a **form** and now they can actually do something together.

![Screen Shot 2023-04-24 at 12.15.44.png](./attachments/Screen%20Shot%202023-04-24%20at%2012.15.44.png)
### Organisms

Organisms are groups of molecules joined together to form a relatively complex, distinct **section of an interface, like a Header or a Footer.**

![Screen Shot 2023-04-24 at 12.15.58.png](./attachments/Screen%20Shot%202023-04-24%20at%2012.15.58.png)
### Templates

Templates consist mostly of **groups of organisms stitched together to form pages**. It’s here where we start to see the design coming together and start seeing things like layout in action.

![Screen Shot 2023-04-24 at 12.18.59.png](./attachments/Screen%20Shot%202023-04-24%20at%2012.18.59.png)
### Pages

They are nothing more than **specific instances of the 'Templates' you just created**. ** **

![Screen Shot 2023-04-24 at 12.19.08.png](./attachments/Screen%20Shot%202023-04-24%20at%2012.19.08.png)
> If you have any doubts about this you can click here to view a full documentation on [https://bradfrost.com/blog/post/atomic-web-design/](https://bradfrost.com/blog/post/atomic-web-design/) .
