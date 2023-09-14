# First Steps (Storybook Setup)


---

Let’s create our React component library!

## Create a React Application

<sup>If you already have a React application you can skip this part and jump right into  to the installing section.</sup>

1. Create a new folder with the name of your component library. 

```powershell 
mkdir testing-sb
```

2. Initialize an empty NPM project with git

```powershell 
npm init 

git init
```

> You should also set up a [.gitignore](https://docs.github.com/en/free-pro-team@latest/github/using-git/ignoring-files) file. 

3.  Now we can add React and Typescript to our project

``` 
npm i --save-dev react react-dom @types/react typescript
```

> Since `react` requires that we need to have a single copy of `react-dom`, we will be adding it as a [peerDependency](https://flaviocopes.com/npm-peer-dependencies/) so that our package always uses the installing client's version.

`package.json`

```json 
...
"peerDependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
},
...
```

Let's also add a `tsconfig` for compiling our **TypeScript**

`tsconfig.json`

``` 
{
  "compilerOptions": {
    "target": "es5",
    "outDir": "lib",
    "lib": ["dom", "dom.iterable", "esnext"],
    "declaration": true,
    "declarationDir": "lib",
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react"
  },
  "include": ["src"],
  "exclude": ["node_modules", "lib"]
}
```

## Installing Storybook

1. Simply run 

```powershell 
npx sb init
```



To run the development server 

```powershell 
npm run storybook
```

And you are ready to go! Your storybook should be running in `http://localhost:6006`.


