---
title: PassKit
parent: Diverses
---

# PassKit
- <u>Apple Developer Docs</u>
  - [PassKit Web Service Reference](https://developer.apple.com/library/archive/documentation/PassKit/Reference/PassKit_WebService/WebService.html)
  - [Wallet Passes](https://developer.apple.com/documentation/walletpasses)
  - [Updating passes](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html)
    - URL = https://api.push.apple.com(:443)/3/device/${pushToken} ?
    - Header apns-topic=${passTypeIdentifier} benötigt?
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
  - Links
    - <https://stackoverflow.com/a/15878404/7437541> 4/2013
    - <https://stackoverflow.com/a/14391001/7437541> 1/2013
    - <https://stackoverflow.com/a/14927661/7437541> 2/2013
    - <https://stackoverflow.com/a/38333199/7437541> 7/2016
    - <https://stackoverflow.com/a/15213566/7437541> 3/2013
- Apple Push Feedback Service
  - *The feedback service no longer exists in the HTTP/2-based APNs API. Instead, the APNs server will respond to a request to send a notification to a device that has uninstalled the destination app with an HTTP/410 response and a rejection reason of "unregistered," along with a timestamp at which the device token stopped being valid. Please see Sending Notification Requests to APNs for details. So, in short, no, you definitely don't need to be calling the feedback service if you're using the HTTP/2-based APNs API.*
  - *Tokens for uninstalled apps will return "success" for a while, until at some point the system decides it is OK to start returning 410. This can take several days after a notification is sent to a token after the app has been uninstalled. This is to prevent tracking of user behavior about installing/uninstalling apps, and is by design. It is acceptable to send notifications to these tokens until you receive a 410, after which you can delete the token from your database.* (<https://developer.apple.com/forums/thread/109376>)

## Wallet-Apps für Android
<table>
  <thead>
    <tr>
      <td>Name</td>
      <td>URLs</td>
      <td>Store Downloads</td>
      <td>API?</td>
      <td>.pkpass importieren?</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Wallet Passes</td>
      <td>https://play.google.com/store/apps/details?id=io.walletpasses.android&hl=de&gl=US</td>
      <td>10 Mio+</td>
      <td>ja</td>
      <td></td>
    </tr>
    <tr>
      <td>PassWallet</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
     <tr>
      <td>Pass2U</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
