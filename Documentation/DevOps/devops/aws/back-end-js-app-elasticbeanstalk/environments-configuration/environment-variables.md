# Environment Variables

Our environment is a cluster of servers that most likely will need environment variables in order to run properly, to do this we need to go into the `Software` section in our configurations.



![Image from iOS (9).jpg](./attachments/Image%20from%20iOS%20(9).jpg)


Inside Software we can to into `Environment properties` and edit all our variables. Please note that the environment variable of `PORT` is very important to set it up as EB will setup a reverse proxy with Nginx and it will use the `PORT` value to know where to listen for the node application we’re deploying.



![Image from iOS (8).jpg](./attachments/Image%20from%20iOS%20(8).jpg)
Once we’re ready and we’ve reviewed all settings we can go ahead and click on `Apply`, this will update our application’s environment and will take a couple of minutes.
