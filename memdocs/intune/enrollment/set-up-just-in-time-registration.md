---
# required metadata

title: Set up just in time registration   
titleSuffix: Microsoft Intune
description: Set up just in time registration in Intune for devices enrolling via a supported Apple device enrollment or user enrollment method.   
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/23/2023
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

# Enable just in time registration in Microsoft Intune    
**Applies to iOS/iPadOS**  

Set up *just in time (JIT) registration* in Microsoft Intune to enable device users to initiate and complete device enrollment from a work or school app. The Intune Company Portal isn't required when using JIT registration. Instead, JIT registration utilizes the Apple single sign-on (SSO) extension to complete Entra ID registration and compliance checks. Registration and compliance checks can be fully integrated in a designated Microsoft or non-Microsoft app that's configured with the Apple single sign-on (SSO) app extension.  The extension reduces authentication prompts during the device user's session and establishes SSO across the whole device. 

This article describes how to enable just-in-time (JIT) registration by creating an SSO app extension policy in the Microsoft Intune admin center.      

## Prerequisites  
JIT registration is supported with the following enrollment types: 

* Apple user enrollment: Account driven user enrollment 
* Apple device enrollment: Web-based device enrollment  
* Apple automated device enrollment: For enrollments that use Setup Assistant with modern authentication as the [authentication method](automated-device-enrollment-authentication.md).  

## Best practices for SSO configuration
* The user's first sign-in after they reach the home screen has to happen in a work or school app that's configured with the SSO extension. Otherwise, Azure AD registration and compliance checks can't be completed. We recommend pointing employees to the Microsoft Teams app, because it's integrated with the latest identity libraries and will provide the most streamlined experience from the user's home screen.

* The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add the bundle IDs for your Microsoft apps to your policy. You only need to add non-Microsoft apps.  

* Don't add the bundle ID for the Microsoft Authenticator app to your SSO extension policy. Since it's a Microsoft app, the SSO extension will automatically work with it.  

## Setup JIT registration     
Create a single sign-on app extension policy to enable just-in-time (JIT) registration.  
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. [Create an iOS/iPadOS device configuration policy](../configuration/device-features-configure.md) under **Device features** > **Category** > [**Single sign-on app extension**](../configuration/device-features-configure.md#single-sign-on-app-extension).  
3. For **SSO app extension type**, select **Microsoft Entra ID**.  
4. Add the [app bundle IDs](../configuration/bundle-ids-built-in-ios-apps.md) for any non-Microsoft apps using single sign-on (SSO). The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add Microsoft apps to your policy. 

   Don't add the Microsoft Authenticator app to the SSO extension either.  That app is added later in an app policy.     
5. Under **Additional configuration**, add the required key-value pair. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.   
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}}
6. (Recommended) Add the key-value pair that enables SSO in the Safari browser for all apps in the policy. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.    
    * **Key**: browser_sso_interaction_enabled
    * **Type**: Integer
    * **Value**: 1
7. Select **Next**.  
8. For **Assignments**, assign the profile to all users, or select specific groups. 
9. Select **Next**.  
10. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile. 
11. Go to **Apps** > **All apps** and assign Microsoft Authenticator to groups as a required app. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md) and [Assign apps to groups](../apps/apps-deploy.md).  

## Next steps   
Create an enrollment profile for enrolling devices. The enrollment profile triggers the device user's enrollment experience, and enables them to initiate enrollment. For information about how to create a profile for supported enrollment types, see the following resources:  

* [Account driven user enrollment](apple-account-driven-user-enrollment.md)
* [Apple automated device enrollment for Setup Assistant with modern authentication](device-enrollment-program-enroll-ios#create-an-apple-enrollment-profile) 
* [Web based device enrollment](web-based-device-enrollment-ios.md)  


