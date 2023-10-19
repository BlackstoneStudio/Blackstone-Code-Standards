# Git Flow & Task Process

## Task Creation (Local repo)

1. **Sync changes and create the task.**
   - Make sure you are in the "develop" branch and pull changes:
     ```shell
     git checkout develop && git pull
     ```

2. **Create the story in your local repo (If it is a new one).**
   - Create a new branch for the story, replacing `#` with the actual story or task number:
     ```shell
     git checkout -b story/TSK-#
     ```

3. **If the task is a subtask.**
   - Pull changes from the story branch, if any:
     ```shell
     git checkout story/TSK-# && git pull
     ```
   - Create a new branch for the subtask:
     ```shell
     git checkout -b subtask/TSK-#
     ```

## Push the Task.
   - This process should always be done before pushing changes. Merge conflicts are likely to arise; contact everyone involved in the project to resolve them.
   - Commit your changes (Refer to [Commit Guidelines](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/tree/master/commit)).
   - After committing your changes, sync changes with parent branches:
     ```shell
     git checkout develop && git pull
     ```
   - Sync "develop" into the parent story branch and push if there are changes in the story:
     ```shell
     git checkout story/TSK-# && git pull && git merge develop
     git push
     ```
   - Sync the story into your subtask:
     ```shell
     git checkout subtask/TSK-# && git merge story/TSK-#
     ```
   - Finally, push your changes:
     ```shell
     git push
     ```

## Stay In Sync With Your Local Branches
1. **Sync changes from develop**
   - Make sure you are in the "develop" branch and pull changes:
     ```shell
     git checkout develop && git pull
     ```
2. **Checkout into your story & pull changes**
   - ```shell
     git checkout story/TSK-# && git pull
     ```
3. **Sync develop changes into the story**
   - ```shell
     git merge develop
     ```
   - If the merge command bring us changes:
      ```shell
      git push
      ```
4. **Sync story changes with your subtask**
   - ```shell
     git checkout subtask/TSK-# && git merge story/TSK-#
     ```
*You can start from step 2 if you really want to stay in sync with a story in your subtask*

## Git Flow Reference
![Git Flow Reference](https://productive-files-production.s3.amazonaws.com/attachments%2Ffiles%2F003%2F246%2F034%2Foriginal%2F8ef76612-feb8-47ca-963a-2cd28b5fb62a.png)
