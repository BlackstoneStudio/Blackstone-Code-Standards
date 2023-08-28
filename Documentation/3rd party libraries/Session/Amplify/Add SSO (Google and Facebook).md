# Setting Up Authentication with AWS Amplify

Follow these steps to set up authentication using AWS Amplify:

1. Run the command `amplify add auth`.

   PS: Do you want to use the default authentication and security configuration?
   - Select the option: "default configuration with social provider (federation)"

   PS: How do you want users to be able to sign in?
   - Select the option: "Email"

   PS: Do you want to configure advanced settings?
   - Select the option: "No"

   PS: What domain name prefix do you want us to create for you?
   - Press Enter

   PS: Enter your redirect signin URI
   - Enter your localhost project: "http://localhost:3000/"

   PS: Do you want to add another redirect signin URI?
   - Press "Y"
   - Enter your domain develop project: "https://project.develop.com/" (use "https")

   PS: Enter your redirect signout URI
   - Enter your localhost project: "http://localhost:3000/"

   PS: Do you want to add another redirect signout URI?
   - Press "Y"
   - Enter your domain develop project: "https://project.develop.com/" (use "https")

   PS: Select the social providers you want to configure for your user pool
   - Select with the space key: "facebook" and "google", then press Enter
   - add facebookAppIdUserPool, facebookAppSecretUserPool, googleAppIdUserPool and googleAppSecretUserPool when request

2. In your index project, implement this code:

```javascript
import awsConfig from './aws-exports';

const [localRedirectSignIn] = awsConfig.oauth.redirectSignIn.split(',');
const [localRedirectSignOut] = awsConfig.oauth.redirectSignOut.split(',');

const updatedAwsConfig = {
  ...awsConfig,
  oauth: {
    ...awsConfig.oauth,
    redirectSignIn: isLocalhost ? localRedirectSignIn : process.env.REACT_APP_REDIRECT_LOGIN_AMPLIFY,
    redirectSignOut: isLocalhost ? localRedirectSignOut : process.env.REACT_APP_REDIRECT_LOGIN_AMPLIFY,
  },
};

Amplify.configure(updatedAwsConfig);
```

3. In your .env file, add the following line:

```bash
REACT_APP_REDIRECT_LOGIN_AMPLIFY=https://project.development.com/
```

5. For more information, check this page: [Amplify Auth Social Provider Documentation](https://docs.amplify.aws/lib/auth/social/q/platform/js/#full-samples)

