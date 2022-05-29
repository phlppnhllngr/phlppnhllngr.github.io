---
title: PassKit
parent: Diverses
---

# PassKit
- [Apple - PassKit Web Service Reference](https://developer.apple.com/library/archive/documentation/PassKit/Reference/PassKit_WebService/WebService.html)
- [Apple - Updating passes](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html)
- <u>StackOverflow/User PassKit</u>
  - *There are a few special considerations for Passbook* (<https://stackoverflow.com/a/15878404/7437541>)
    - *1. All Pass push requests must be sent to the production APNS server (gateway.push.apple.com on port 2195)*
    - *2. You must use your Pass Type ID certificate and key to authenticate with the APNS server (do not use App APNS certificates)*
    - *4. The payload should be an empty - E.g. {"aps":""}*
    - *5. alert, badge, sound and custom property keys are all ignored - the push's only purpose is to notify Passbook that your web service has a fresh pass. The notification text will be determined by the changeMessage key in pass.json and the differences between the old and the new .pkpass bundles*
    - *6. The changeMessage string should contain %@ if you wish for the content of the value key to be displayed. Change messages may have static text in addition to the %@ variable, such as this: "changeMessage":"New updates: %@". If no %@ is provided, a generic message with the kind of pass is displayed: "Store card changed".*
    - *7. As of iOS9, if you modify more than one field at a time, only one generic message will be displayed on the lock screen.*
    - *~~8. You still need to regularly query the feedback service and purge expired/invalid pushTokens from your database~~*
- Apple Push Feedback Service
  - *The feedback service no longer exists in the HTTP/2-based APNs API. Instead, the APNs server will respond to a request to send a notification to a device that has uninstalled the destination app with an HTTP/410 response and a rejection reason of "unregistered," along with a timestamp at which the device token stopped being valid. Please see Sending Notification Requests to APNs for details. So, in short, no, you definitely don't need to be calling the feedback service if you're using the HTTP/2-based APNs API.*
  - *Tokens for uninstalled apps will return "success" for a while, until at some point the system decides it is OK to start returning 410. This can take several days after a notification is sent to a token after the app has been uninstalled. This is to prevent tracking of user behavior about installing/uninstalling apps, and is by design. It is acceptable to send notifications to these tokens until you receive a 410, after which you can delete the token from your database.* (<https://developer.apple.com/forums/thread/109376>)
