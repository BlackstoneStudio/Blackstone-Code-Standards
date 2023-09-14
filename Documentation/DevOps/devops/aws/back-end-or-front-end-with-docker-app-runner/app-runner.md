# App Runner

1. We create a service in app-runner with the ECR repository previously created.

![Screenshot 2023-01-17 at 17.15.15.png](./attachments/Screenshot%202023-01-17%20at%2017.15.15.png)




2. Add the service name and environment variables, if necessary additional configurations.

![image-20220225-000717.png](./attachments/image-20220225-000717.png)
## Custom Domain (Optional)

1. Go to the service settings, in the custom domains tab click on "link domain".

![d2c84b87-033d-4d35-8860-098695d2a609.png](./attachments/d2c84b87-033d-4d35-8860-098695d2a609.png)


2. Enter your domain name.

![Screen Shot 2022-02-28 at 10.44.25.png](./attachments/Screen%20Shot%202022-02-28%20at%2010.44.25.png)
3. Copy the records name and values from step 1.

![04e38f89-ec38-45b6-822f-f7deab2a3fc0.png](./attachments/04e38f89-ec38-45b6-822f-f7deab2a3fc0.png)


4. Set this value in your domain provider.

Example [Route 53:](https://aws.amazon.com/es/route53/)

1. Create a record in your Route 53 hosted zone:

![Screen Shot 2022-04-21 at 11.14.50.png](./attachments/Screen%20Shot%202022-04-21%20at%2011.14.50.png)
![Screen Shot 2022-04-21 at 11.15.52.png](./attachments/Screen%20Shot%202022-04-21%20at%2011.15.52.png)
2. Set the CNAMEs with the name of the records and the previous values obtained.

![1adc73f8-c81a-42e8-b62a-ee8778e24c87.png](./attachments/1adc73f8-c81a-42e8-b62a-ee8778e24c87.png)


3. Verify new records.

![442d1848-b5cf-4e13-94ec-d127d5da5226.png](./attachments/442d1848-b5cf-4e13-94ec-d127d5da5226.png)



