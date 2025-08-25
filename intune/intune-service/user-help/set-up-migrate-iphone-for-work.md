---
# required metadata

title: Migrate to a new iPhone for work | Microsoft Intune
titlesuffix: Microsoft Intune
description: Learn how to transfer your work access from an old iPhone to a new iPhone. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/06/2023
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
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

# Migrate to a new iPhone for work   

Transfer work account credentials, apps, and settings from the old iPhone you used for work, to your new one. This article describes how to:     

* Set up and enroll your new iPhone for work. 
* Transfer data from your old iPhone to your new one. 

Review all steps carefully before you start setting up your new iPhone.   

## Prerequisites  
> [!CAUTION]
> If you're using app-based multifactor authentication (MFA), you'll need to use your old device to complete MFA when setting up your new device. Don't factory reset your old device or remove the Microsoft Authenticator app until you have successfully set up your new device. If you use SMS or call-based MFA, you can use either your old or new device to complete setup. 

Your old phone must already have access to protected work resources and be set up for multifactor authentication (MFA). To create a backup of your data, you need:
* A [personal Microsoft account](https://account.microsoft.com/account) to act as your recovery account.
* An [iCloud account](https://www.icloud.com/) for the actual storage location. 

We recommend turning on *phone sign-in* for the easiest way to authenticate. To set up phone sign-in:  
  1. On your old device, open Microsoft Authenticator.  
  2. Tap your employee email address. 
  3. Tap **Enable phone sign-in**.  

## Step 1: Before you begin  

If you're migrating from an old iPhone you used for work to a new iPhone, first complete these steps on your old iPhone. If you don't want to restore work account credentials, apps, and settings from a previous iPhone, continue to [Step 2: Power on the new device](set-up-migrate-iphone-for-work.md#step-2-power-on-the-new-device).       

1. Set up Microsoft Authenticator recovery settings. On your old device, set up a recovery account for your work account credentials:    
    1. Open Microsoft Authenticator.
    2. Go to **Settings** and turn on **iCloud backup**. Your account credentials are backed up to your iCloud account and your **Recovery Account** is created.       
    3. Optionally, you can sync your autofill passwords from Authenticator. Scroll to **Autofill** > **Sync account** to set up the password sync.  

    > [!NOTE]
    > You'll need to sign in and set up your work account on the new device after you go through device enrollment and restore the backup.    

2. Turn on automatic app downloads in your App Store settings to automatically install all apps from your old device onto your new device:   
    1. On your old device, go to **Settings** > **App Store**. 
    2. Go to **Automatic Downloads** and turn on **Apps**.  

3. Turn on iCloud backup and make sure a recent backup exists:  
   1. On your old device, go to **Settings** and tap your Apple ID > **iCloud** > **iCloud Backup**. 
   2. Turn on iCloud Backup. To start a new backup, tap **Back Up Now**. 

4. Check iCloud backup settings:
   1. Go back to **iCloud** to confirm that your other iCloud backup settings are correct.  
   2. Check that the apps you want to restore from iCloud are set appropriately.       

## Step 2: Power on the new device  
Set up your new iPhone. Complete these steps on your new iPhone unless otherwise indicated.   

1. Complete the Setup Assistant experience:    
    1. Power on the new phone and select your language. 
    2. When the Quick Start menu appears, place your old phone close to the new phone and leave it there while you continue setup.  
    3. Choose how you want to transfer your data. Skip this step if you're not transferring anything.  
      * **Transfer from iCloud**: You're automatically signed into iCloud on the new phone and restoration from backup begins. Your apps and data download in the background, so you can use the new device right away.  
      * **Transfer from the old phone**: You must wait for the transfer to complete on both devices before you can use the new device.  
2. After your device restarts and you're on the homepage (where your default apps appear), wait while your transferred apps automatically install.   
3. Check that the Microsoft Authenticator app is installed before continuing. It could have installed from your iCloud apps backup. If you don't have the app, install Microsoft Authenticator from the [App Store](https://apps.apple.com/us/app/microsoft-authenticator/id983156458).  
4. Initiate the device enrollment workflow:   
    1. On your new device, open a productivity app, such as Microsoft Teams, and sign in with your work account.  
    2. Complete the MFA requirements or passwordless authentication using Authenticator on your old phone. 
    3. You'll get blocked by Conditional Access and prompted to enroll your new device.     

## Step 3: Device enrollment  
When you open a productivity app, such as Microsoft Teams, and sign in with your work account, you'll be prompted to install the Company Portal app for iOS and enroll your device. Complete these steps to finish setting up your device for work.   

1. Install [Intune Company Portal](https://apps.apple.com/us/app/intune-company-portal/id719171358) on your new iPhone.   
2. Complete mobile device management (MDM) profile installation. 
   1. Sign into Company Portal with your work account. 
   2. Tap through the setup pages to review privacy information. 
   3. Download the management profile. 
   4. Go to the Settings app to complete profile installation. 
3. Complete a device sync. Return to the Company Portal app and wait while Company Portal syncs the device and checks for device compliance. 
4. Wait for your work apps to install. Authenticator will install if it's not already installed on your device by now.  
5. Make the iPhone compliant. Update your device settings as prompted by Company Portal to ensure the iPhone meets your organization's device compliance policy requirements.  
6. Re-evaluate compliance. After you resolve device compliance issues, return to Company Portal and tap **Check status** to re-evaluate compliance. Ensure the device is compliant before moving on to the next step.  
7. Get access. You should now have access to work resources on your iPhone. Open an app you use for work and sign in with your work account to access work files.  
8. Restore your Authenticator backup. Open Authenticator and tap **Begin recovery** to sign in with your personal Microsoft account and restore allowed MFA credentials and saved passwords. 
9. Enable *phone sign-in*. After you restore the backup, you'll see a placeholder for your employee email address in Authenticator. Select the account and tap **Set up 2-step verification** to register this device. Then register and set up MFA to gain access to email. 

## Frequently asked questions 
This section provides answers to frequently asked questions about setting up and migrating iPhones for work access. 

### General  

#### How do I migrate from an old iPhone that can't be used for MFA? 
If you're unable to use your old device to set up your new device, then you must register and set up multifactor authentication (MFA) on your new device before you can access email. 

#### What happens if I use SMS/call for MFA and Microsoft Authenticator isn't set up for MFA?  
If you use SMS or call-based MFA, as long as the number is active and can receive the SMS/call for verification on any type of device, you can use it for two-step verification while setting up your new device. However, we recommended that you set up *phone sign-in* for the easiest setup experience. 
 
#### How do I migrate from an old iPhone that has two-step verification set up to a new iPhone? 
Don't factory reset the old iPhone or remove the Authenticator app until you have successfully set up your new iPhone. You'll need to use your old iPhone for two-step verification (if using app-based MFA) when setting up your new device. Follow the steps in this article from beginning to end to set up your new iPhone.  

### Android

#### Can I migrate from an Android to an iPhone using these steps?  
If your Android phone is active and is set up for two-step verification, you can use it to set up work access on your iPhone. You can't restore an Authenticator app backup from Android to iOS and vice-versa. 

Still need help? Contact your IT support person. Sign into the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) or app to check for your organization's contact information.    
