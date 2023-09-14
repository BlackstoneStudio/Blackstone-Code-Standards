# CRA Strategy

This strategy uses AWS S3 and AWS Cloudfront.

For this strategy, you need to config the AWS S3 where the project will be uploaded, and the AWS Cloudfront to cab have a path where we could see the project run.

To upload the project we will use Circle Ci like the next example.

```yaml 
// Job in .circleci/config.yml
CarbonBuild:
    docker:
      # specify the version you desire here
      - image: nikolaik/python-nodejs:latest

      # Specify service dependencies here if necessary
      # CircleCI maintains a library of pre-built images
      # documented at https://circleci.com/docs/2.0/circleci-images/
      # - image: circleci/mongo:3.4.4

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

The code above is how CircleCi can upload the project to AWS and deploy it in a development path. You need to put special attention to the name profile. Need to be the same in the config file (line 30) as in the command where call de s3 and CloudFront (lines 63, 67).
