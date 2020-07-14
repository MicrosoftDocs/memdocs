---
# required metadata

title: Store a recovery key   
description: Upload and store your device recovery key from the Company Portal website.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/16/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
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
---

# Store a recovery key 

Store a personal recovery key to complete encryption for your already-encrypted device. In addition to satisfying encryption requirements, storing your key in Intune under the management of your IT admin lets you:

* Easily and quickly retrieve or rotate the key for your encrypted device from any device. 
* Ask your IT support person for help if you need to retrieve or rotate the key and can't access the apps to do it yourself.

> [!NOTE]
> IT support people with admin access in Intune can rotate personal recovery keys for device users. They can also view keys, but only those that belong to corporate-owned devices. They can't view the keys that belong to personal devices. (*LN: does "marked as corporate" = these macOS devices are "corporate-owned?" I wonder if the current phrase could cause confusion? I could imagine the device user/reader might say "well, the org could just mark my device as corporate and steal my recovery key." Why would an IT person want to see the recovery key?*) 

Should you get locked out of your device, you'll be able to retrieve your key from the following locations:
   
- Company Portal website
- Company Portal app for iOS/iPadOS 
- Company Portal app for Android
- Intune app


## Do I need to upload a key?
An IT support person will let you know if you're required to upload a personal recovery key. They may contact you over email, phone, or some other IT communication channel that's used in your organization. You won't receive a notification from the Intune or Company Portal apps. 

We only recommend uploading a recovery key if you encrypted your device before you enrolled it with your organization. 

Depending on your organization's policies, you might be blocked from accessing corporate resources on your device until you've uploaded your key.  

## Upload personal recovery key 
Complete these steps to upload a personal recovery key for your encrypted Mac device.

 (*LN: Will they receive  notification about encryption at all? How will they know anything is wrong if they missed the comms from their IT team? Will they get the standard "your device isn't encrypted" message?*)


1. Go to the Company Portal website and sign in with your school or work account.  (*LN: Is there a link we should share in this line?*)
2. Select your encrypted device.
3. Select **Store recovery key**. 
4. Enter your 24-character, alphanumeric FileVault key. 
5. Enter the key again. Then select **Save**. 
6. Wait while your key is uploaded. You'll see a success notification once the key has been stored.  (*LN: Do they really need to wait while it uploads? Will upload be fairly quick? After they key is uploaded, can they just close the website? Or do they need to do something else right now? If they get an error message, does that just mean that the key didn't match in both entry fields?*) 

## Company Portal messages

|Message  |Meaning  |
|---------|---------|
|Keys must match. Check keys and try again.     | Appears under **Confirm recovery key** to let you know that your keys don't match each other. Retype the keys in both fields and then try saving again.        |
|Couldn't update recovery key for <device name>. Row2     | Appears as a toast notification in the upper-right corner of the website to let you know that Company Portal couldn't store the recovery key you entered. Select your encrypted device. Then read the message in the grey box at the top of the page for next steps.       |
|We were unable to upload your recovery key. Check that you entered the correct key and try again. If the problem persists, try to manually rotate your key. Tap to learn more.     | Your organization hasn't enabled FileVault on their side yet, or your device hasn't checked-in with your organization in a while. On the device details page, under **Status**, select **Check access** to sync your device. Then try to store the recovery key again. If the problem persists, contact your IT support person and let them know that you synced your device but are still unable to store your FileVault key.         |
|Your recovery key has been updated. If you ever get locked out of your device and need to retrieve your key, sign in to Company Portal and select **Get recovery key**.    | Appears on the device details page to let you know that the key you saved has been stored.        |


(*LN: For the "we were unable to upload" message....I don't get how the CP validates the "wrong key" if it's the person's first time uploading the key. How would CP know that it's wrong?*)


## IT pro support

If you're an IT support person and want to configure and manage FileVault encryption for Mac devices in you organization, see [Use device encryption with Intune](/intune/protect/encrypt-devices).

## Next steps

Using the Company Portal website, the Intune app, and the Company Portal apps for iOS and Android, you can retrieve the recovery key and use it to access your Mac device.To learn how to retrieve your recovery key, see [Get recovery key](get-recovery-key-cpweb.md).

Find out what else you can do in the Company Portal website. See [Using the Intune Company Portal website](using-the-intune-company-portal-website.md) for a list of actions.  

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
