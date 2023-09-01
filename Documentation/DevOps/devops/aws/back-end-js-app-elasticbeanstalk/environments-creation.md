# Environments Creation

For an Elastic beanstalk application we need to create environments and the environments are where our application is going to run and be configured. Usually we’ll create 2 environments one for `Production` and one for `Development`, but in some cases we’ll need a third environment of `Staging`. If you have questions as to which environments are required please reach out to your Project Owner.

To create a new environment in our application we need to navigate to our app from the left navigation panel and then click on `Create a new environment`.



![Image from iOS (3).jpg](./attachments/Image%20from%20iOS%20(3).jpg)


In the next step we need to define our application type, for the vast majority of cases we’ll select `Web server environment` and click on `Select`.



![Image from iOS (2).jpg](./attachments/Image%20from%20iOS%20(2).jpg)


In the next step we’re going to create the environment’s name, we usually use the naming convention of `<AppName>-<EnvironmenName>`, so we would have something like `MyApplication-develop`. Then we copy this environment name and paste it in the domain section and click on `Check availability`. This will change the url of our deployment and will make future setups easier.

In the next section we need to select `Managed platform` and we’ll setup the platform’s configurations. In some cases where we have a docker configuration we can use a docker platform but in most cases we’ll be using `Node.js` for the Platform and the latest version of Node available as Platform branch and version. Then we want to deploy the application with some sample code as this will be the easiest to make sure the deployment is working and we’ll overwrite this code anyways when we do our first deployment.

Now we can go ahead and create our application version.



![Image from iOS (5).jpg](./attachments/Image%20from%20iOS%20(5).jpg)


Now we need to wait for the environment to finish being created.



![Image from iOS (4).jpg](./attachments/Image%20from%20iOS%20(4).jpg)


Once this process is completed our environment is ready to be used and should be deployed with some sample code in the URL we get in the header section.



![Image from iOS (6).jpg](./attachments/Image%20from%20iOS%20(6).jpg)

