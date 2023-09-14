# CircleCI

CircleCI is a continuous integration and continuous delivery (CI/CD) that uses jobs and workflows to automate the process of building, testing and deploying applications. The commands and orbs provide a convenient way to reuse and share common configurations.

Key components in CircleCI:

- **Commands**: Commands in CircleCI are custom commands that you can use in your jobs to perform specific actions. You can define custom commands to simplify and reuse common tasks in your CircleCI configurations.
- **Orbs**: Orbs are reusable CircleCI configuration packages. They provide predefined building blocks containing preconfigured jobs, commands, and parameters. Orbs allow easy reuse of common configurations and help standardize best practices in your workflows.
- **Jobs**: Jobs are independent units of work within a CircleCI workflow. Each job represents a specific task, such as compiling code, running tests, or deploying an application. You can define multiple jobs and specify their order of execution.
- **Workflows**: Workflows in CircleCI are sequences of jobs that represent the complete workflow for building, testing, and deploying an application. You can create custom workflows and specify how the jobs should be executed, including dependencies and conditions.

When using CircleCI, you can define job and workflow configurations in a YAML configuration file (known as **.circleci/config.yml**). This file describes how your applications should be built, tested, and deployed, and how the various components are related. Example:

```yaml 
version: 2.1
orbs:
  # The orb "circleci/aws-ecr@7.2.0" provides predefined commands to interact with Amazon Elastic Container Registry (ECR).
  aws-ecr: circleci/aws-ecr@7.2.0

# Sets default settings for all jobs. These settings include the working directory, the Docker image used (node:18.16.0)
defaults: &defaults
  working_directory: ~/repo/api
  docker:
    - image: node:18.16.0

# Defines a custom command called "ecr_publish" that uses the AWS ECR orb to build and push a Docker image to ECR. This command accepts parameters to specify the label and URL of the ECR account.
commands:
  ecr_publish:
    parameters:
      tag:
        type: string
      accountUrl:
        type: string
    steps:
      - aws-ecr/build-and-push-image:
          dockerfile: Dockerfile
          account-url: <<parameters.accountUrl>>
          aws-access-key-id: AWS_ACCESS_KEY
          aws-secret-access-key: AWS_SECRET
          repo: ${MY_APP_PREFIX}
          tag: <<parameters.tag>>

jobs:
  # It performs tasks such as code verification, dependency installation, code generation with Prisma, and linting execution (code style and quality verification).
  LintCheck:
    <<: *defaults
    steps:
      - checkout
      - attach_workspace:
          at: ~/repo/api
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "package.json" }}
            - v1-dependencies-
      - run:
          name: Install dependencies
          command: npm install
      - run:
          name: Prisma Generate
          command: npx prisma generate
      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package.json" }}
      - run:
          name: Run JS Lint
          command: |
            npm run lint

  # Performs similar tasks to "LintCheck", but also includes test execution.
  Test:
    <<: *defaults
    steps:
      - checkout
      - attach_workspace:
          at: ~/repo/api
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "package.json" }}
            - v1-dependencies-
      - run:
          name: Install dependencies
          command: npm install
      - run:
          name: Prisma Generate
          command: npx prisma generate --schema=./prisma/schema.prisma
      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package.json" }}
      - run:
          name: Run Test
          command: npm run test

  # It uses a specific executor called "aws-ecr/default" and performs the application deployment in a development environment. It uses the custom command "ecr_publish" defined above to push the Docker image with the "develop" tag to ECR.
  DeployDevelop:
    executor: aws-ecr/default
    steps:
      - ecr_publish:
          tag: develop
          accountUrl: AWS_ECR_ACCOUNT_URL

workflows:
  Build&Deploy:
    jobs:
      # The "LintCheck" and "Test" jobs are executed simultaneously.
      - LintCheck
      - Test
      # "Authorization" requires manual approval and that the "Test" and "LintCheck" jobs finish correctly, it is used to control the deployment in the "develop" branch.
      - Authorization:
          type: approval
          requires:
            - LintCheck
            - Test
          filters:
            branches:
              only:
                - develop
      # Is executed after the deployment has been approved in "Authorization" and is filtered so that it is only executed in the "develop" branch.
      - DeployDevelop:
          requires:
            - Authorization
          filters:
            branches:
              only: develop
```
