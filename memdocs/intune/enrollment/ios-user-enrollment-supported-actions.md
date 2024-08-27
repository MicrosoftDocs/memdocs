---
# required metadata

title: Overview of Apple User Enrollment in Microsoft Intune
titleSuffix: Microsoft Intune
description: Utilize Apple User Enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/19/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rishitasarin
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Overview of Apple User Enrollment in Microsoft Intune  
You can utilize Apple User Enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune. *Apple User Enrollment* is an enrollment solution specifically for bring-your-own-device (BYOD) scenarios. It sets up the personal device so that work data is stored on a separate volume and in managed apps, away from the user's personal data and apps. Supervised mode isn't available with this enrollment type. As the admin, you get access to a limited but appropriate subset of Intune management options and restrictions to ensure that your organization's data stays safe.  

This article provides an overview of the Apple User Enrollment features and functionality supported by Microsoft Intune. 

## Apple User Enrollment methods  

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
| Version | iOS/iPadOS 15 or later |iOS 13 or later <br/><br/> iPadOS 13.1 or later |
| Required apps | Microsoft Authenticator |Intune Company Portal app for iOS <br> </br> Microsoft Authenticator |  

## Supported settings 

Microsoft Intune supports a specific subset of device management options for devices enrolled via Apple User Enrollment. If a pre-existing configuration profile is applied to a device, only the settings supported by Apple User Enrollment take effect. This section lists the supported configurations and policies, and also includes limitations and nonsupported capabilities. This list is not exhaustive and will continue to be updated.   

### Device configuration and management 
Supported device configuration policies and management capabilities include: 

- VPN: User enrollment is limited to per-app VPN. For more information, see [Set up per-app Virtual Private Network (VPN) for iOS/iPadOS devices in Intune](../configuration/vpn-setting-configure-per-app.md). Safari domains are not supported. 
- Wi-Fi: For more information, see [Add Wi-Fi settings for iOS and iPadOS devices in Microsoft Intune](../configuration/wi-fi-settings-ios.md).
- Device restrictions: For a list of supported device restrictions, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md). 
- Remote actions for admins: You can retire, delete, remote lock, and sync devices. For more information about these actions and how they work, see [Manage devices with Microsoft Intune](../remote-actions/device-management.md).  

### App deployment and management    
Supported app types include:   
- User-licensed apps and custom apps purchased through an Apple Volume Purchase Program (VPP) 
- Line-of-business (LOB) apps  
- Web apps  

### Company Portal actions   
Employees and students can access management options for their personal devices in the Intune Company Portal app or on the Company Portal website. Supported actions include:  
- Rename   
- Remove  
- Remote lock  
- Check status  

>[!NOTE]
> The *rename* action that's available to device users changes the display name in Company Portal. It doesn't rename the device in the Microsoft Intune admin center.  

For more information about how employees and students can access these actions, see:

* [Using the Intune Company Portal website](../user-help/using-the-intune-company-portal-website.md) 
* [Check status, or sync device, in Company Portal app](../user-help/sync-your-device-manually-ios.md)
* [Reset device in Company Portal app](../user-help/effects-of-device-reset-company-portal-ios.md)  
* [Remove or unenroll device in Company Portal app](../user-help/unenroll-your-device-from-intune-ios.md)

### Limitations and capabilities not supported    

When using Apple User Enrollment to enroll devices, Intune doesn't collect:  
  - App inventory for apps outside of the managed Apple File System volume.  
  - Certificate and provisioning profile inventory outside of the managed APFS volume.  
  - UDID and other persistent device identifiers, such as phone number, serial number, and IMEI.  

Intune doesn't support:  
  - SCEP user profiles with Subject Name Format of Serial Number.  
  - Installation of Apple App Store apps as managed apps.  
  - MDM control of apps outside of the managed APFS volume. App protection policies still apply to these apps. However, you can't take over management or deploy a managed version of these apps unless the user deletes them from their device.  
  - Custom privacy text in the Company Portal that's exclusively for user enrollment workflows. If you customize the text explaining what your organization can and can't see, users see the same text in the Company Portal during both Apple Device Enrollment and Apple User Enrollment. 
  - Reporting for app types that aren't supported.   

Limitations include: 
- User enrollment supports a unique enrollment ID for each device enrolled, but this ID doesn't persist after the user unenrolls the device.  
- Devices running iOS version 15.5 can't enroll with Apple User Enrollment if a mutli-factor authentication text or call is needed on the same device during enrollment.  
- Devices running iOS versions 15.7 through iOS 16.3 can't enroll with Apple User Enrollment while utilizing multi-factor authentication (MFA) via text. The phone call option must be used to enroll if MFA is needed on the same device during enrollment.  

If these capabilities are important to you, we recommend using Apple Device Enrollment for BYOD scenarios or Apple Automated Device Enrollment for corporate-owned devices.  

## Next steps  

After considering supported settings and enrollment features, choose the user enrollment method you want to use to enroll devices. The following articles describe how to set up these enrollment methods in the Microsoft Intune admin center:    

* [Set up user enrollment with Company Portal](apple-user-enrollment-with-company-portal.md)   
* [Set up account driven user enrollment](apple-account-driven-user-enrollment.md)   

For more information about Apple User Enrollment, see [User Enrollment and MDM](https://support.apple.com/guide/deployment/dep23db2037d/web) on the Apple support website.  
