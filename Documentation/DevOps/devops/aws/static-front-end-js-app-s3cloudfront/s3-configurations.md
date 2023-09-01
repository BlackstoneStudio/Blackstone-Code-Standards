# S3 Configurations

To host a static JS appication like a CRA or Gatsby aplication we use S3 to host a static website. For this we need to create buckets and set them up so they can host a page. To start first we need to create your bucket with the application name and the environment like this: `my-application-development` and select the Region for this bucket.

![Screen Shot 2022-10-13 at 16.09.31.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.09.31.png)
On the next step, just click next as we won’t be making any changes here. The permissions section we actually want to enable public access as we’ll host a public website/app. So your configuration should look like this:

![Screen Shot 2022-10-13 at 16.10.15.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.10.15.png)
Now we will have created a new S3 bucket and we need to set it up, first we want to change its policy to allow us to get any object inside the bucket. We want to go into the bucket settings into Permissions > Bucket Policy.

![Screen Shot 2022-10-13 at 16.12.21.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.12.21.png)
And then, we want to add this policy:

``` 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<AWS_BUCKET_NAME>/*"
        }
    ]
}
```

*Replace `<AWS_BUCKET_NAME>` with your bucket name like on the attached screenshot.

After we save this configuration, we will want to go now into Properties > Static website hosting. We will now set this bucket to host a static website ans we want to direct index & error to `index.html` like in the following configuration:

![Screen Shot 2022-10-13 at 16.14.28.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.14.28.png)
![Screen Shot 2022-10-13 at 16.15.11.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.15.11.png)
Take note of the Endpoint URL as we will be using this in the next steps and now save this configuration.

![Screen Shot 2022-10-13 at 16.16.31.png](./attachments/Screen%20Shot%202022-10-13%20at%2016.16.31.png)
At this point our S3 bucket is set up to host a static website, just like the output of a React application build. So now we need to setup a Cloudfront distribution to handle our new bucket.


