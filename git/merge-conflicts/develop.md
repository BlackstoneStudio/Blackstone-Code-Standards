# How to resolve conflicts with the develop branch

This commonly happens when we try to send a story to the develop branch.
### We need to do:
1. `git checkout develop && git pull`
2. `git checkout story/TSK-###`
3. `git merge develop`

**After that the conflicts should appear in your text editor, Please communicate with everyone involved in the project to resolve conflicts correctly and not overwrite other changes. Finally push the changes**