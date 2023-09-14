# Custom Paths

When a project grows and we have many folders, the routes look super long, and the truth is that it doesn't look very flashy, for this **we can customize our routes in the tsconfig.json file!**

### Configuration 

> Syntax: {` “name_of_path": ['base_path_url']` }

tsconfig.json

```json 
{
  "compilerOptions": {
    ...
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  ...
}

```

Please take a look at more examples in the following links: 

- [https://dev.to/jimyhdolores/custom-patch-tsconfig-json-typescript-220f](https://dev.to/jimyhdolores/custom-patch-tsconfig-json-typescript-220f) 
- [https://www.typescriptlang.org/tsconfig#paths](https://www.typescriptlang.org/tsconfig#paths) 
