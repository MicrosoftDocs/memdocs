---
# required metadata

title: Intune actions and options supported with Apple User Enrollment
titleSuffix: Microsoft Intune
description: Learn which Intune actions and options are supported with Apple User Enrollment
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/24/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: amhaq
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Overview of Apple User Enrollment in Microsoft Intune 

> [!IMPORTANT]
> The account driven user enrollment feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

You can utilize Apple User Enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune. *Apple User Enrollment* is an enrollment solution specifically for bring-your-own-device (BYOD) scenarios. It sets up the personal device so that work data is stored on a separate volume and in managed apps, away from the user's personal data and apps. Supervised mode isn't available with this enrollment type. As the admin, you get access to a limited but appropriate subset of Intune management options and restrictions to ensure that your organization's data stays safe.  

This article provides an overview of the Apple User Enrollment features and functionality supported by Microsoft Intune. 

## User enrollment options  
Microsoft Intune supports account driven Apple User Enrollment and Apple User Enrollment with Company Portal.   

* Account driven user enrollment: Also referred to as *account-based enrollment*. The device user initiates enrollment by going to the **Settings** app > **VPN & Device Management** and adding their work or school account. After the device user approves device management, the enrollment profile silently installs, and Intune policies are applied.      
* User enrollment with Company Portal: Also referred to as *profile based enrollment*. The device user initiates enrollment by signing into the Intune Company Portal app and following a series of screens and prompts. They are redirected from the app to Safari to download a preconfigured enrollment profile, and then go to the **Settings** app to install the profile.   

The following table provides a side-by-side comparison of each method.   

| Feature or scenario | Account driven user enrollment | User enrollment with Company Portal|
| --- | --- | --- | 
| Just-in-time registration | ✔️ |❌ |
| BYOD and personal devices | ✔️ |✔️ |
| Devices associated with single user | ✔️ |✔️| 
| Enrollment initiated by device user | ✔️ |✔️|
| Enrollment location | User is prompted to enroll device when they sign into an app with their work account. Enrollment takes place within a single screen in the device settings app. |User is prompted to enroll device when they sign into an app with their work account. Enrollment takes place over a series of screens in the Company Portal app, Safari web browser, and device settings app.|
| Supervision|❌|❌| 
| BYOD and personal devices | ✔️ |✔️ |
| BYOD and personal devices | ✔️ |✔️ |
| Version | iOS/iPadOS 15 or later |iOS 13 or later <br/><br/> iPadOS 13.1 or later |
| Required apps | Microsoft Authenticator |Intune Company Portal app for iOS <br> </br> Microsoft Authenticator |  

## Supported settings 

Microsoft Intune supports a specific subset of device management options for user enrollment. If a pre-existing configuration profile is applied to a device set up via user enrollment, only the settings supported by user enrollment take effect. This section describes the supported settings.  

### Password settings   

If you configure any password settings, Microsoft Intune automatically sets the **Simple passwords** setting to **Block**. Microsoft Intune also enforces a six-digit device PIN.  

For example:  
1. You create an enrollment profile for user enrollment with Company Portal. 
2. Within the profile you you configure **Password expiration**.  
2. You assign the enrollment profile.  
3. Microsoft Intune applies the password settings in the following ways:    
  - The **Password expiration** setting is ignored.  
  - Simple passwords such as `111111` or `123456` are prohibited.  
  - A six-digit pin is enforced.  

### Remote actions for Intune admins    
You can apply these Microsoft Intune remote actions, which are available in the admin center, to devices enrolled via Apple User Enrollment:    
- Retire  
- Delete  
- Remote Lock  
- Sync  

### App deployment options  
You can deploy these app types to devices enrolled via User Enrollment:  
- User-licensed apps and custom apps purchased through an Apple Volume Purchase Program (VPP) 
- Line-of-business (LOB) apps  
- Web apps  

### Supported actions for device users 
Employees and students can access management options for their personal devices in the Intune Company Portal app or on the Company Portal website. Supported actions include:  
- Rename   
- Remove  
- Remote lock  
- Check status  

>[!NOTE]
> The *rename* action that's available to device users changes the display name in Company Portal. It doesn't rename the device in the Microsoft Intune admin center.  

## Other supported options

The following options are supported in Intune for devices enrolled by using Apple User enrollment:
- Per-App VPN. This support excludes Safari Domains as User Enrollment doesn't support configuring Safari settings.
- WiFi 
- Corporate app removal upon unenrollment
- Jailbreak Detection

The following restrictions are supported:
- View corporate documents in unmanaged apps
- Viewing noncorporate documents in corporate apps
- Allow unmanaged apps to read from managed contacts accounts
- AirDrop as an unmanaged destination
- Required encrypted backup
- Managed apps sync to cloud
- Control Center access while device locked
- Notification Center access while device locked
- Today view while device locked
- Block screenshots
- Block Enterprise Book backup
- Block Enterprise Book metadata sync
- Require encrypted backup
- Require watch wrist detection
- Block Siri
- Block Siri while device is locked
- Require Safari fraud warnings
- Block diagnostics submission to Apple  

## Options not supported
The following device management options aren't supported on devices enrolled via Apple User Enrollment. If you need these options, we recommend using Apple Device Enrollment for BYOD scenarios or Apple Automated Device Enrollment for corporate-owned devices.
- Collect app inventory for apps outside of the managed APFS volume.
- Collect inventory of certificates and provisioning profiles outside of the managed APFS volume.
- Collect UDID and other persistent device identifiers, such as phone number, serial number, and IMEI
- User Enrollment supports a unique enrollment ID for each device enrolled, but this ID doesn't persist after unenrollment. 
- SCEP User profiles with Subject Name Format of Serial Number.
- Device-level VPN.
- Device-licensed VPP app deployment.
- Install App Store apps as managed apps.
- MDM control of applications outside of the managed APFS volume.
  - App protection policies still apply to these apps. However, you can't take over management or deploy a managed version of these apps unless the user deletes them from their device.
- Actions, configurations, settings, and commands requiring supervision. 
- Customized privacy text in the Company Portal. If you customize the text explaining what your organization can and can't see, then users will see the same text for User and Device Enrollment in the Company Portal. 
- Devices running iOS 15.5 can't enroll with User Enrollment if MFA text or call is needed on the same device during enrollment. 
- Devices running iOS 15.7 through iOS 16.3 can't enroll with User Enrollment with MFA text. MFA call must be used in order to enroll with User Enrollment if MFA is needed on the same device during enrollment. 
- Application reporting for app types unsupported with User Enrollment. 


## Next steps  

After considering supported settings and enrollment features, choose the user enrollment method you want to use to enroll devices. The following articles describe how to set up these enrollment methods in the Microsoft Intune admin center:    

* [Set up user enrollment with Company Portal](apple-user-enrollment-with-company-portal.md)   
* [Set up account driven user enrollment](apple-account-driven-user-enrollment.md)   

For more information about Apple User Enrollment features and functionality, see [User Enrollment and MDM](https://support.apple.com/guide/deployment/dep23db2037d/web) on the Apple support website.  


