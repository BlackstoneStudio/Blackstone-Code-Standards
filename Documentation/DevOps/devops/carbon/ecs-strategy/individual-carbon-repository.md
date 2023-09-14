# Individual Carbon Repository

This repository is in charge to create the Docker image, upload it to AWS and make a call to create the clusters, tasks, and services to the get project online.

### Circle CI config

Our Circle CI config needs to have specific settings and commands.

To explain this file, we’ll use the config on Taxaroo-Carbon.

```yaml 
version: 2

jobs:
  CarbonBuild:
    machine: true
    steps:
      - checkout
      - add_ssh_keys:
            fingerprints:
              - "67:2b:10:4c:2d:cd:b7:80:2b:7e:43:0c:63:73:c5:75"
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
            echo "[default]" >> ~/.aws/config
            echo "region = us-east-1" >> ~/.aws/config
            echo "output = json" >> ~/.aws/config
            echo "aws_access_key_id=${AWS_ACCESS_KEY}" >> ~/.aws/config
            echo "aws_secret_access_key=${AWS_SECRET}" >> ~/.aws/config
      - run:
          name: Clone repos and change branch
          command: |
            export NVM_DIR="/opt/circleci/.nvm"
            [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
            nvm install v10.20.0 && nvm use v10.20.0 && nvm alias default v10.20.0
            npm i
            node get-git.js get-repo -j "${BRANCHES_NAME}"
            node get-git.js get-branch -j "${BRANCHES_NAME}"
            node get-git.js copy-env -j "${BRANCHES_NAME}" -c "${CARBON_BUILD_ID}"
      - run:
          name: Create docker images
          command: |
            export NVM_DIR="/opt/circleci/.nvm"
            [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
            nvm install v10.20.0 && nvm use v10.20.0 && nvm alias default v10.20.0
            node get-git.js docker-images -j "${BRANCHES_NAME}"
      - run:
          name: Docker images push
          command: |
            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 372527289275.dkr.ecr.us-east-1.amazonaws.com
            export NVM_DIR="/opt/circleci/.nvm"
            [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
            nvm install v10.20.0 && nvm use v10.20.0 && nvm alias default v10.20.0
            node get-git.js docker-push -j "${BRANCHES_NAME}"
      - run:
          name: Call the post create
          command: |
            export NVM_DIR="/opt/circleci/.nvm"
            [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
            nvm install v10.20.0 && nvm use v10.20.0 && nvm alias default v10.20.0
            node get-git.js call-post-create -c $CARBON_BUILD_ID -b $BRANCH -r $REPO_ID

```

In line 4, we define the name of our Circle CI Job;

As you can see, first we specify the type of container. For this strategy, we use `machine: true`. This gives us a Linux virtual machine. This VM count with some need it installations but needed some extras.

First, we need to specify our ssh key passing our fingerprints to can clone repositories from our git server. To know how to get the fingerprints for Circle CI, [click here](https://circleci.com/docs/2.0/gh-bb-integration/#enable-your-project-to-check-out-additional-private-repositories).

First, we install the AWS CLI and make a file where we put our AWS credentials (Lines 11 - 30).

After this, the next commands we will use the [custom node commands](https://blackstonestudio.atlassian.net/wiki/spaces/BSD/pages/991985805/Custom+Node+Commands). This command accepts variables, some variables came from the Blackstone Carbon application, like `BRANCHES_NAME` or `CARBON_BUILD_ID`. Other variables are part of our project setting in Circle CI like `AWS_ACCESS_KEY` or `AWS_SECRET`. 

> In some commands, first, we export and install a different node version to use in our custom node commands, this is only if the node version does not work with our custom command node.

1. We clone all repositories necessaries, change the branches, and copy the .env files and Dockerfiles (Lines 31 - 40).
2. We create the Docker image for each repository (Lines 41 - 47).
3. We push the Docker images to AWS ECR (Lines 48 - 55).
4. We call the ‘post create’ function to finished to get online the project (Lines 61 - 67).
