---
# required metadata

title: Overview of Apple device enrollment in Microsoft Intune  
titleSuffix: Microsoft Intune
description: Utilize Apple device enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/07/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
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

Create an enrollment profile in the admin center to select and configure enrollment types. Go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** and select **Enrollment types**.  

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
| Just-in-time registration | ❌ |✔️ |
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

## Limitations 

* Device users must download the management profile in Safari. When a user gets blocked by conditional access policies, they are given a link that redirects them to device enrollment. The link opens in their default browser. If the default browser is not Safari, the users should copy and paste the link into Safari so that enrollment can continue. 

* After the management profile downloads, device users have a limited amount of time to go to the Settings app and install the profile. If they wait top long to do it, they'll receive a message letting them know that the management profile can't be found. They must select **enroll again** to restart the enrollment process and download the management profile again. 

* Device users may be unable to access work apps if they try signing in on their newly enrolled device while Microsoft Authenticator is still trying to deploy. Users should wait a few minutes while Authenticator catches up with the Intune service, and then try to sign into their work app again.  

* Device users can sign into any of their work or school apps to complete enrollment, except for Microsoft Defender. If they try to sign into Microsoft Defender before any other app, they will be redirected back to Safari for enrollment. 

* Web based device enrollment can be used without JIT registration. However, users in that scenario can't currently use the Company Portal app to enroll. To prepare for this scenario, we recommend deploying a web clip of the Company Portal website to users, because the web clip functions the same as the Company Portal app during enrollment.


## Known issues  

* There's a bug that occurs iOS devices running version 17.0.3. During web based device enrollment, Safari incorrectly reports the device OS version, causing enrollment to fail.
  * Issue: Although web based device enrollment works on devices running major and minor OS versions, we have seen it fail on devices targeted with more granular OS requirements. Specifically, it happens when the OS version in an enrollment restriction contains the build number. For example, enrollment works when an enrollment restriction requires at least iOS 17.0 to enroll. But if you change the restriction to 17.0.3, enrollment may start failing on devices running 17.0.3.  
  * Solution: We are currently working to fix this issue. We recommend the followng workarounds:
    * On the first web enrollment page, tell the device user to switch to mobile view in Safari. Then reload the page.   
    * If the problem persists, tell the device user to clear their cookies in Safari and start enrollment over again.  
    * Use another enrollment type if you want to apply more granular restrictions than the major and minor version numbers.   

## Next steps  

Choose the user enrollment method you want to use to enroll devices, and then create an enrollment profile. For more information about how to enable web-based enrollment in the Microsoft Intune admin center, see [Set up web based enrollment](web-based-device-enrollment-ios.md).     

For more details about Apple device enrollment features and functionality, see [Device Enrollment and MDM]( https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple support website. 

 


