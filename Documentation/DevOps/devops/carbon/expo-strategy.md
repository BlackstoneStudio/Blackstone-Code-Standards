# Expo Strategy

This strategy uses [Expo](https://expo.io/) to make the deploys.

```yaml 
publish: &publish
  working_directory: ~/klearacne
  docker:
    - image: node:10.15
  resource_class: xlarge
  steps:
    - checkout

    - restore_cache:
        keys:
          - v1-dependencies-{{ checksum "package.json" }}
          # fallback to using the latest cache if no exact match is found
          - v1-dependencies-

    - run:
        name: Installing dependencies
        command: |
          npm install
          npm install -g expo-cli
    - save_cache:
        paths:
          - node_modules
        key: v1-dependencies-{{ checksum "package.json" }}

    - run:
        name: Create app.json
        command: |
          node .carbon/build.js
          cat app.json
    - run:
        name: SignIn into Expo
        command: expo login -u $EXPO_USERNAME -p $EXPO_PASSWORD

    - run:
        name: Publish to Expo
        command: expo publish --non-interactive --max-workers 8

```

The code above is an example of how CircleCI config file has the Expo deploy. Is easy to know what is happening, after installing the dependencies, we install the Expo-CLI, and using Expo-CLI we make the login (line 32) and publish the project (line 36).\

This is the CircleCI configuration, but in carbon build we need to add, in the settings project, the repo and the strategy.

```javascript 
export const blackstone = {
  id: 'blackstone',
  name: 'Blackstone',
  projectKey: 'BLKS',
  boardId: '17',
  avatar: 'https://bitbucket-assetroot.s3.amazonaws.com/c/photos/2020/Mar/23/2638871585-2-openmappr-logo_avatar.png',
  hero: 'https://images.unsplash.com/photo-1490971688337-f2c79913ea7d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80',
  repositories: [
    {
      id: 'Blackstone-Native',
      name: 'Blackstone Native',
      build: {
        enabled: true,
        strategy: 'expo',
        job: 'CarbonBuild',
      },
      local: {
        git: 'github.com/BlackstoneStudio/Blackstone-Native.git',
        defaultBranch: 'develop',
      },
    },
  ],
};
```

In the code above, we can see that we have the Blackstone-Native repository, and in the build property we indicate the strategy and the job (the job is the name that we put in the CircleCI config file, for general we use CarbonBuild).

We need to be sure that the ID of the repository is exactly like the name of the repository in Github.
