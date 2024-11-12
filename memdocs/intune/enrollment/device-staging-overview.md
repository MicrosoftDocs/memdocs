---
# required metadata

title: Device staging overview   
titleSuffix: Microsoft Intune
description: An overview of device staging, Android Enterprise token types, and token management in Microsoft Intune.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/16/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Device staging overview   

**Applies to Android**  

Enable device staging during enrollment to reduce end user steps for frontline workers and optimize productivity. During device staging, you or a third-party vendor can complete both the admin and end user stages of pre-provisioning. Minimal interaction is required of the user when they receive their device.   

Device staging uses a *staging* token during the enrollment process rather than the *default* token type. Microsoft Intune supports device staging for Android Enterprise devices running Android 8 or later. You can enable device staging in these enrollment profiles:   

* Android Enterprise corporate-owned fully managed  

* Android Enterprise corporate-owned work profile  

This article provides an overview of device staging, token types, and token management in the Microsoft Intune admin center. 

## Token types     

When you create an enrollment profile in the admin center for one of the supported management types, you have to select the token type. Your options include the default token and the staging token. Each type enables a different enrollment experience.  

### Staging token  

The *staging* token enables a staged version of the enrollment flow so that you or a third-party vendor can complete the admin *and* end user steps. This process requires more work from the admin or third party vendor than the end user.

There are three stages during this process:  

-  Stage 1 - Completed by admin 
-  Stage 2 - Completed by admin or third-party vendor 
-  Stage 3 - Completed by end users    

The device is userless in stage 1 and stage 2. It becomes user affiliated during the last stage. End users complete the last stage when they get the device and sign in to the Microsoft Intune app with their work or school account. Devices are ready to use after sign-in.  

In the first stage, an Intune admin completes the following steps:  

1. Create the enrollment profile and staging enrollment token in the admin center. 

1. Set the token's expiration date. 

1. Optionally, in the admin center, create a dynamic device group or an assignment filter so you can assign policies and apps in the user stage. The dynamic device group feature isn't available to configure in the remaining stages. 

In the second stage, an Intune admin or third-party vendor completes the following steps: 
 
1. Unbox, assemble, and power on the new device you're enrolling.      

1. With the device, scan the staging token's QR code or enter the token string.  

1. Complete the enrollment steps and setup wizard. At the end of setup, you are on the device's home screen.  

1. Turn off the device and distribute it to the end user.   

During stage 2, the Intune assignment filter is the only available option for targeting policies and apps. After the final stage ends, you can use other supported targeting options. Example: User security groups and dynamic groups 

In the third, and final stage, an end user completes the following steps: 

1. Power on the device.  

1. Open the Microsoft Intune app, and then sign in with your work or school account.   

1. Complete the remaining enrollment steps. When enrollment is done, the device is ready for use at work or school.   

> [!NOTE]
> Screens that don’t require end user input can be skipped, depending on technical feasibility. An *enrollment in progress* screen takes their place.  

### Default token   

The *default* token enables the standard enrollment flow, with two stages of pre-provisioning: 

-  Stage 1 - Completed by admin 
-  Stage 2 - Completed by end users    

With this token, end users complete most of the pre-provisioning steps. As the admin, you complete a portion of the pre-provisioning steps before you distribute the devices to your workforce. Device users complete the remaining steps when they sign in with their work or school account. 

In the first stage, an Intune admin completes the following steps:  

1. Create an enrollment profile with the default enrollment token.
   
1. With the new device, scan the QR code, and then follow the on-screen prompts to configure the device. 

1. For a device enrolling with a newly created enrollment token, create a dynamic device group or an assignment filter to assign policies and apps in the user stage.  

1. Distribute the device to the end user.   

In the second, and final stage, an end user completes the following steps: 

1. Unbox the device and connect to Wi-Fi.
   
1. Sign in to work or school account, and then follow the on-screen prompts.
   
1. Complete the pre-provisioning steps. If they're going through work profile enrollment, for example, they create and install the work profile.
   
1. Grant app permissions or accept terms wherever required. 

For detailed steps, see:  

- [Set up enrollment for Android Enterprise fully managed devices](android-fully-managed-enroll.md)  
- 
- [Set up enrollment for corporate-owned work profile devices](android-corporate-owned-work-profile-enroll.md)      

## Replace, remove, or export token  
Select your token in the admin center to access token management options:   

- **Replace token**: Generate a new token that's nearing expiration. 

- **Revoke token**: Immediately expire the token. After you revoke it, the token is no longer usable. This option is useful if you: 

  - Accidentally share the token with an unauthorized party. 

  - Complete all enrollments and no longer need the token. 

- **Export token**: Export the JSON content of the token. You can use this option to get the JSON content required for Google Zero Touch or Knox Mobile Enrollment configuration.  

When applied, these actions don't have any effect on devices that are already enrolled.   

## Reporting   

To view all devices with a staging token, go to **Devices** > **All devices**. 

Devices set up via staging remain in stage 2 until the end user signs in with their work or school account. These devices appear in the report with a *staging* prefix.   

* Naming convention: *Staging_serialnumber_enrollmentmode_MM/DD/YY_H.MM*  
* Example: *Staging_ XX1234_AnroidEnterprise_06/22/2024_ 4.20 AM*   

After end users complete enrollment, the *username* replaces the *staging* prefix in the report. 

* Naming convention: *Username_enrollmentmode_MM/DD/YY_H.MM*  
* Example: *john@contoso.com_ AnroidEnterprise_06/22/2024_ 4.20 AM*   

