# Elastic Beanstalk Setup

The first step to get our application into ElasticBeanstalk is to set it up to work with EB. For this there are 2 ways of doing it. 

The first way is using the EB CLI, for this you will need to install the EB CLI. You can follow this instructions to do so:

[https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html) 

You will need to install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) if you don’t have it in your system already.



The alternate way, that is easier is to create a folder with the name `.elasticbeanstalk` and inside of this we need to create a file with the name `config.yml`

We can use the following code as a template for the contents of `config.yml`, here we’ll need to replace some values.

``` 
branch-defaults:
  develop:
    environment: <APPLICATION_ENVIRONMENT>
    group_suffix: null
global:
  application_name: <APPLICATION_NAME>
  branch: null
  default_ec2_keyname: null
  default_platform: Node.js 12 running on 64bit Amazon Linux 2
  default_region: us-east-1
  include_git_submodules: true
  instance_profile: null
  platform_name: null
  platform_version: null
  profile: taxaroo
  repository: null
  sc: git
  workspace_type: Application

```



In the template above we need to replace the values for `<APPLICATION_ENVIRONMENT>` and `<APPLICATION_NAME>` with the values of our application and environment that were setup in AWS.
