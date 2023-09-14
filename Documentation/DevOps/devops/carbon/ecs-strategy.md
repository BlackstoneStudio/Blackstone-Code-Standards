# ECS Strategy

###### Contents



---

This strategy uses AWS ECS and for this implementation, we use Docker images. In this section, you will learn how to configure your project to automatically create the Docker image and upload it to AWS ECR through the Circle CI configuration.

To explain this strategy we will use the Taxaroo Project.

Taxaroo Project has multiple repositories linked to each other. This feature makes the strategy more difficult to implement.

First will see the setting file in Blackstone Carbon.

```javascript 
exports const taxaroo = {
  id: 'taxaroo',
  name: 'Taxaroo',
  projectKey: 'TAXR',
  boardId: '32',
  avatar: 'https://bitbucket-assetroot.s3.amazonaws.com/c/photos/2020/Aug/25/3435059862-1-Taxaroo-App-logo_avatar.png',
  hero: 'https://images.unsplash.com/photo-1490971688337-f2c79913ea7d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80',
  repositories: [
    {
      id: 'Taxaroo-API-V2',
      name: 'Taxaroo API',
      build: {
        enabled: true,
        strategy: 'ecs',
        job: 'CarbonBuild',
        branch: 'develop',
        carbonRepo: 'Taxaroo-Carbon',
        carbonBranch: 'develop',
        branches: {
          'Taxaroo-App': 'develop',
          'Taxaroo-Admin': 'develop',
          'Taxaroo-Clients': 'develop',
        },
      },
      sync: [
        {
          direction: 'local',
          cron: '0 * * * *',
          branches: {
            origin: 'develop',
            local: 'sync/develop',
          },
        },
      ],
      local: {
        git: 'github.com/BlackstoneStudio/Taxaroo-API-V2.git',
        defaultBranch: 'develop',
      },
      origin: {
        git: 'github.com/Software-as-a-Service-LLC/taxaroo-api.git',
        defaultBranch: 'develop',
        defaultBranchFrom: 'develop',
      },
    },
    // More repositories with the same properties
  ],
};

```

In the previous example, we indicate the strategy (ECS), the job (this is for Circle CI), the carbonRepo indicates the repository ( [individual-carbon-repository](./ecs-strategy/individual-carbon-repository.md)  ) that has all the information to create the Docker image and upload it to AWS ECR and call the function that creates everything for you need it to start the environment on AWS, the carbonBranch indicates the branch to will make the work, and branches indicate the repositories and branches that the current repository needs to be linked.

For this strategy need to have a repository in charge to create all things


