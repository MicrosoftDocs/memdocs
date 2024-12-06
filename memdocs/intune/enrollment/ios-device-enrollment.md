---
# required metadata

title: Overview of Apple device enrollment in Microsoft Intune  
titleSuffix: Microsoft Intune
description: Utilize Apple device enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/16/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

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

# Overview of Apple device enrollment in Microsoft Intune  
*Apple device enrollment* lets employees and students enroll new and existing personal devices for work or school. It unlocks essential iOS/iPadOS management capabilities for you in the Microsoft Intune admin center, while also protecting the personal data of employees and students. This article provides an overview of the Apple device enrollment features and functionality supported by Microsoft Intune.    

## App or web based enrollment        
Device enrollment supports an app based enrollment experience and web based enrollment experience. In the admin center, your device enrollment options are:   

* **Device enrollment with Company Portal**  
* **Web based device enrollment**   

Create an enrollment profile in the admin center to select and configure enrollment types. Go to **Devices** > **By platform** > **iOS/iPadOS** > **Device onboarding** > **Enrollment** and select **Enrollment types**.  

> [!TIP]
> We recommend enabling web-based enrollment for devices running iOS/iPadOS 15 and later because it doesn't require employees and students to install the Company Portal app. Post-enrollment functionality remains the same as with app-based enrollment. 

Web-based enrollment utilizes just in time (JIT) registration with the Apple single sign-on (SSO) extension to facilitate Microsoft Entra registration within the employee's work apps and reduce the number of times they have to authenticate. To enable JIT registration in enrollments, [create a device configuration profile with an SSO app extension policy](web-based-device-enrollment-ios.md#step-1-set-up-just-in-time-registration). You aren't required to use JIT registration with web-based enrollment but we recommend using it to make the enrollment experience faster and easier for your employees and students. 

The following table provides details about app and web-based enrollment.   

| Specification | App-based enrollment | Web-based enrollment|
| --- | --- | --- | 
| Supported version | iOS/iPadOS 14 and later |iOS/iPadOS 15 and later |
| BYOD and personal devices | ✔️ |✔️ |
| Device associated with single user | ✔️ |✔️|
| Device reset required| ❌|❌|
| Enrollment initiated by device user | ✔️ |✔️|
| Supervision |❌|❌| 
| Just-in-time registration | ✔️ |✔️ |
| Required apps | Intune Company Portal app for iOS <br> Microsoft Authenticator | Microsoft Authenticator |  
| Enrollment location | App-based enrollment takes place in the Company Portal app, Safari, and device settings app. |Web-based enrollment takes place in Safari and the device settings app.| 

 ## Supported settings    
Microsoft Intune supports a subset of device management options for devices enrolled via Apple device enrollment. If a pre-existing configuration profile is applied to a device, only the settings supported by Apple device enrollment take effect. 

<!-- P2 For supported settings in Intune device configurations profiles, see:

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)  
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md) 
   * List others.... -->  

## User experience 
Employees and students can access management options for their personal devices in the Intune Company Portal app or on the Company Portal website. Supported actions include:  

- Rename   
- Remove  
- Remote lock  
- Check status  

>[!NOTE]
> The *rename* action that's available to device users changes the display name in Company Portal. It doesn't rename the device in the Microsoft Intune admin center.  

For more information about how employees and students can access these actions in the web version, see [Using the Intune Company Portal website](../user-help/using-the-intune-company-portal-website.md).  

## Certificates  
This enrollment type supports the Automated Certificate Management Environment (ACME) protocol. When new devices enroll, the management profile from Intune receives an ACME certificate. The ACME protocol provides better protection than the SCEP protocol against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Devices that are already enrolled do not get an ACME certificate on unless they re-enroll into Microsoft Intune. ACME is supported on devices running: 

- iOS 16.0 or later  

- iPadOS 16.1 or later  

## Known issues and limitations 

Intune enrollment with Apple device enrollment has the following known issues and limitations. 

* Due to Apple restrictions, device users going through web based device enrollment must download the management profile in Safari. 

* Just like Company Portal enrollment, once the management profile downloads, users have a limited amount of time to go to the Settings app and install the profile. If they wait too long, they must download the management profile again to continue.  

* Device users may be unable to access work apps if they try signing in on their newly enrolled device while Microsoft Authenticator is still trying to deploy. Users should wait a few minutes while Authenticator catches up with the Intune service, and then try to sign into their work app again.  

* Web-based device enrollment can be used without JIT registration. We recommend using the web version of Company Portal instead of Company Portal for iOS to deploy apps to the device. If you are planning to use the Company Portal app for app deployment, MS Authenticator and the SSO extension policy must be sent to the device post web enrollment. 

* There is a known issue with web-based enrollment and JIT registration that prevents the Company Portal app from recognizing enrolled devices. When a user tries to sign in to Company Portal for iOS on a device that doesn't have the SSO extension policy, Company Portal is unable to determine that the device has been enrolled. We are actively working to resolve this issue. To avoid this issue, we recommend deploying the SSO extension policy to enrolling devices. Or, as a temporary workaround, you can deploy a web clip for the web version of Company Portal, as described under [Best practices for web enrollment](web-based-device-enrollment-ios.md#best-practices).    

## Next steps  

Choose the user enrollment method you want to use to enroll devices, and then create an enrollment profile. For more information about how to enable web-based enrollment in the Microsoft Intune admin center, see [Set up web based enrollment](web-based-device-enrollment-ios.md).     

For more details about Apple device enrollment features and functionality, see [Device Enrollment and MDM]( https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple support website. 

 


