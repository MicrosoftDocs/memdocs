---
# required metadata

title: Set up new iPhone | Microsoft Intune
titlesuffix: Microsoft Intune
description: Learn how to migrate old iPhone that's already enrolled to a new iPhone. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2023
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

ms.reviewer: rishitasarin  
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# iPhone setup guidance for work or school  

Set up a new or existing iPhone for work access. This article describes how to:     

* Set up a new iPhone. 
* Migrate settings and apps from an active iPhone that can access protected work resources and is set up for multifactor authentication (MFA) to a new iPhone. 

Review all steps carefully before you start setting up your device for work.  

## Prerequisites  
You'll need to use your old device for 2-step verification (if using app-based MFA) when setting up the new device. Do not factory reset your old device or remove the Authenticator app before you have successfully set up your new device. 

If you use SMS or call-based MFA, you can use either your old or new device to complete setup. We recommend turning on phone sign-in for the easiest way to authenticate. To set up phone sign-in:
  1. On your existing device, open Microsoft Authenticator.  
  2. Tap your employee email address. 
  3. Tap **Enable phone sign-in**.  

## Before you begin  

If you're migrating from an existing iPhone you use for work to a new device, first complete these steps on your existing device. If you don't need to restore apps and settings from a previous iPhone, continue to [Power on the new device](set-up-migrate-iphone-for-work.md#power-on-the-new-device).       

1. Set up Microsoft Authenticator recovery settings. On your current device, set up a personal Microsoft account as a recovery account in Authenticator.  
    1. Open Microsoft Authenticator.
    2. Go to **Settings** > **iCloud backup**. Turn on iCloud backup. A recovery account is set up.    
    3. Optionally, you can sync your autofill passwords from Authenticator. Scroll to **Autofill** > **Sync account** to adjust autofill settings.  

    > [!NOTE]
    > You'll need to set up your work account on the new device after you restore the backup.    

2. Turn on automatic app downloads in your App Store settings to automatically install all apps from your current device onto your new device. 
    1. On your current device, go to **Settings** > **App Store**. 
    2. Go to **Automatic Downloads** and turn on **Apps**.  

3. Turn on iCloud backup and make sure a recent backup exists. 
   1. On your current device, go to **Settings** and tap your Apple ID > **iCloud** > **iCloud backup**. 
   2. Turn on iCloud Backup. To start a new backup, tap **back up now**. 

4. Check iCloud backup settings. Go to **Settings** > your Apple ID > **iCloud** to confirm that other iCloud backup settings are correct. Check that the apps you want to restore from iCloud are set appropriately. 

Continue to [Power on the new device](set-up-migrate-iphone-for-work.md#power-on-the-new-device).  

## Power on the new device  
Complete these steps on your new device.  

1. Complete the Setup Assistant experience.  
  1. Power on the new phone and select your language. 
  2. When the Quick Start menu appears, bring your old phone close to the new phone and leave it there while you continue setup.  
  3. Choose how you want to transfer your data, or skip.  
   * **Transfer from iCloud**: You'll be automatically signed into iCloud on the new phone and restoration from backup will be initiated. Your apps and data will be downloaded in the background, so you can use the new device right away.  
   * **Transfer from the old phone**: You must wait for the transfer to complete on both devices before you can use the new device.  
  4. After your device restarts and you're on the homepage with your default apps, wait for your apps to automatically install.   
2. Check that the Microsoft Authenticator app is installed before continuing. It may have installed from your apps backup in iCloud. If not, install Microsoft Authenticator from the [App Store](https://apps.apple.com/us/app/microsoft-authenticator/id983156458). 
3. Initiate the onboarding workflow. 
  1. Open a productivity app, such as Microsoft Teams. 
  2. Complete the MFA requirements or passwordless authentication using Authenticator on your old phone. 
  3. You will get blocked by conditional access and prompted to enroll the device. Continue to [Device enrollment](set-up-migrate-iphone-for-work.md#device-enrollment).   

## Device enrollment  

1. Install Company Portal. Open a productivity app, such as Microsoft Teams, and you will be prompted to enroll your device and install the Company Portal app for iOS.  
2. Complete mobile device management (MDM) profile installation. 
  1. Sign into Company Portal.
  2. Tap through setup pages to review privacy information. 
  3. Download the management profile. 
  4. Go to the Settings app to complete profile installation. 
3. Complete a device sync. Return to Company Portal to continue syncing the device and checking for device compliance. 
4. Wait for apps to install. Authenticator is automatically installed or taken over if already installed.  
5. Make the device compliant. Update your device settings as prompted by Company Portal to ensure the device meets your organization's compliance policy requirements.  
6. Re-evaluate compliance. After you address compliance issues, return to Company Portal and tap **Check status** to re-evaluate compliance on your device. Ensure the device is compliant before moving on to the next step.  
7. Get access. You should now have access to work resources on your iPhone. Launch an app you use for work to access work files.  
8. Restore your Authenticator backup. Open Authenticator and tap **Begin recovery** to sign in with your Microsoft account and restore allowed 2-step verification credentials and saved passwords. 
9. Enable *sign in with your phone*. After you restore the backup, you'll see a placeholder for your employee email address in Authenticator. Select the account and tap **Set up 2-step verification** to register this device. Then register and set up MFA to gain access to email. 

## Frequently asked questions 
This section provides answers to frequently asked questions about setting up and enrolling iPhones for work access. 

## How do I migrate from an old iPhone that can't be used for 2-step verification? 
If you are unable to use your old device when setting up your new device, go to ??? to register and set up MFA before you can access email. 

## I use SMS/call for 2-step verification, and Microsoft Authenticator is not set up for 2-step verification. How should I proceed? 
If you use SMS or call-based MFA, as long as the number is active and can receive the SMS/call for verification on any type of device, you can use it for 2-step verification while setting up your new device. However, we recommended that you set up phone sign-in for the easiest setup experience. 
 
## How do I migrate from an old iPhone that has 2-step verification to a new iPhone? 
Do not factory reset the old device or remove the Authenticator app before you have successfully set up your new device. You will need to use your current device for 2-step verification if using app-based MFA when setting up your new device.  

## I am trying to migrate from an Android to an iPhone. How should I proceed? 
If your Android phone is active and is set up for 2-step verification, you can use it to set up work access on your iPhone. You cannot restore an Authenticator app backup across Android and iOS or vice-versa. 

Still need help? Contact your IT support person. Sign into the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) or app to check for your organization's contact information.    
