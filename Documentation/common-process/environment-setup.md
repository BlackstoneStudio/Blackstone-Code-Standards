# Environment Setup
This configuration is focused on mac users, but it also works for Linux.

## Xcode installation and configuration (For Mac users only and the first thing you must install is)

1. **Open the App Store, search for Xcode and click get**.
	   ![Xcode First Step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/xcode+1.png)

2. **Open Xcode and accept the license.**
	   ![Xcode second step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/xcode+2.png)

3. **If your mac has M1 processor install Rosetta.**
	   ![Xcode third step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/xcode+3.png)

4. **Open preferences.**
	   ![Xcode fourth step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/xcode+4.png)

5. **Go to Locations and set Xcode under Command Line Tools.**
	   ![Xcode fifth step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/xcode+5.png)

## Brew installation and configuration (Mac users only)
You can follow the instructions on the [official website](https://brew.sh), the following process is the one we found there.

1. Open Terminal
2. Run `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
3. Execute the commands described in Next Steps (Terminal)
	   ![Brew step 1](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/brew+1.png)

## VS Code installation and configuration

Download VS code from the [official website](https://code.visualstudio.com/download "https://code.visualstudio.com/download") and install it.

1. Press `Command+Shift+P`(Mac)
2. Press `Ctrl+Shift+P` (Win/Linux)
3. Install ‘code’ command PATH
	   ![VS Code first step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/VS+Code+1+.png)

4. Go to **Preferences>settings** and Check `JS/TS › Implicit Project Config: Check JS` to improve error detections:
	   ![VS Code second step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/VS+Code+2.png)

**(Optional)** Install recommended extensions
- [https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments "https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments")

- [https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker "https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker")
- [https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint "https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint")

- [https://marketplace.visualstudio.com/items?itemName=mintlify.document](https://marketplace.visualstudio.com/items?itemName=mintlify.document "https://marketplace.visualstudio.com/items?itemName=mintlify.document")

- [https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode "https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode")

- [https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint "https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint")

- [https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log](https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log "https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log")

- [https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens "https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens")

## NVM installation and configuration
You can follow the instructions on the [official website](https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating "https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating"), the following process is the one we found there.

1. Open Terminal
2. Run `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash`
	   ![Nvm first step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/nvm+1.png)

3.  RUN `code ~/.zshrc` and add the following lines
 ```
 export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

![Nvm second step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/nvm+2.png)

4. Save and run `source ~/.zshrc`
5. NVM test with `nvm ls`
6. Install the version of Node to be used
    1. Run `nvm install 18` (LTS)
    2. Run `nvm install 16` (Old LTS)
       ![Nvm third step](https://blackstone-code-standards-images.s3.us-west-2.amazonaws.com/nvm+3.png)

## Other installations you may need

- GitHub SSH
    
    - [![](https://docs.github.com/assets/cb-600/images/site/favicon.png)Generación de una nueva clave SSH y adición al agente SSH - Documentación de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
        
    - [![](https://docs.github.com/assets/cb-600/images/site/favicon.png)Agregar una clave SSH nueva a tu cuenta de GitHub - Documentación de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
        
- React Native
    
    - [![](https://reactnative.dev/img/favicon.ico)Setting up the development environment · React Native](https://reactnative.dev/docs/environment-setup)
        
- PostgresSQL
    
    - [![](https://www.postgresql.org/favicon.ico)PostgreSQL: Downloads](https://www.postgresql.org/download/)