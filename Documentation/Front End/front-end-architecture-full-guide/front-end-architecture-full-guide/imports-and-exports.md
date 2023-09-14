# Imports and Exports

The** export statement** is used in JavaScript modules to **share objects, functions, interfaces, variables, etc. **stored within the module with other files.

Ideally we should use named imports since they are easier to re-export and organize.

> The example below is for components, however it can be applied for  other files/folders including hooks, utils; etc.

#### Named exports 

```javascript 
// BAD
const MyComponentOne = (props) => (
  <div>
    // Your code here
  </div>
);

export default MyComponentOne;

// GOOD 
export const MyComponentOne = (props) => (
  <div>
    // Your code here
  </div>
);
```

Now we just need to add an `index.ts` file to export our component:

```javascript 
// BAD
import MyComponentOne from './MyComponentOne';

export default MyComponentOne;

// GOOD
export * from './MyComponentOne';
```

#### Exporting multiple files

Imagine we have several UI components inside our atoms, molecules, organisms and templates, so instead of import each component from its own path we can** import all from the same path:**

> This is really important to maintain a good and organized structure!

```javascript 
// BAD
import MyComponentOne from './atoms/MyComponentOne';
import MyComponentTwo from './molecules/MyComponentTwo';
import MyComponentThree from './organisms/MyComponentThree';
import MyComponentFour from './templates/MyComponentFour';

export {
  MyComponentOne,
  MyComponentTwo,
  MyComponentThree,
  MyComponentFour,
};

// GOOD
export * from './atoms';
export * from './molecules';
export * from './organisms';
export * from './templates';
```

```javascript 
// BAD
import MyComponentOne from 'src/components/atoms/MyComponentOne';
import MyComponentTwo from 'src/components/molecules/MyComponentTwo';
import MyComponentThree from 'src/components/organisms/MyComponentThree';
import MyComponentFour from 'src/components/templates/MyComponentFour';

// GOOD
import {
  MyComponentOne,
  MyComponentTwo,
  MyComponentThree,
  MyComponentFour,
} from 'src/components';
```

> If you need to rename your component it can be done this way:

```javascript 
import { MyComponentOne as NewName } from 'src/components';
```

> If you would like to know any more information about this section, please refer to the following links!

[https://blog.webdevsimplified.com/2022-07/react-folder-structure/](https://blog.webdevsimplified.com/2022-07/react-folder-structure/) 

[https://profy.dev/article/react-folder-structure](https://profy.dev/article/react-folder-structure) 

[https://www.bundleapps.io/blog/use-named-exports-over-default-exports-in-javascript](https://www.bundleapps.io/blog/use-named-exports-over-default-exports-in-javascript) 

[https://dev.to/vladimirvovk/default-exports-vs-named-exports-2jm0](https://dev.to/vladimirvovk/default-exports-vs-named-exports-2jm0) 


