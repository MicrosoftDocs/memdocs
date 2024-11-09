---
# required metadata

title: Store a recovery key in Intune through the Company Portal website 
description: Upload and store your device recovery key from the Company Portal website.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/18/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid:

searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: annochiva
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Store your personal FileVault key   

*Applies to macOS*  

Store a FileVault key for your personally encrypted macOS device. In addition to satisfying encryption requirements, storing your key in Intune enables you to: 

* Easily and quickly retrieve or rotate the key from any device. 
* Ask your support person for help if you need to retrieve or rotate the key and can't access the apps or website to do it yourself.


## Retrieve or rotate the key

If you get locked out of your device, you can retrieve your key from the following locations:
   
- Company Portal website
- Company Portal app for iOS/iPadOS 
- Company Portal app for Android
- Intune app
 
 IT support people with administrator access to Intune can rotate your personal recovery key for you if you get locked out of your device. They can also view keys, but only the ones that belong to corporate-owned devices. IT support people can't view recovery keys that belong to personal devices.   


## Do I need to store my key?  
An IT support person will let you know if you're required to upload a personal recovery key. You may receive a notification from the Company Portal apps for iOS/iPadOS or Android if that's how your organization's IT department normally communicates with you.  

We only recommend uploading a recovery key if you fall into one of the following categories:
* You encrypted your device before you enrolled it with your organization. 
* You encrypted your device manually through macOS system preferences.   

Depending on your organization's policies, you might be blocked from accessing corporate resources on your device until you've uploaded your key.  

## Upload personal recovery key 
Complete these steps to save the personal FileVault key for your encrypted Mac device.  


1. Go to the [Company Portal website](https://portal.manage.microsoft.com) and sign in with your school or work account. 
2. Select your encrypted device.
3. Select **Store Recovery Key**.  
4. Enter your 24-character, alphanumeric FileVault key.  
5. Enter the key again. Then select **Save**.
6. Wait while Company Portal attempts to verify, rotate, and save your personal recovery key. No further action is needed once the key has been saved. If you leave the website before the upload is complete, you can follow up on the status the next time you sign in. 


## Company Portal messages
This section describes the messages you might see as you store a recovery key.    

|Message  |Meaning  |
|---------|---------|
|Keys must match. Check keys and try again.     | Appears under the **Confirm Recovey Key** box to let you know that your keys don't match each other. Retype the keys in both fields.      |
|Couldn't update recovery key for device.| Appears as a toast notification at the top of the screen to let you know that Company Portal couldn't store your recovery key. For more details, select your encrypted device. Then read the message at the top of the page for next steps. |
|We were unable to upload your recovery key. Check that you entered the correct key and try again. If the problem persists, try to manually rotate your key. Tap to learn more.     | Appears on the device's page and could mean a couple things: first, Company Portal couldn't rotate and save your key because the key you entered is incorrect. Verify that you have the right key and try again. Or second, your device hasn't checked in with your organization in a while. To sync the latest updates from your organization, select your device in Company Portal, and then select **Check status**. Then try to store the recovery key again. Finally, if the problem persists, it might mean that your organization hasn't enabled FileVault on their side. Contact your IT support person and let them know that you synced your device but are still unable to store your FileVault key.         |
|Your recovery key has been updated. If you ever get locked out of your device and need to retrieve your key, sign in to Company Portal and select **Get recovery key**.    | Appears on the device's page. The key you saved was successfully rotated and your new personal recovery key is stored.    |


## IT pro support

If you're an IT support person and want to configure and manage FileVault encryption for Mac devices in your organization, see [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md).  

## Next steps

You can always retrieve your key from the Company Portal website, the Intune app, and the Company Portal apps for iOS and Android, and use it to access your Mac device. To learn how to retrieve your recovery key, see [Get recovery key](get-recovery-key-cpweb.md).

Find out what else you can do in the Company Portal website. See [Using the Intune Company Portal website](using-the-intune-company-portal-website.md) for a list of actions.  

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
