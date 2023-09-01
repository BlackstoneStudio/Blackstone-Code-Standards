# CORS error on video preview.

This error occurs when trying to play the video in the Media Libraries.

![Screen Shot 2022-07-01 at 11.40.26.png](./attachments/Screen%20Shot%202022-07-01%20at%2011.40.26.png)
This is due to the default S3 policies, all we have to do is update them and allow GET methods.
S3 > Buckets > My bucket > permissions > Cross-origin resource sharing (CORS) > Edit

``` 
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]
```
