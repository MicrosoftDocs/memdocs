---
# required metadata

title: Back up and restore iOS/iPadOS
titleSuffix: Microsoft Intune
description: Learn about backup and restore scenarios for iOS/iPadOS devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/25/2022
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

You might have to back up and restore an Intune Automated Device Enrollment (ADE) managed iOS/iPadOS device during the setup assistant process. For example, when: 
- A device is factory reset and is then restored from a previous backup. 
- A user receives a new device and wants to migrate the data from the old device. 

To back up and restore an iOS/iPadOS device, you must follow the Apple instructions:

- To back up your device, see [How to back up your iPhone, iPad, and iPod touch](https://support.apple.com/HT203977).
- To restore your device, see [Restore your iPhone, iPad, or iPod touch from a backup](https://support.apple.com/HT204184).
- To transfer data to a new device, see the following Apple support article:
    - [Use iCloud to transfer data from your previous iOS device to your new iPhone, iPad, or iPod touch](https://support.apple.com/HT210217)  
    
For more information about restoring Apple devices from backup, see [Get started using Apple Business Manager or Apple School Manager with Mobile Device Management](https://support.apple.com/HT207516).

> [!NOTE] 
> Device-to-Device migration as offered on the Quick Start screen after resetting an iOS device isn't supported with Apple Business Manager (ABM). For details refer to the following [Apple support document.](https://support.apple.com/HT210216)
> Since this screen appears on the device before a wi-fi connection has been established and before the ABM profile has been downloaded, this quick start screen cannot be hidden via ABM.  

## Back up Microsoft Authenticator      
If you're using the Microsoft Authenticator app, it's also important to back up your credentials and accounts. For more information, visit [Back up and recover account credentials in the Authenticator app](https://support.microsoft.com/account-billing/back-up-and-recover-account-credentials-in-the-authenticator-app-bb939936-7a8d-4e88-bc43-49bc1a700a40#:~:text=The%20Microsoft%20Entra%20Authenticator%20app,or%20having%20to%20recreate%20accounts.).

## Restoring a backup to an iOS/iPadOS device

When a user restores their content from an iCloud or iTunes backup, there are many considerations to bear in mind:
 
- Restoring a backup is only possible during Apple Setup Assistant. This backup is a ‘one-time’ opportunity. Linking the Apple ID in settings post-setup isn't the same as a restore.
While it links files and documents, it doesn't typically restore any user data and preferences (think 'look and feel' such as wallpaper, widgets, installed applications, user preferences, and so on). Only a limited set of data may be restored such as iCloud Photo Library and messages for example.  
- The restore process workflow is different, depending on whether you restore the backup to the same device, or a different device.  
    - When restoring to a different device than the one on which the backup was performed, after the backup is successfully restored, setup assistant will continue with the enrollment process (from the 'remote management' screen onwards). The result is that you are enrolled in the MDM vendor and also maintain your content that has been restored from your iCloud account.  
    - When restoring to the same device on which the backup was performed, after the backup is successfully restored, setup assistant doesn't resume. You're left on the device's home screen. The result is that you don't go through any 'remote management' and subsequent enrollment steps. You retain the management state (and management profile) that you had at the time the backup was done. This result is typically a good thing, unless this process is being performed as part of a migration to a different EMM vendor (see below).  
        - In addition, specific to Intune, there are two different methods to reset a device and they will affect the post-restore behavior regarding enrollment state:  
            - If you performed a local reset of the device, then the device will remain enrolled post-restore and shouldn't require any intervention. This is typically the desired behavior.  
            - If you performed a remote wipe by using the MEM/Intune web portal, this will first unenroll the device before the wipe. As a result, post-restore, the device will need to be re-enrolled using the Company Portal app before it will be functional.  
- Also consider the amount of time that has elapsed since the backup was taken, and what impact a restore (which essentially sets the device back to that prior time), might have. For example, has the corresponding device record in Intune been deleted? (either by accident or an intentional retirement/clean-up). What about the Azure AD record? What about the management certificate? These certificates are valid for a year for iOS/iPadOS. Is the management certificate being restored still valid? Was the management certificate renewed after the backup was done? These scenarios might be less common, but they are worth being aware of – especially if the backup being restored isn't recent.
- To avoid issues, ensure that users do not perform a backup whilst the device is enrolled – you want users to perform any backup/restore activities without impacting the management profile and related certificates. If the management profile was locked on the device by the prior EMM, the end user won't have an option to remove the management profile on the device.  To facilitate this type of migration, one option would be to retire the device from the prior EMM before the user does a backup of the iOS/iPadOS device. Alternatively, if you cannot ensure that the device was unenrolled when the backup was taken, consider hiding the Setup Assistant *restore screen*. The setting that lets you hide the screen can be found in your iOS/iPadOS enrollment profile in the Microsoft Endpoint Manager admin center. For more information, see step 18 in [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).    


## Migrating to MEM/Intune from another EMM vendor

### Specific to backup/restore
 
- In most cases, your MDM enrollment state (at the time of backup) isn't of any special significance. However, in a migration scenario where you are moving from one MDM vendor to another, it is important to be aware of.  
    - When restoring a backup, taken while enrolled in MDM vendor A and restoring it on the same device but attempting to enroll in Intune, this will result in failure. The restore will be successful (no errors) as explained above, however since the management profile from MDM vendor A has been restored, the device isn't under management by Intune. Attempting to manually enroll the device using the Company Portal app will result in an error when trying to install the new Intune management profile "The new MDM payload doesn't match the old payload". To remediate this error, you would need to remove the existing management profile belonging to MDM vendor A and then re-enroll into Intune using Company Portal. Migrating from one Intune tenant to another Intune tenant would exhibit the same behavior.
    - To correctly and fully re-enroll an ADE device, a factory reset is required, and the device cannot be restored from its own backup (otherwise the ADE configuration and profiles in the backup will be applied). 

### Migrating without wiping the device

There is an additional migration scenario to consider, which should not be impacted by any of the above.
- If a migration is performed from one MDM vendor to another without a device wipe (such as by using a tool such as EBF Onboarder for example), there should be no negative impact to the device, as it is never restored. Instead, the device is ‘off-boarded/unenrolled’ from one MDM vendor and has the management profile removed, and then enrolls manually into Intune using the Company Portal app. The users iCloud account isn't removed and no backup is restored as setup assistance isn't involved in this scenario.
- There are other considerations in a scenario where the device is migrated without performing a device wipe:
    - If the device was supervised under the current EMM vendor, the supervised state will be maintained
    - The new management profile (MEM/Intune) cannot be ‘locked’ – meaning the user is able to remove the management profile in Settings.
    - These devices will enroll into MEM/Intune as ‘personal’ devices, rather than ‘corporate’ devices. This condition will have an impact on the app inventory gathered from the device, the displayed phone number, etc., as described [here](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).
        - If you want to designate these migrated devices as corporate devices, following either of these steps:
            - Add Corporate device identifiers as described [here](./device-enrollment-program-enroll-ios.md). Provided you can obtain a list of serial numbers from your current EMM vendor and this list is imported prior to enrolling the devices in Intune, this is the simplest option and avoids scripting.
            - Use a script to modify the OwnershipType from Personal to Corporate. A sample script, which uses an exported list (.csv) of device serial numbers (taken from your current EMM vendor) as input, is located [here](https://github.com/scottbreenmsft/scripts/tree/master/Intune/Devices/SetOwnership).  
            


> [!NOTE] 
> If you use enrollment restrictions to prevent (block) personally owned devices from enrolling, you will need to add the devices using corporate device identifiers, prior to enrollment.

## Next steps

[Learn more about Automated Device Enrollment](device-enrollment-program-enroll-ios.md).
