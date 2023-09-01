# CircleCI Configuration

This document will assume that the project you’re working with has an active CircleCI configuration. If it doesn’t the contact your project lead to solve this situation.

On every CircleCi configuration you’ll notice it is composed of to main sections `jobs` and `workflows`. We’ll need to add steps to both of them in order to have the Lint service run.

First we need to add a `job` add the following job to the end of the jobs list (Make sure the spacing is not changed by your IDE as it might invalidate the YML file)

If your project doesn’t have CSS add the following:

``` 
  LintCheck:
    docker:
      - image: node:10.15.0
    working_directory: ~/repo
    steps:
      - checkout
      - run:
          name: Install Dependencies
          command: |
            npm install
      - run:
          name: Run JS Lint
          command: |
            npm run lint:js
```

If your project does have CSS then this script should be added

``` 
  LintCheck:
    docker:
      - image: node:10.15.0
    working_directory: ~/repo
    steps:
      - checkout
      - run:
          name: Install Dependencies
          command: |
            npm install
      - run:
          name: Run JS Lint
          command: |
            npm run lint:js
      - run:
          name: Run CSS Lint
          command: |
            npm run lint:css
```



If your project needs to be built and has an `npm run build` command you will need to add one more step in your steps with the following content:

``` 
      - run:
          name: Build Project
          command: |
            npm run build
```

Now that we’ve defined our `job` in Circle CI we need to add it to our workflows we do this by adding `- LintCheck` inside `workflows>build-deploy>jobs`


