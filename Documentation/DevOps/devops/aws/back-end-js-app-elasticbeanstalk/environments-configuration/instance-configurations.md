# Instance Configurations

Now that we have most of the configurations for our application we need to set up the settings for how updates are going to be made into our EB environment, by default it updates all instances at the same time. Ideally we want to change this so our application has no downtime when it’s being updated.

To do this we need to go into the `Rolling updates and deployemnts` section.



![Image from iOS (15).jpg](./attachments/Image%20from%20iOS%20(15).jpg)


In this next screen in Application deployments we want to setup `Rolling` for `Deployemnt Policy` and in `Percentage` we can set it up to `50%`.



![Image from iOS (12).jpg](./attachments/Image%20from%20iOS%20(12).jpg)


Once we’ve filled this settings and reviewed all looks good we can go ahead and save this configurations.
