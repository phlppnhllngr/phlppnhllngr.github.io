---
title: PassKit & Google Wallet
parent: Diverses
---

# PassKit & Google Wallet

## PassKit
- <u>Apple Developer Docs</u>
  - [PassKit Package Format Reference](https://developer.apple.com/library/archive/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/PackageStructure.html) 
  - [PassKit Web Service Reference](https://developer.apple.com/library/archive/documentation/PassKit/Reference/PassKit_WebService/WebService.html)
  - [Wallet Passes](https://developer.apple.com/documentation/walletpasses)
    - [Adding a Web Service to Update Passes](https://developer.apple.com/documentation/walletpasses/adding_a_web_service_to_update_passes/) 
  - [Updating passes](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html)
  - [API Collection Wallet](https://developer.apple.com/documentation/passkit/wallet)
  - APNs
    - URL = https://api.push.apple.com(:443)/3/device/${pushToken}
          = gateway.push.apple.com:2195 ?
    - Header apns-topic=${passTypeIdentifier} benötigt?
    - <https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html>
- <https://developer.apple.com/de/support/expiration/>
- <u>StackOverflow/User PassKit</u>
  - *1. All Pass push requests must be sent to the production APNS server (gateway.push.apple.com on port 2195), there is no way to use the sandbox.*
  - *2. You must use your Pass Type ID certificate and key to authenticate with the APNS server (do not use App APNS certificates)*
  - *5. alert, badge, sound and custom property keys are all ignored - the push's only purpose is to notify Passbook that your web service has a fresh pass. The notification text will be determined by the changeMessage key in pass.json and the differences between the old and the new .pkpass bundles*
  - *6. The changeMessage string should contain %@ if you wish for the content of the value key to be displayed. Change messages may have static text in addition to the %@ variable, such as this: "changeMessage":"New updates: %@". If no %@ is provided, a generic message with the kind of pass is displayed: "Store card changed".*
  - *7. As of iOS9, if you modify more than one field at a time, only one generic message will be displayed on the lock screen.*
  - *~~8. You still need to regularly query the feedback service and purge expired/invalid pushTokens from your database~~*
  - *Passbook Serial Number: What characters are valid? What is the max length?*
    - *Pretty much any character can be used*
    - *400 characters also ingests ok.*
  - *the push payload should be empty [`{}`] for a Passbook push. Anything you do send will be ignored.*
  - *Unless %@ is present in the message, you will only ever see the generic message "Coupon Changed"*
  - *Change message updates are considered active updates. These used to vibrate and/or make a sound when they arrived, but Apple reduced this to simply waking the phone and displaying on the Lock Screen several releases ago. There is nothing that you can do as an issuer, or the customer can do on their phone to change this behaviour.*
  - *If your devices are updating and receiving the new passes, but you are not seeing a notification then it is most likely that your pass.json doesn't contain a changeMessage key.*
  - *In order for a notification to display: a pass data value must have changed (field labels, colours and images do not trigger updates), and the changed field must include the changeMessage key, preferably with a %@ placeholder that will be replaced with the new field value.*
  - *For Passbook, the APNS push's only purpose is to notify the device that the web service has fresh content. All notification activity is determined by the differences between the old and new pass.json files.*
  - *to help with privacy, the push tokens are regularly rotated - this may occurs at random, or with changes in hardware (user transferring to a new phone), or often with iOS upgrades. Your web-service API implementation will see this as a new registration request, and you will only learn that the old token is invalid through either the feedback APNS API (now deprecated), or by receiving a ExpiredProviderToken (403) response from the newer HTTP2 APNS API.*
  - `Passbook error [2013-03-22 11:10:28 -0700] Web service error for pass.com.example.purchase (https://www.example.com/): Server requested update to serial number '12345', but the pass was unchanged.` *This error occurs when a call from a device to: webServiceURL/version/devices/deviceLibraryIdentifier/registrations/passTypeIdentifier?passesUpdatedSince=tag, returns one or more serial numbers, and your web service returns a 302 response (or a 200 response but delivers an identical .pkpass bundle) to the subsequent call to: webServiceURL/version/passes/passTypeIdentifier/serialNumber. In the case of a 200 response, you will receive a second error message warning you that your web service ignored the last modified header and returned the full unchanged pass data. Normally, a device would request updated serials following a push request. In such cases, your pass has normally has changed and the alert does not trigger. However, Passbook also calls for updates serials immediately after a reboot and so you may be seeing a wave of these messages due to the recent 6.1.3 iOS update, as the freshly installed Passbook library calls your service to see if there are any updates available to older passes it has inherited. Also worth noting that, Passbook calls for updated serials by passTypeIdentifier. If you are issuing a push request for a one pass, but the device contains other passes with the same passTypeIdentifier, your web service may be inadvertently responding with serial numbers for these old passes. To fix it, you should look at your logic for handling the "Getting Serial Numbers" call to ensure that no serials are returned that would give a 302 response to a "Getting the Latest Version of a Pass" call.*
  - *The passUpdatedSince={tag} value is set from the last successful response that your web service gave to the requsest: https://{webServiceURL}/v1/devices/{deviceLibraryIdentifier}/registrations/{passTypeIdentifier}. You set it by providing a key of lastUpdated in the JSON dictionary response to the above request. The value can be anything you like, but the simplest approach would be to use a timestamp. The if-modified-since value is set by the Last-Modified HTTP header sent with the last .pkpass bundle received matching the passTypeIdentifier and serialNumber. Again, you can choose what value to send in this header.*
  - *If you are sending multiple notifications to the same device within a short period of time, the push service will send only the last one.*
  - *There are no caps or batch size limits for using APNs. The iOS 6.1 press release stated that APNs has sent over 4 trillion push notifications since it was established. It was announced at WWDC 2012 that APNs is sending 7 billion notifications daily.*
  - *you do need to modify a field in the pass to get a push notification to show. This is because, unlike with app pushes, a Passbook push payload does not determine the content of the notification. The purpose of a Passbook push message is to alert the device that the web service has a new pass with updated content. The alert text is determined solely by the new pass contents. Any content in the push payload is ignored. Apple advise a push notification with an empty JSON dictionary. If the following criteria are met, the device will display the notification provided in the changeMessage key:
The value has changed. The changeMessage contains the %@ string. Id the %@ string is not present, the pass will show a notification Pass Changed. If no changeMessage key is present for the changed value, no message will show.*
  - *This is what a successful registration looks like in the console: <https://stackoverflow.com/a/15633582/7437541>*
  - *If you fail to renew your certificate, then issued passes would remain valid indefinitely, but you would lose the ability to modify or update them in any way.*
  - Links: <https://stackoverflow.com/a/15878404/7437541>, <https://stackoverflow.com/a/14391001/7437541>, <https://stackoverflow.com/a/14927661/7437541>, <https://stackoverflow.com/a/38333199/7437541>, <https://stackoverflow.com/a/15213566/7437541>, <https://stackoverflow.com/a/54311888/7437541>, <https://stackoverflow.com/a/15583017/7437541>, <https://stackoverflow.com/a/15719781/7437541>, <https://stackoverflow.com/a/14845067/7437541> <https://stackoverflow.com/a/66989932/7437541>
- Apple Push Feedback Service
  - *The feedback service no longer exists in the HTTP/2-based APNs API. Instead, the APNs server will respond to a request to send a notification to a device that has uninstalled the destination app with an HTTP/410 response and a rejection reason of "unregistered," along with a timestamp at which the device token stopped being valid. Please see Sending Notification Requests to APNs for details. So, in short, no, you definitely don't need to be calling the feedback service if you're using the HTTP/2-based APNs API.*
  - *Tokens for uninstalled apps will return "success" for a while, until at some point the system decides it is OK to start returning 410. This can take several days after a notification is sent to a token after the app has been uninstalled. This is to prevent tracking of user behavior about installing/uninstalling apps, and is by design. It is acceptable to send notifications to these tokens until you receive a 410, after which you can delete the token from your database.* (<https://developer.apple.com/forums/thread/109376>)
- <https://medium.com/@yangzhoupostbox/asp-net-web-api-example-for-apple-wallet-passbook-a124a1d90bb3>


## Google Wallet
- **Google Docs**
  - <https://developers.google.com/wallet>
  - [Generic pass codelab: Integrate the Google Wallet API to digitize passes on web](https://codelabs.developers.google.com/add-to-wallet-web#0)
  - [YT 05/22: How to digitize any wallet object with the Google Wallet API](https://www.youtube.com/watch?v=iZz_8N9WPVA)
  - Google Wallet Samples
    - *contains samples for using the Google Wallet REST APIs*
    - *Each sample demonstrates the following: Authenticating using a Google Cloud service account, Creating Pass Classes, Creating/retrieving Pass Objects, Creating a signed JWT for use in a "Add to Google Wallet" URL*
    - letzter Commit: Mai 2022
    - <https://github.com/google-pay/wallet-samples>
  - passes-rest-samples
    - *demonstrates integration of the basic components of the Google Pay API for Passes*
    - *howcases several aspects of the API: Defining Class and Object resource definitions, Insertion of classes and objects via Google Pay API for Passes REST API, Signing a JSON Web Token that is used to generate save links or used in JS Web button*
    - letzter Commit: Juli 2020
    - <https://github.com/google-pay/passes-rest-samples>
- **Libs**
  - <https://developers.google.com/pay/passes/support/libraries>
