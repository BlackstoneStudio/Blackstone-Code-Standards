# Route 53 [FE]

With our S3 & Cloudfront distribution created we need to setup our DNS records so we can point our domain to our site. We want to go to the hosted zone in Route53 for the domain we want to use and we want to create a new record using the `Simple Routing` option.

In the next screen we want to `Define simple record`here we will setup a CNAME record to our cloudfront distribution.

![Image from iOS.jpg](./attachments/Image%20from%20iOS.jpg)


![Image from iOS (1).jpg](./attachments/Image%20from%20iOS%20(1).jpg)
Now we want to create this record and our setup for the environment is ready and we should proceed to setup our repository and CI configurations.
