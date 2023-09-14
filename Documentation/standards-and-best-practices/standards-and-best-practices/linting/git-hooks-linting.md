# Git Hooks Linting

First, you need to setup ESLint, for this, you can take a look at our [ESLint configuration document](https://blackstonestudio.atlassian.net/wiki/spaces/BSD/pages/917438501/ESLint+Setup) (Page pending). Once you have linting setup in the project the next step is configuring and installing `Husky` and `lint-staged` inside the project. 

For this we need to run:

**yarn**

`yarn add --dev husky lint-staged`

**npm**

`npm i -D husky lint-staged`

In case the project has CSS as well make sure to run:

**yarn**

`yarn add --dev stylelint stylelint-config-standard`

**npm**

`npm i -D stylelint stylelint-config-standard`

⚠️ OR if your project uses .**scss **⚠️

**yarn**

`yarn add --dev stylelint stylelint-config-sass-guidelines`

**npm**

`npm i -D stylelint stylelint-config-sass-guidelines`

If the project use Typescript you must check that have the next dependencies:

``` 
@types/react
@types/react-dom
```

> If the project uses React Native you must install `@types/react-native`

This will install all the packages we need, now we need to setup Husky and Lint Staged in our package.json. So we’ll need to open this file in our IDE and add the following scripts:

> If your project use Typescript replace js,jsx for ts,tsx

``` 
"lint-staged": {
  "src/**/*.{js,jsx}": [
    "npm run lint:js:fix",
	"git add ."
  ]
},
"husky": {
  "hooks": {
    "pre-commit": "lint-staged"
  }
},
```

In the case that our project has CSS files we’ll add the following rule to lint-staged:

``` 
"src/**/*.{css,scss}": [
  "npm run lint:css:fix",
  "git add ."
]
```

Then we will create a **.stylelintrc** file and paste

``` 
{
  "extends": "stylelint-config-standard"
}
```

⚠️ OR if your project uses .**scss **⚠️

``` 
{
  "extends": "stylelint-config-sass-guidelines",
}
```

Additionally, you should add a couple of scripts to your package.json in order to make linting faster & easier. Go ahead and add the following:

> If you’re project use Typescript replace .js,.jsx for .ts,.tsx

``` 
    "lint:js": "eslint './src/**/*.{js,jsx}'",
    "lint:js:fix": "npm run lint:js -- --fix"
```

In case the project has CSS, add these ones as well:

``` 
    "lint:css": "stylelint 'src/**/*.{css,scss}'",
    "lint:css:fix": "npm run lint:css -- --fix"
```

The next immediate step is setting up Linters to run using CircleCI and instructions can be found on the Linting CI Configuration.



**Reference:**

- [https://github.com/typicode/husky](https://github.com/typicode/husky) 
- [https://github.com/okonet/lint-staged](https://github.com/okonet/lint-staged) 
- [https://stylelint.io/user-guide/get-started](https://stylelint.io/user-guide/get-started)
