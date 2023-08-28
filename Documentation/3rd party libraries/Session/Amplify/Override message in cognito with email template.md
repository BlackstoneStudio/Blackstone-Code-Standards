## Override message in cognito with email template

Follow these steps to set up an override message in cognito with email template

1. Inside the user pool, go to "User pool properties."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/27ea10f7-6b15-46d6-88f8-9bd3a4e16e6d)


2. Click on "Add Lambda trigger."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/2e57ed0c-bd55-42ec-b9bb-317d9e894853)


3. Select "Messaging."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/b58cd64d-bcf8-4655-9ba8-7b94fee889ee)

4. Choose or create your "Lambda function."

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/743009b0-243b-403e-b8da-c1d3aad92260)


5. **Very important:** Your "Lambda function" must return the confirmation code in the "emailMessage" property.

6. Click the "Add Lambda trigger" button to complete the process.

## Example Lambda Function

Here's an example Lambda function that you can use:

```javascript
'use strict';

export const handler = async (event, context, callback) => {
  const name = event.request.userAttributes.name;
  
  const verifyEmail = (name, code) => `
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link
          href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,600;0,700;1,500&display=swap"
          rel="stylesheet"
        />
      </head>
    
      <body>
        <div style="width: 100%;font-family: 'Poppins', sans-serif;">
          <div style="background: linear-gradient(180deg, #40b1bb -2.88%, #80cbd1 100%);padding: 36px;text-align: center;">
            <img
              style="width: 260px;"
              src="https://invasion-website-assets.s3.us-west-2.amazonaws.com/intravelr_White_eb0d5a3f9d.png"
              alt="invasion"
            />
          </div>
          <div style="margin-bottom: 50px;">
            <div style="margin: 30px 0;padding: 16px;">
              <div style="margin: 30px 0;">
                <p style="font-weight: bold;font-size: 24px;">Verify your Account</p>
                <p style="font-weight: bold;font-size: 16px;">Hey ${name},</p>
              </div>
              <div style="text-align: center;">
                <p style="font-size: 16px;color: #595959;">Your 6-digit verfication code:</p>
                <p style="font-size: 16px;color: #595959;">${code}</p>
              </div>
              <p style="font-size: 16px;color: #595959;">
                Please type this code into the field to complete your account verification.
              </p>
            </div>
            <div style="width: 100%;border-top: 1px solid #c8c8c8;"></div>
            <div style="padding: 16px;">
             <p style="font-size: 16px;color: #595959;">
                  Should you have any questions or run into any problems, please reach out to us
                  thorugh email: <strong>support@intravelr.com</strong>
                </p>
            </div>
          </div>
          <div style="background: linear-gradient(180deg, #40b1bb -2.88%, #80cbd1 100%);padding: 36px;text-align: center;">
            <p style="color: white !important;font-size: 14px;">Please do not reply to this email.</p>
          </div>
        </div>
      </body>
    </html>
  `;
  
    const forgotPassword = (name, code) => `
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link
          href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,600;0,700;1,500&display=swap"
          rel="stylesheet"
        />
      </head>
    
      <body>
        <div style="width: 100%;font-family: 'Poppins', sans-serif;">
          <div style="background: linear-gradient(180deg, #40b1bb -2.88%, #80cbd1 100%);padding: 36px;text-align: center;">
            <img
              style="width: 260px;"
              src="https://invasion-website-assets.s3.us-west-2.amazonaws.com/intravelr_White_eb0d5a3f9d.png"
              alt="invasion"
            />
          </div>
          <div style="margin-bottom: 50px;">
            <div style="margin: 30px 0;padding: 16px;">
              <div style="margin: 30px 0;">
                <p style="font-weight: bold;font-size: 24px;">Forgot Password</p>
                <p style="font-weight: bold;font-size: 16px;">Hey ${name}, A request has been received to change your Intravelr Account Password</p>
              </div>
              <div style="text-align: center;">
                <p style="font-size: 16px;color: #595959;">Here is your verification code:</p>
                <p style="font-size: 16px;color: #595959;">${code}</p>
              </div>
            </div>
            <div style="width: 100%;border-top: 1px solid #c8c8c8;"></div>
            <div style="padding: 16px;">
             <p style="font-size: 16px;color: #595959;">
                  if you did not request this password change, please contact <strong>support@intravelr.com</strong> Thank you, The Intravelr team
                </p>
            </div>
          </div>
          <div style="background: linear-gradient(180deg, #40b1bb -2.88%, #80cbd1 100%);padding: 36px;text-align: center;">
            <p style="color: white !important;font-size: 14px;">Please do not reply to this email.</p>
          </div>
        </div>
      </body>
    </html>
  `;
  
  
  if (event.triggerSource === "CustomMessage_SignUp") {

    event.response = {
        emailSubject: 'Your verification code',
        emailMessage: verifyEmail(name, event.request.codeParameter)
    };
  }else if (event.triggerSource === 'CustomMessage_ForgotPassword'){
      event.response = {
        emailSubject: 'Your verification code',
        emailMessage: forgotPassword(name, event.request.codeParameter)
    };
  }
  
  callback(null, event);
};
```

For more information, view this [Link](https://docs.amplify.aws/lib/auth/emailconfirm/q/platform/js/)
