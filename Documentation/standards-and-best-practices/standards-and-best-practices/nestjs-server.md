# Nest.js Server

Here is a curated project example for you to imitate. Follow the getting started steps and base your test scripts on the ones validated here.

1. **Clone** the [**BLKS-73-nest-template**](https://bitbucket.org/blackstone_studio/blackstone-testing-framework/src/ace987326f3b77917bee78a6918c2e092f69c5f0/?at=feature%2FBLKS-73-nest-template) branch from the *Blackstone Testing Framework* repository.
2. **Open** the local project folder and install the dependencies: `npm install`
- Look at the [package.json](https://bitbucket.org/blackstone_studio/blackstone-testing-framework/src/ace987326f3b77917bee78a6918c2e092f69c5f0/package.json?at=feature%2FBLKS-73-nest-template) to be familiar with the framework and commands
3. **Run** the project and explore the server performance: `npm start`
4. **Inspect** the code and review the tests scripts at: `__tests__`
- Check the [React Testing Library guidelines](https://blackstonestudio.atlassian.net/wiki/spaces/TF/pages/475561985/Introduction+to+our+testing+stack#React-Testing-Library) to learn about the commands and test files.
5. **Adapt** the test scripts to your project. Follow this project’s explanation.


---

# [UT] Unit testing

## Using NestJS Test Library

Imagine we have some code with [NestJs](https://blackstonestudio.atlassian.net/wiki/spaces/TF/pages/475561985/Introduction+to+our+testing+stack#Nest-(Automated-Testing)). But this is not using entry points, nor the drivers can be tested separately. This makes it difficult to create unit tests. However, [NestJs](https://blackstonestudio.atlassian.net/wiki/spaces/TF/pages/475561985/Introduction+to+our+testing+stack#Nest-(Automated-Testing)) has its own library -based on Jest. It allows an application instance to be created which makes it easy to test specific modules or drivers.

```javascript 
const module: TestingModule = await Test.createTestingModule({
     imports: [
       Modules
     ],
     providers: [
	  Services
     ],
   }).compile();
 
   app = module.createNestApplication(); // Instance of the application is created
   service = module.get<Service>(Service); // A service is saved in a variable
   await app.init(); // The application for testing starts

```

At the example, we see how we can test parts of the application individually.

Doing unit tests with requests to GraphQL can become complicated. But if you want to test mutations and queries, try testing them with [Postman](https://blackstonestudio.atlassian.net/wiki/spaces/TF/pages/475561985/Introduction+to+our+testing+stack#Postman-%E2%80%93-Newman). Because verifying GraphQL requests is very simple. 

Here is an example when there is a pre-request script. This is useful when you want to test updates or delete mutations:

```javascript 
pm.sendRequest({
    url: pm.variables.get("variableName"), // Use an environment variable
    method: 'POST',
    header: {
        'Authorization': 'Bearer ' + pm.variables.get("variableName"), 
        "Content-Type": "application/json"
    },
    body: {
        mode: 'raw',
        raw: JSON.stringify({
            query: "mutation | query queryNAme (variables){
	    functionName(variables) {
	        Awnser
    	}
}",
            variables: {
               ”Variable”: “value”
            }
        }),
    },
}, function (err, res) {
    pm.environment.set("variableName", res.value); // Setting environment variable
});

```


