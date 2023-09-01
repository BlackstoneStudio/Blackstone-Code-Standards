# Route 53 [EB]

At this point we have a fully setup EB environment but we still need to make it wor with a custom domain, for this we’ll be using Route53, if your domain is not using this service then the procedure will be different.

Inside our Route53 application we need to navigate to the hosted zone where we want to create the custom domain in and we’ll click on `Create record`.



![Image from iOS (1).jpg](./attachments/Image%20from%20iOS%20(1).jpg)


In the next step we’ll setup our new DNS record, first we need to set the record name we’ll be using and then, since our application is in EB as well we can use `A` for `Record type` then we want to switch on the `Alias` section.

Now in the section of `Route traffic to` select `Alias to Elastic Beanstalk environment` and then select the AWS Region your application is in. After this in the next dropdown you should be able to select the environment you want to use.

> An `Alias` is how AWS references a custom integration between DNS settings inside Route53 and internal AWS services.



![Image from iOS (2).jpg](./attachments/Image%20from%20iOS%20(2).jpg)


Once this values have been reviewed we can go ahead and click on `Create redords`, this will create our new DNS records and propagation will start. It takes anywhere from 5 mins to 72 hours for DNS to fully propagate, but once this happens you should be able to see your application in your custom domain.
