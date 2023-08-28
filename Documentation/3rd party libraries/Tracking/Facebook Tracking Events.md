# Setting Up Facebook App Events with Expo

Follow these steps to set up Facebook App Events with Expo based on the [official guidelines](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#auto-events) and [Expo Facebook SDK](https://docs.expo.io/versions/latest/sdk/facebook/#facebooksetautologappeventsenabledasyncenabled-boolean-promisevoid) documentation:

1. Ensure you have the following:
   - [Facebook Developer Account](https://developers.facebook.com/apps)
   - [Facebook Ad Account](https://www.facebook.com/ads/manager/accounts/)
   - [Facebook app](https://developers.facebook.com/docs/apps)

2. **Automatic App Event Logging:** According to the [official guidelines](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#auto-events), there are three key events collected as part of the Automatic App Event Logging:
   - App Install
   - App Launch
   - In-App Purchase

3. Implement the following code in `src/Modules/API/Services/LogAppEventsService.js`:

```javascript
import * as Facebook from 'expo-facebook';

export default class LogAppEventsService {
  constructor() {
    this.facebook = Facebook;
    this.setAutoLogAppEvents = this.enableAutoLogAppEvents;
    this.setAdvertiserTrackingEnable = this.enableAdvertiser;
  }

  /**
     * enableAutoLogAppEvents
     * @param {boolean} enable - Parama that indicate if enable auto log app events or not
     */
  async enableAutoLogAppEvents(enable) {
    let success = null;
    try {
      this.facebook.setAutoLogAppEventsEnabledAsync(enable);
      success = true;
    } catch (error) {
      success = false;
    }

    return success;
  }

  /**
     * enableAdvertiserTracking
     * @param {boolean} enable - Parama that indicate if enable advertiser
     */
  async enableAdvertiser(enable) {
    let success = null;
    try {
      this.facebook.setAdvertiserIDCollectionEnabledAsync(enable);
      success = true;
    } catch (error) {
      success = false;
    }

    return success;
  }
}
```

**Remember that you need to be logged in to perform these actions.**

For manually logging events, you can refer to the official documentation and generate the corresponding code.

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/8793ac2d-e075-41db-8f92-bd1d69ddaf9c)

