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

Upload and store your personal recovery key in Intune to meet your organization's security requirements and protect your device. Storing your key ensures that you can [retrieve it]
(#retrieve-a-personal-recovery-key) later if the need arises. Should you get locked out of your device, for example, you can access your key on any device from the following locations:
   
- Company Portal website
- Company Portal app for iOS/iPadOS 
- Company Portal app for Android
- Intune app


Your personal recovery key is stored in Intune and managed by an IT administrator. An admin can:

* Rotate the FileVault recovery key for you.  (*LN: Why is this useful? Is there a good/common example for doing this? Will the user for sure have a managed device if they're taking these steps?*)
* View the personal recovery key, but only if your device is marked as *corporate*. An IT support person can’t see keys that belong to personal devices.  
(*LN: does "marked as corporate" = these macOS devices are "corporate-owned?" I wonder if the current phrase could cause confusion? I could imagine the device user/reader might say "well, the org could just mark my device as corporate and steal my recovery key." Why would an IT person want to see the recovery key?*) 

This article is especially helpful to people who encrypted their device before setting it up at work. Rather than start over with encryption, your organization may only ask you to upload your recovery key to Company Portal.  (*LN: Should I add that not all orgs do this? That this may not be available to them (if that's true)? Or don't mention that?*)

## Do I need to upload a key?
Someone from IT will let you know if you're required to upload a personal recovery key. They may contact you over email, phone, or some other IT communication channel that's used in your organization. You won't receive a notification from the Intune or Company Portal apps. 

Depending on your organization's policies, you might be blocked from accessing corporate resources on your device until you've uploaded your key.  

## Upload personal recovery key 
Complete these steps to upload a personal recovery key for your encrypted macOS device.

 (*LN: Will they receive  notification about encryption at all? How will they know anything is wrong if they missed the comms from their IT team? Will they get the standard "your device isn't encrypted" message?*)


1. Go to the Company Portal website and sign in with your school or work account.  (*LN: Is there a link we should share in this line?*)
2. Select your encrypted device.
3. Select **Store recovery key**. 
4. Enter your 24-character, alphanumeric recovery key. 
5. Enter the key again. Then select **Submit**. 
6. Wait while your key is uploaded. You'll see a success notification once the key has been stored.  (*LN: Do they really need to wait while it uploads? Will upload be fairly quick? After they key is uploaded, can they just close the website? Or do they need to do something else right now? If they get an error message, does that just mean that the key didn't match in both entry fields?*) 


## IT pro support

If you're an IT support person and want to configure and manage FileVault encryption for macOS devices in you organization, see [Use device encryption with Intune](/intune/protect/encrypt-devices).

## Next steps

To learn how to access your recovery key, see [Get recovery key](get-recovery-key-cpweb.md).

Find out what else you can do in the Company Portal website. See [Using the Intune Company Portal website](using-the-intune-company-portal-website.md) for a list of actions.  

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
