# Load Balancer

Our EB environment runs behind a load balancer and we need to do some configurations for it to support custom domains with an SSL certificate from ACM. So to edit this we need to click on `Load banacer`.

![Image from iOS (9).jpg](./attachments/Image%20from%20iOS%20(9).jpg)


In this section we want to click on `Add listener` in the `Listeners` section.



![Image from iOS (14).jpg](./attachments/Image%20from%20iOS%20(14).jpg)


Now we need to setup our listener, we want to set up Port to be `443` and protocol `HTTPS` . Next we need to select our certificate, if we don’t see one here we need to follow our ACM certificate creation process in the same region as our EB application.

Finally we want to choose the SSL policy, unless instructed otherwise, we want to use the latest available policy from AWS.

For Default process we want to leave this as `default`, with this we can now click on `Add`.



![Image from iOS (13).jpg](./attachments/Image%20from%20iOS%20(13).jpg)


It’s important to note that at this point we’ve created a listener, but we need to save it at the bottom of the form in order for this settings to be updated in our environment.


