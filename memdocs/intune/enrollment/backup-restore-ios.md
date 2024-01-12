---
# required metadata

title: Back up and restore iOS/iPadOS
titleSuffix: Microsoft Intune
description: Learn about backup and restore scenarios for iOS/iPadOS devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/12/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Backup and restore scenarios for iOS/iPadOS  
*Applies to iOS/iPadOS*  

This article describes the backup and restore scenarios for Intune-managed iOS/iPadOS devices, and includes best practices for how to maintain the device's enrollment status when, for example:  

- A device is factory reset and needs to be restored from a previous backup. 
- A user receives a new device and wants to migrate the data from the old device.
- A device is migrating to Intune from another EMM vendor.  

The backup and restore scenarios are specific to enrollments via Apple Automated Device Enrollment. For information about how to back up, restore, and transfer data for an Apple device, see the following Apple Support documentation:  

- [How to back up your iPhone, iPad, and iPod touch](https://support.apple.com/HT203977).
- [Restore your iPhone, iPad, or iPod touch from a backup](https://support.apple.com/HT204184).
- [Use iCloud to transfer data from your previous iOS device to your new iPhone, iPad, or iPod touch](https://support.apple.com/HT210217)  

> [!NOTE] 
> Device-to-device migration, a data transfer option that appears on the Quick Start screen after resetting an iOS device, isn't supported on devices enrolled via Apple Business Manager. For more information about Quick Start, see [Use Quick Start to transfer data to a new iPhone or iPad](https://support.apple.com/HT210216).  
> Quick Start occurs before a Wi-fi connection is established on the device and before the Apple Business Managed profile downloads. As a result, the Quick Start screen can't be hidden via Apple Business Manager.  

## Back up Microsoft Authenticator      
If you're using the Microsoft Authenticator app, it's also important to back up your credentials and accounts. For more information, see [Back up and recover account credentials in the Authenticator app](https://support.microsoft.com/account-billing/back-up-and-recover-account-credentials-in-the-authenticator-app-bb939936-7a8d-4e88-bc43-49bc1a700a40#:~:text=The%20Microsoft%20Entra%20Authenticator%20app,or%20having%20to%20recreate%20accounts.).  

## Restoring a backup to an iOS/iPadOS device  

Restoring a backup is only possible during Apple Setup Assistant. This backup is a one-time opportunity. Consider the information in this section to help you prepare and support device users restoring their content from an iCloud or iTunes backup.  

>[!NOTE]
> Linking an Apple ID in device settings post-setup isn't the same as restoring a backup. While linking the Apple ID does link files and documents, it doesn't typically restore any user data and preferences such as wallpaper, widgets, installed apps, and user preferences. Only a limited set of data, such as iCloud Photo Library and messages, can be restored.

### Restore options and workflow  
The workflow for the restore process is different depending on where you restore the backup. Your options are:      

    - Restore backup on different device than the one on which the backup was performed: After the backup is successfully restored, Setup Assistant continues with the enrollment process starting on the **Remote management** screen. The result is that you enroll in the MDM vendor and maintain the content that's restored from your iCloud account.  
    - Restore backup on same device the backup was performed: After the backup is successfully restored, Setup Assistant ends and you land on the device's home screen. The result is that you don't go through the subsequent enrollment steps. Your device keeps the management state and management profile that you had at the time the backup was done. This result is typically the desired outcome, unless this process is being performed as part of a [migration to a different EMM vendor](#migrating-to-intune-from-another-emm-vendor).  

### Reset options  
There are two ways to reset a managed iOS/iPadOS device. Each reset method has a different effect on the device's enrollment state post-restoration:      
* If you perform a local reset of the device, the device enrolls after you restore the backup, and shouldn't require any intervention. This behavior is typically the desired outcome.  
* If you perform a remote wipe in the Intune admin center, the device unenrolls from Intune before it's wiped. After you restore the backup, the device will need to be re-enrolled in the Company Portal app.

### Timing of backup      
Consider the amount of time that has elapsed since the backup was taken, and how the device would be impacted if restored to the last backup. Although this scenario might be less common, we recommend being aware of when the backup was created and considering questions like:  
* Has the corresponding device record in Intune been deleted, either by accident or intentionally for retirement or clean-up?
* Has the Microsoft Entra ID record been deleted?
* Has the management certificate been deleted? These certificates are valid for a year for iOS/iPadOS and need to be renewed annually.    
* Is the management certificate being restored still valid? Was the management certificate renewed after the backup was done? These scenarios might be less common, but they are worth being aware of – especially if the backup being restored isn't recent.  
  
To avoid conflicts and issues, user's shouldn't create a backup while the device is enrolled in device management. Doing so can impact the management profile and related certificates. 

If the prior EMM vendor locked the management profile on the device, the device user can't remove the management profile. To facilitate a migration in this scenario, you can: 
* Retire the device from the prior EMM before the user backs up the device.  
* Alternatively, if you can't ensure that the device was unenrolled when the backup was created, consider hiding the Setup Assistant *restore* screen. The setting that lets you hide the screen can be found in the Microsoft Intune admin center in your iOS/iPadOS enrollment profile. For more information, see step 18 in [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).  

## Migrating to Intune from another EMM vendor  
Typically the MDM enrollment state at the time of backup isn't of any special significance. However, in a migration scenario where you're moving from one MDM vendor to another, it's important to be aware of the device's MDM enrollment state so that it doesn't carry over its old management profile. 

### Example  

The following steps outline the sequence of events that lead to enrollment failing:    
1. User creates a backup while enrolled in MDM vendor A. 
2. User restores backup on same device. The backup is restored successfully with no errors indicated.
3. User attempts to manually enroll device via Intune Company Portal app. However, the backup restored the management profile from MDM vendor A, so the user's device can't enroll in Intune.

Company Portal app notifies the user of this conflict by explaining that *the new MDM payload doesn't match the old payload*. To remediate this error, the device user must remove the management profile belonging to MDM vendor A, and then re-enroll into Intune using Company Portal. You can expect the same behavior and outcome when migrating from one Intune tenant to another Intune tenant.     - 

### Migrating without wiping the device

There is a way to migrate devices to another MDM vendor without wiping the device. If a migration is performed from one MDM vendor to another without a device wipe, via a tool such as EBF OnBoarder, there should be no negative impact to the device, as it's never restored. Instead, this route unenrolls and removes the device from the previous MDM vendor. Then it removes the management profile from the device. After the management profile is removed, the device user can manually enroll the device into Intune via the Company Portal app. The user's iCloud account remains connected and no backup is restored, as Setup Assistance isn't involved in this scenario.  

Other details to consider when migrating a device without performing a device wipe:  
* If the device was supervised under the current EMM vendor, it remains supervised.  
* The Apple Activation Lock bypass code is only generated when the device is erased, so Activation Lock can't be managed on these devices once they migrate MDM vendors. 
* The new Intune management profile can't be *locked*, meaning the user must be able to remove the management profile via device settings.  
* These devices enroll into Intune as personal devices, rather than corporate-owned devices. This identification enables Intune to gather more details about app inventory and device information such as phone number. For more information that you can share with end users about what's visible on enrolled devices, see [What can my organization see on my enrolled device?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).  
* If you want to designate devices as corporate devices, you have two options:  
    * [Add corporate device identifiers](corporate-identifiers-add.md). This option requires the least amount of effort and avoids scripting, provided you can obtain a list of serial numbers from your current EMM vendor. The list must be imported prior to enrolling the devices in Intune.  
    * Use a script to modify the `OwnershipType` from *personal* to *corporate-owned*. For a sample script that uses an exported list (.csv) of device serial numbers as input, see [Set ownership](https://github.com/scottbreenmsft/scripts/tree/master/Intune/Devices/SetOwnership).  

> [!NOTE] 
> If you use enrollment restrictions to block personally owned devices from enrolling in Intune, you will need to add the devices using corporate device identifiers prior to enrollment.  

## Next steps

[Learn more about using Microsoft Intune and Apple Automated Device Enrollment](device-enrollment-program-enroll-ios.md).  
