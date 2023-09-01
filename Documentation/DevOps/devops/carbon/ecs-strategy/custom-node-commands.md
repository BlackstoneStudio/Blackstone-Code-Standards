# Custom Node Commands

Here we will learn how create a custom node command.

> For this tutorial we use [Yargs](https://yargs.js.org/). If you know a better library, please teel us.

### Defined our commands

First, we need to install yargs library using `npm install --save yargs`. To maintain organized our project, we recommend creating a config folder and inside of it a file where we declared our custom commands.

To explain how to create a command, we use the command of Taxaroo Carbon.

```javascript 
// config/yargs.js
const { argv } = require('yargs')
  .command('get-repo', 'Get repository from Bitbucket', {
    jstring: {
      alias: 'j',
      desc: 'Json string',
    },
  })
  .command('get-branch', 'Get branch', {
    jstring: {
      alias: 'j',
      desc: 'Json string',
    },
  })
  // More commands as you need
  .help();

module.exports = {
  argv,
};

```

As you can see, after the required we use the [command](https://yargs.js.org/docs/#api-reference-commandcmd-desc-module) function that accepts 3 arguments ([.command(cmd, desc, [module])](https://yargs.js.org/docs/#api-reference-commandcmd-desc-module)).

1. CMD - This is the command how called from our terminal.
2. DESC - A short description of what the command does.
3. MODULE - Here, declare the arguments that our command can accept. Each property is the name that how you can get the information when the command is used. You can specify an alias, a description that is very useful to help those who do not know what the command does or what parameters can send, and if the parameter is required, among other things (mode information [here](https://yargs.js.org/docs/#api-reference-commandcmd-desc-module)). 

> The function help is used to print in the terminal the descriptions of the command and properties automatically when the user puts `--help` as an argument.

### Calling our commands

To calling our custom command is very easy, only need to follow  the syntax `node file_name [command] [parameter] value`


