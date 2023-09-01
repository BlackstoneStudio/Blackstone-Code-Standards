# CI User

When working on a project’s CI setup we need to create a `CI_USER` inside our AWS IAM configurations. This user will be configured inside our CircleCI deployments and will need to have credential policies for the services we'' be using in our project. 

For this example we’ll use the most common configuration for a project where we’re using `S3 + Cloudfront` for hosting a static HTML + JS app, like one built with React, and `Elastic Beanstalk` for an API service.

First we need to navigate to our user management console in AWS, for this navigate to the top right corner, and click on your organization's name, from here click on `My Security Credentials`.



![Image from iOS (6).jpg](./attachments/Image%20from%20iOS%20(6).jpg)


From here we’ll now be on a page where we can see our personal configurations, now we need to navigate to the section in the left navigation menu that says `Users`. This will show us a list of all our current users and from here, we’ll click on `Add User`.



![Image from iOS (5).jpg](./attachments/Image%20from%20iOS%20(5).jpg)


In the next step we’ll name our user and setup the type of user we want to create. Usually creating a user called `CI_USER` is recommended and for our cases we want this user to have `Programatic access` only as this will be used by CI machines.



![Image from iOS (2).jpg](./attachments/Image%20from%20iOS%20(2).jpg)


On the next step we’ll define the access permissions this user will have. Depending on the account configuration there might be a group that has the permissions that we need, but this will be rare and in the vast majority of cases we’ll click on `Attach existing policies directly` and select the policies we’ll be using for this user. 

Based on our example we’ll be attaching the following policies for the services we want the CI user to have:

- S3:  `arn:aws:iam::aws:policy/AmazonS3FullAccess`
- Cloudfront: `arn:aws:iam::aws:policy/CloudFrontFullAccess`
- Elastic Beanstalk: `arn:aws:iam::aws:policy/AdministratorAccess-AWSElasticBeanstalk`

![Image from iOS (1).jpg](./attachments/Image%20from%20iOS%20(1).jpg)


We can use the search functionality to find this policies faster, next we'll click on tags. We don’t usually add tags to a CI user but you can do this if the project requires so.



![Image from iOS (4).jpg](./attachments/Image%20from%20iOS%20(4).jpg)


After this step, we’ll review the configurations we’ve just setup for this user. It’s important that we review all the properties we’ve added to the user before we create it, they can be updated or changed afterwards, but it’s always better to create the user with the right configurations from the start as it will ensure we have the right configurations enabled once we start running deployments with CircleCI.



![Image from iOS (3).jpg](./attachments/Image%20from%20iOS%20(3).jpg)


Once we verify all is correct we can go ahead and click on `Create user` and in the next step we’ll be presented with the user’s credentials. It is crucial that we save this credentials as the `Secret access key` will only be shown in this screen and if lost it will need to be re-created.



![Image from iOS.jpg](./attachments/Image%20from%20iOS.jpg)
Usually we recommend downloading the credentials as a `csv` and storing them in a safe credential storing mechanism like 1Password.

At this point we have a fully configured CI User that can be integrated into any CircleCI deployment configuration.
