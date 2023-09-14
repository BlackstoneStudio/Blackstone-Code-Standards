# Folder Structure

## First things first, **Folder Structure.**

Now, this may vary depending on what the project requirements are, this means, not all directories mentioned here are strictly needed and can be omitted, just as others can be added. But it must be said, this is basically **the directory structure we want to follow inside our /src folder**:

- **hooks**: This is useful to any size project since almost every single one will have **multiple custom hooks**, so having them in a single place is really handy!

> It will only store the global hooks that are used across multiple pages.

- **utils: **All** utility functions **such as for example, formatters.  All the files in this folder should be <ul>straightforward</ul>.
- **services: **All **code interactions with any external API**. Generally, on larger projects you will have many different APIs to interact with, and this folder is the right place to put all the code related to it.
- **assets: **This will contain sub directories such as **Fonts**, **Images** (png, jpg, etc), **Svg**, **Icons** (.Tsx files of the SVG’s), etc. for your project. Pretty much anything that isn't code related.
- **data: **This one is similar to the assets folder, but this is for storing our **data assets such as JSON files** that contain information used in our code (store items, theme information, etc).
- **styles**: Here we should place our Theme, global styles, etc.
- **routes: **Our defined routes. 

> Please refer to our [Route Handling](/wiki/spaces/~6148a35e7a3c880067277460/pages/2220720148) guide! 

- **types: **Here we should place our** Global Types**.
- **components: **This will contain **every single global component** for the entire project. 

> Please refer to our [Component Design System](/wiki/spaces/~6148a35e7a3c880067277460/pages/2221178913) guide! 

- **views**:

This directory should contain one sub directory per page inside your project. Each one of them must contain a** root file **(generally `index.js`) alongside all the **files and sub directories that are only applicable to that page. **

Let’s say, we have a `Login` page that only needs a component called `LoginForm`, and a custom hook called `useLogin`. 

We would end up with a **view directory** called `Login` containing the **root file** `index.js`, a **sub directory** for the `Login Form` and a **hook file** for the `useLogin` hook. 

> This component and hook are only ever used in the `Login` page so they are stored within the respective directory instead of being stored in the global `hooks` or `components` directory.

#### Example of some Optional Directories

- **redux: **All our **Redux files **and sub directories.
- **context: **All our **React Context** files and sub directories.
- **stories: **All our **Storybook stories**.
- **__tests__: **All our **tests files** and sub directories. 
