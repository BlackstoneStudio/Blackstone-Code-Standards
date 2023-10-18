# How to resolve conflicts with the UAT branch.

This commonly happens when we try to send a story to the UAT branch.
In this case we have to be more careful, since the UAT branch does not have to reach any branch ( according to our [git flow](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/blob/master/git/gitflow/gitflow.md) ).

We will create a new temporary branch from the story branch that conflicts with UAT, that temporary branch should have the same name as the story branch but with the '-UAT' suffix

### We need to do:

1. `git checkout UAT && git pull`
2. `git checkout story/TSK-### && git pull`
3. `git checkout -b story/TSK-###-UAT`
4. `git merge UAT`

**After that the conflicts should appear in your text editor, Please communicate with everyone involved in the project to resolve conflicts correctly and not overwrite other changes. Finally push the changes**

*After pushing the changes we need to delete the temporary branch that we created to resolve the conflicts*:

1. Delete from **local** repo:
   `git branch -D story/TSK-###-UAT`
2. Delete from **remote**
	`git push origin --delete story/TSK-###-UAT`