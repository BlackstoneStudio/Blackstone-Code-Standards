# The file is too big

This problem is mainly due to the Nginx configuration since by [default the maximum file size](https://linuxhint.com/what-is-client-max-body-size-nginx/) is 1m.

To extend this we can use the variable `client_max_body_size` in your server.

In elasticbeanstalk you can add the following file to extend the configuration of Nginx:

`.platform/nginx/conf.d/bodysize.conf`

``` 
client_max_body_size 100M;
```
