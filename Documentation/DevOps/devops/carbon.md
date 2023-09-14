# Carbon

Carbon is an in-house developed tool to support the Continuous Integration and manage our Continuous Delivery internal framework.

We created an special configuration for:



---

# Overview

To watch the project run on a server, we use different strategies to get up the application on AWS. This feature is part of Carbon.

To set up a project to get up on a server you need to make some configurations on AWS, Circle CI, and Blackstone Carbon.

### Blackstone Carbon

The first thing that we’ll see is what we need to add to our Blackstone carbon application.

In this project, we have a folder called ‘projects’ in the settings folder where we have a series of files called depending on the name of the project, where we have the basic information of what we will do.

These files are like a JSON file that has the key project and the board ID that they have in Jira, we assign it an ID and a name and it has a property where we place the repository that we want to build and upload to AWS.

*<sub>Blackstone example file</sub>*

```javascript 
module.exports = {
  id: 'blackstone',
  name: 'Blackstone',
  projectKey: 'BLKS',
  boardId: '17',
  avatar: 'https://bitbucket-assetroot.s3.amazonaws.com/c/photos/2020/Mar/23/2638871585-2-openmappr-logo_avatar.png',
  hero: 'https://images.unsplash.com/photo-1490971688337-f2c79913ea7d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80',
  repositories: [
    {
      id: 'Blackstone-Site',
      name: 'Blackstone Site',
      build: {
        enabled: true,
        strategy: 'cra',
        job: 'CarbonBuild',
      },
      local: {
        git: 'github.com/BlackstoneStudio/Blackstone-Site.git',
        defaultBranch: 'develop',
      },
    },
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

In the above example, we can see how we configure two repositories with different strategies.

The Strategy is where or how will be built the project, for the moment we have 3 different strategies.

- **CRA** - This is a React project that will be built on AWS S3 + Cloudfront.
- **Expo** - This is an Expo project that builds and publishes the mobile app on the Expo dashboard.
- **ECS** - This is a project that uses Docker images and needs to be connected with different parts that are in development too. This strategy is up in AWS ECS.

On each repository, you need to specify the strategy to follow, and the name of the job that will be called on Circle CI (Preferably use CarbonBuild).

> The id property in each repository needs to be exactly as to be the name on the Github repository.
> Example: [Blackstone-Site](https://blackstonestudio.atlassian.net/wiki/spaces/BG/overview) it is correct, blackstone-site is wrong, BlackstoneSite is wrong. 

### Circle CI config

The second thing that we gonna a see is what we need to put on our config file of Circle CI.

*<sub>Blackstone-Site example of CarbonBuild job for CRA strategy</sub>*

```yaml 
CarbonBuild:
    docker:
      # specify the version you desire here
      - image: nikolaik/python-nodejs:latest

    working_directory: ~/repo

    steps:
      - checkout
      - run:
          name: Install AWS CLI
          command: |
            curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
            unzip awscliv2.zip
            ./aws/install -i /usr/local/aws-cli -b /usr/local/bin
            aws --version
      - run:
          name: Setup AWS credentials
          command: |
            mkdir ~/.aws
            touch ~/.aws/config
            chmod 600 ~/.aws/config
            echo "[profile default]" > ~/.aws/config
            echo "aws_access_key_id=${AWS_ACCESS_KEY}" >> ~/.aws/config
            echo "aws_secret_access_key=${AWS_SECRET}" >> ~/.aws/config
      - run:
          name: Check ENV
          command: |
            printenv
      # Download and cache dependencies
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "package.json" }}
            # fallback to using the latest cache if no exact match is found
            - v1-dependencies-

      - run:
          name: Install Dependencies
          command: |
            yarn install

      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package.json" }}

      # run tests!
      # - run: yarn test
      - run:
          name: Build Application
          command: |
            CI=false yarn run build
      - run:
          name: Deploying to AWS S3
          command: |
            aws s3 sync public/ s3://${AWS_DEV_S3_BUCKET} --profile default --region ${AWS_DEV_REGION}
      - run:
          name: Invalidate Cloudfront Cache
          command: |
            aws cloudfront create-invalidation --distribution-id ${AWS_DEV_CLOUDFRONT_DISTRIBUTION} --paths "/*" --profile default
```

In the above example, we can see how to configure our Circle CI to make a release on Elastic Beanstalk.

When we want to upload the project on AWS we need to install the AWS CLI in our Circle CI container and add our credentials to a specific config file. This can be seen from line 15 to 31, and the “AWS_ACCESS_KEY” and “AWS_SECRETS” are environment variables in the Circle CI project configuration ([more info here](https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project)).

> The AWS credentials must have the correct permission to create the project on the required services.

Likewise, if our project uses the Expo strategy, we need to set our expo credentials as environment variables in the Circle CI project configuration.

This is only the big picture of how gets carbon build in our project. On the next page, we see all steps to set up each of the strategies.
