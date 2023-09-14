# Styling Projects

### Using Sass

We know there are many good styling practices out there, but, after a lot of research we are going to stick with **SASS modules**, and here’s why. 

1. Sass is a stylesheet language that’s compiled to CSS. It allows you to** use **[https://sass-lang.com/documentation/variables](https://sass-lang.com/documentation/variables) **, **[https://sass-lang.com/documentation/style-rules#nesting](https://sass-lang.com/documentation/style-rules#nesting) **, **[https://sass-lang.com/documentation/at-rules/mixin](https://sass-lang.com/documentation/at-rules/mixin) **, **[https://sass-lang.com/documentation/modules](https://sass-lang.com/documentation/modules) **, and more, **all with a fully CSS-compatible syntax.
2. Sass helps keep **large stylesheets well-organized** and makes it easy to share design within and across projects.

| **Benefits**                                                                                                                                                                                                     | **Pros**                                                                                                                                                                                                          | **Cons**                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - **Not need huge resources** to work on big projects.
- Sass files are executed on the server and send CSS to the browser.
- **Provides functions, mixins, loops, variables, objects and even simple lists. **
 | - **Easy to learn** after CSS.
- helps us to have an introduction to **programming and algorithmic thinking.**
- Many legacy projects are done in SASS.
- **Community support **and fixes for many known issues.
 | - Necessary to understand the complete logic of SASS before understanding even the basic structure.
- Is **not compatible with other React libraries**.
- Class names can clash.
- **Requires knowledge of BEM and utility classes to implement efficiently.**
 |

> Let’s see a basic example of styling using sass modules.

> **To name your classes** please refer to our [Sass + BEM Methodology](#sass-bem) guide!

[component_file].module.scss

```sass 
.subtitle {
  color: $modal-blue; // Example of a variable
  text-transform: capitalize;

  @include formSubtitle; // Example of a mixin
}
```

styles/variables.scss

```sass 
$modal-blue: #003e7e;
```

styles/mixins.scss

```sass 
@mixin formSubtitle {
  margin: 0;
  font-size: 0.625rem;
  font-weight: 400;
  line-height: 1.25rem;
  letter-spacing: 0.2125rem;
  font-family: 'woodfordbourne-regular', sans-serif;
}

```

> Take a look at the full documentation on [https://sass-lang.com/documentation/](https://sass-lang.com/documentation/) 


---


### First of all, what is BEM?

**(Block. Element. Modifier)** is a naming methodology, which aims to solve many of the problems you’ll commonly encounter when naming classes and structuring your CSS/SCSS. It also does a great job of enabling you to create reusable front end components, which is **something we all strive for: to be healthy, wealthy and create reusable components.**

| **Benefits**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | **Pros**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | **Cons**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - **Clear and organized structure**: Makes the code easier to understand, maintain and update.
- **Reusable code**: By separating blocks, elements and modifiers into specific, reusable classes, BEM promotes code reuse and saves development time.
- **Scalability**: Can be applied to projects of any size and complexity, making it ideal for large and long-term projects.
- **Flexibility**: Can be adapted to different development environments and working tools.
- **Collaboration**: Facilitates collaboration between different developers and teams, as it provides a common standard for naming CSS classes and avoids conflicts in the code.
 | - **Compatibility**: Works with other web development methodologies and technologies, such as Sass, Less and React.
- **Efficiency**: Reduces the time and effort needed to write and maintain code.
- **Improves accessibility**: Better website accessibility by allowing screen readers to identify and navigate elements more easily.
- **Enables better code management**: Better code management as the project grows and changes over time by dividing code into blocks and reusable elements.
 | - **Increased complexity:** Having longer and more detailed class names can be especially **problematic for smaller or short-term projects**.
- **Larger number of classes:** A larger number of classes can be generated compared to other methodologies, which **can increase the size of the CSS file and negatively affect the loading speed of the website**.
- **Learning curve:** Implementing the BEM methodology requires some time and effort to become familiar with the structure and nomenclature, which can create a learning curve for developers new to the methodology.
 |

### But, how does this work? 

As the name says, we are going to have 3 main parts in our code: 

**The block**

The **component in question**, let’s say a card. 

> **It must have a clear and easy to understand name** that clearly indicates its function in the structure of the web page and what we want to achieve with it.

**The element**

A **single part from the block**, let’s say a card header, a `<p></p>` tag. **They are written by leading double underscores.**

> **Syntax: **`[name_of_block]__[name_of_element]`

**The modifier **

This is an **optional class that modifies the appearance or behavior** of the block or element. **This is written by leading double dash.**

> **Syntax:** `[name_of_block]__[name_of_element]--[name_of_modifier]`

> Let’s take a look at how it would look like in practice!

example.tsx

```typescript 
import React from 'react';
import styles from './example.module.scss';

export const Example = () => {
  return (
    // The block
    <div className={styles.card}>
        // The element                      // The modifier
        <p className={[styles.card__header, styles['card__header--active']].join(' ')}
          Organization User List
        </p>
    </div>
  );
};

```

example.scss

```sass 
// The block
.card {
  // The element
  &__header {
    color: red;
    margin-bottom: 20px;
    text-align: center;
    // The modifier
    &--active {
      font-weight: bold;
    }
    &:hover {
      // you can also use selectors!
    }
  }
```

> The `&` **essentially saves us rewriting the parent selector over and ove**r. What we end up with is the styles for our nav component encapsulated into a single block. Having the classes in one block like this makes it easy to identify, edit and move around.

> To look at some more examples you can click here! [https://andrew-barnes.medium.com/bem-and-sass-a-perfect-match-5e48d9bc3894](https://andrew-barnes.medium.com/bem-and-sass-a-perfect-match-5e48d9bc3894) .


---

## @import, @use and @forward sass

These directives are important in Sass because they allow you to import code from other Sass files, making it easier to organize and maintain CSS styles in large, complex projects. Here are some of the features and uses of each:

### @import

**Imports code from another Sass file and adds it to the current file.** However, it has some disadvantages, such as the possibility of name conflicts and the loading of unnecessary code.

> This is the oldest directive and has been **replaced by @use.** It can still be used in older versions of Sass, but it is recommended to avoid using it. 

### @use

This is the **recommended directive for importing code** from other Sass files in newer versions of Sass. @use has some advantages over @import, such as the creation of a scope to avoid naming conflicts, the ability to rename imported elements, and the elimination of unnecessary code loading. In addition, @use allows the import of complete modules and the export of elements for use in other files.

> Please refer to [https://sass-lang.com/documentation/at-rules/use](https://sass-lang.com/documentation/at-rules/use)  to learn more things about this like the use of variables and default values.

### @forward

This is a directive used in conjunction with @use to **re-export elements from one Sass file to another without adding additional scope.** @forward is useful when you want to create a module that groups several functions, mixins or variables and you want to import them all together into another file. **With @forward you can create one access point for all functions, mixins or variables without adding an additional scope.**

> Please refer to [https://sass-lang.com/documentation/at-rules/forward](https://sass-lang.com/documentation/at-rules/forward)  to learn more about this!.

> Let’s see an example!

global.scss

```sass 
// bad
@import 'variables';
// good
@use 'variables' as variables;
```

index.scss 

```sass 
@forward 'globals';
@forward 'mixins';
@forward 'variables';
```


---

## Global Styling

The creation of a directory with base styles for a project is i**ntended to optimize the work and maintain a consistent style throughout the application**. 

#### Benefits

- **Visual consistency**:  By defining global styles in one place, it ensures that visual elements throughout the application have a consistent look and feel. This improves the user experience when using the application, as users can better recognize and understand the design patterns and behaviors of visual elements. In addition, maintaining a consistent style throughout the application also contributes to the branding and visual identity of the application.
- **Time savings**: Defining global styles in a separate file saves time when writing style code. Instead of writing the same styles over and over again in multiple files, you can define them once and reuse them throughout the application. This also saves time when making style changes, as only the global style file needs to be modified instead of searching and changing each instance individually.
- **Improved performance**: By reducing the size of the style file through the use of global styles, application performance can be improved by reducing page load time. By reducing the amount of code that the browser must download and parse, you can speed up page load time and improve the user experience.

There are **4 important files **to include in this folder, we’ll guide you through them!

![Screen Shot 2023-04-28 at 9.56.14.png](./attachments/Screen%20Shot%202023-04-28%20at%209.56.14.png)
### Global** **

This file contains the styles that are applied to all elements of the application (`html,body,p, etc)`. By defining these global styles in one place, there is no need for you to write the same code throughout different files in your project.

global.scss

```sass 
html {
  box-sizing: border-box;
}
body {
  background: black;
}
h1 {
  font-size: 2.126rem;
}
```

### Mixins 

Mixins are blocks of code that can be reused in many parts of the application. For example, you can create a mixin for a button with a specific style and reuse it in different places throughout the application. This saves time and improves visual consistency throughout the application.

mixins.scss

```sass 
@use 'variables' as variables;

@mixin button ($bg,$fontColor){
  border: none;
  outline: none;
  color: $color;
  background: $bg;
  padding: 10px 20px;
  border-radius: 3px; 
}
```

### Variables

Variables are values that can be reused throughout the application's styling code. For example, you can define a variable for the main color of the brand and use it throughout the styling code. This way, if you need to change the main color of the brand, you only need to modify the variable instead of searching and changing each instance individually.

variables.scss

```sass 
@import url('https://fonts.googleapis.com/css2?family=Public+Sans:wght@200;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@300;400;500;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500;600;700&display=swap');

$font-family: 'Open Sans', sans-serif;

$primary-medium: #193c78;
$primary-bright: #006ef5;
$primary-dark: #061c40;
$primary-light: #cff3ff;
$primary-linkWork: #013e7d;

$secondary-dark: #d6d6d6;
$secondary-medium: #efecec;
$secondary-light: #f7f7f7;

$black: #000000;
$white: #ffffff;
$green: #008139;
$alert-red: #d62727;
```

### Normalize  

Normalize is a file used to make styles look the same in all browsers. Some browsers may interpret styles differently, which can cause visual inconsistencies. Normalize helps normalize these styles so that they look the same in all browsers.

normalize.scss

```sass 
html {
  line-height: 1.625rem;
  webkit-text-size-adjust: 100%;
}
```

### Index

This is the file where you want to import all the styles! 

index.scss

```sass 
@forward 'globals';
@forward 'mixins';
@forward 'variables';
@forward 'normalize';
```


---

## More good styling practices!

### Use of `rem` values instead of `px`

Within CSS, em and rem are both scalable units that also specify values of properties. em and rem meet[ ](https://www.w3.org/WAI/fundamentals/accessibility-intro/)[https://www.w3.org/WAI/fundamentals/accessibility-intro/](https://www.w3.org/WAI/fundamentals/accessibility-intro/) , and, unlike px, scale better. Consequently, **they are more suited for responsive design.**

- **em** is a CSS unit **relative to the font-size of the nearest parent element.**
- **rem** is a CSS unit** relative to the font size of an HTML element.**

When the root font-size is not explicitly set, rem values are **relative to the browser’s default font-size of 16px**.

**But, what does this mean?**

This means that when the root font-size is 16px, a value of 1rem would be` 16px * 1 = 16px`. And a value of 10rem would be` 16px * 10 = 160px`.

Don’t worry, we have a **helper conversion tool **if you need it. 

[https://www.w3schools.com/tags/ref_pxtoemconversion.asp](https://www.w3schools.com/tags/ref_pxtoemconversion.asp) 

> If you have any doubt about this you can refer to [https://blog.logrocket.com/using-em-vs-rem-css/](https://blog.logrocket.com/using-em-vs-rem-css/) 


