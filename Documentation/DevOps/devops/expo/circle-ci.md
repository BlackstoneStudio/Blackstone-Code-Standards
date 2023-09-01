# Circle CI

To setup an Expo project to create builds for `develop` and `master` branches we need to add some configurations to our `.circleci/config.yml` file. For this example we’ll assume you already have a CircleCi configuration file and we’ll just extend it with the necessary configurations. At the end of this document we’ll have a sample of the completed configurations file.

Firs we need to define our reusable job where we’ll add all the necessary values for our deployment, this gets added at the root lever of the `config.yml` file.



``` 
publish: &publish
  working_directory: ~/klearacne
  docker:
    - image: node:12.19
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



Now we need to add this to our jobs in CircleCI we can add this to an existing job using the following structure:

``` 
publish_to_expo_dev:
    environment:
      EXPO_RELEASE_CHANNEL: dev
      CARBON_BUILD_ID: circle-ci-v2
    <<: *publish
```

In the above example we’re defining a new jib and adding custom environment variables, then we’re re-using all the process in our re-usable job.

Finally here’s an example of a fully built CI configuration file:

> Final CircleCI Configuration
>
> ``` 
> version: 2
> publish: &publish
>   working_directory: ~/klearacne
>   docker:
>     - image: node:12.19
>   resource_class: xlarge
>   steps:
>     - checkout
>     - restore_cache:
>         keys:
>           - v1-dependencies-{{ checksum "package.json" }}
>           # fallback to using the latest cache if no exact match is found
>           - v1-dependencies-
>     - run:
>         name: Installing dependencies
>         command: |
>           npm install
>           npm install -g expo-cli
>     - save_cache:
>         paths:
>           - node_modules
>         key: v1-dependencies-{{ checksum "package.json" }}
>     - run:
>         name: Create app.json
>         command: |
>           node .carbon/build.js
>           cat app.json
>     - run:
>         name: SignIn into Expo
>         command: expo login -u $EXPO_USERNAME -p $EXPO_PASSWORD
>     - run:
>         name: Publish to Expo
>         command: expo publish --non-interactive --max-workers 8
> jobs:
>   SonarScan:
>     docker:
>       - image: sonarsource/sonar-scanner-cli
>     working_directory: ~/repo
>     steps:
>       - checkout
>       - run:
>           name: Create SonarQube Properties
>           command: |
>             printenv
>   LintCheck:
>     docker:
>       - image: node:12.19
>     working_directory: ~/repo
>     steps:
>       - checkout
>       - run:
>           name: Install Dependencies
>           command: |
>             npm install
>       - run:
>           name: Run JS Lint
>           command: |
>             npm run lint:js
>   publish_to_expo_dev:
>     environment:
>       EXPO_RELEASE_CHANNEL: dev
>       CARBON_BUILD_ID: circle-ci-v2
>     <<: *publish
>   CarbonBuild:
>     <<: *publish
>   publish_to_expo_prod:
>     environment:
>       EXPO_RELEASE_CHANNEL: default
>     <<: *publish
> workflows:
>   version: 2
>   QualityCheck:
>     jobs:
>       - SonarScan:
>           filters:
>             branches:
>               ignore:
>                 - master
>                 - develop
>       - LintCheck:
>           filters:
>             branches:
>               ignore:
>                 - master
>                 - develop
>   BuildDeploy:
>     jobs:
>       - publish_to_expo_dev:
>           filters:
>             branches:
>               only:
>                 - develop
>       - publish_to_expo_prod:
>           filters:
>             branches:
>               only:
>                 - master
> ```
