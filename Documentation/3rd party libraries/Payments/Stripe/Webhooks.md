## Adding a Webhook

To add a webhook, follow these steps:

1. First, create the webhook and determine the events it will trigger for. In this example, we will be listening for the `payment_intent.succeeded` event. For more detailed information, refer to the [Stripe documentation](https://stripe.com/docs/webhooks).

2. Access your dashboard and click on the "Developers" section.

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/b8a5e207-ee88-46ba-9b9e-779ff1c5808b)


3. From the left-hand menu, select "Webhooks."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/4b269a36-aafa-43bc-90b4-46722664bb0a)


4. Click on "Add endpoint."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/d2ff64cc-488f-43a9-8f98-9951804c7d29)


5. Provide the necessary details for your endpoint and choose the specific event you wish to monitor (in this case, `payment_intent.succeeded`).

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/99c9c574-9c5a-4767-a13e-45af84ce965c)


6. Lastly, click on "Reveal" to uncover the key. This key is used in your API to authenticate and validate incoming requests.

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/54d7dc7d-a9c9-45e9-b012-632203a6bb8e)
