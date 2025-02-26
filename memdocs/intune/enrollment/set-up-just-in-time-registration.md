---
# required metadata

title: Set up just-in-time registration   
titleSuffix: Microsoft Intune
description: Set up JIT registration in Intune for devices enrolling via a supported Apple device enrollment or user enrollment method.   
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/22/2024
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

# Set up just-in-time registration in Microsoft Intune    
**Applies to iOS/iPadOS**  

Set up *just-in-time (JIT) registration* in Microsoft Intune to enable device users to initiate and complete device enrollment from a work or school app. The Intune Company Portal isn't required when using JIT registration. Instead, JIT registration utilizes the Apple single sign-on (SSO) extension to complete Microsoft Entra registration and compliance checks. Registration and compliance checks can be fully integrated in a designated Microsoft or non-Microsoft app that's configured with the Apple single sign-on (SSO) app extension.  The extension reduces authentication prompts during the device user's session and establishes SSO across the whole device.  

JIT compliance remediation, the feature that initiates compliance checks, is enabled automatically on devices utilizing JIT registration and targeted with compliance policies. Compliance remediation happens in an embedded flow within the app users are registering. They can see their compliance status and take actionable steps to remediate the issues as they complete JIT registration. If their device is noncompliant, for example, the Company Portal website opens in the app and shows them the reason for noncompliance.  

This article describes how to enable JIT registration by creating an SSO app extension policy in the Microsoft Intune admin center.  

## Prerequisites  
Microsoft Intune supports JIT registration and compliance remediation for all iOS and iPadOS enrollments, including: 

* Apple User Enrollment: Account-driven user enrollment and user enrollment with Company Portal  
* Apple Device Enrollment: Web-based device enrollment and device enrollment with Company Portal  
* Apple automated device enrollment: For enrollments that use Setup Assistant with modern authentication as the [authentication method](automated-device-enrollment-authentication.md)  

To take advantage of JIT compliance remediation, you must assign compliance policies to devices.  

## Best practices for SSO configuration  
* The user's first sign-in after they reach the home screen has to happen in a work or school app that's configured with the SSO extension. Otherwise, Microsoft Entra registration and compliance checks can't be completed. We recommend that you point employees to the Microsoft Teams app. The app is integrated with the latest identity libraries and provides the most streamlined experience from the user's home screen.  

* The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add the bundle IDs for your Microsoft apps to your policy. You only need to add non-Microsoft apps.  

* Don't add the bundle ID for the Microsoft Authenticator app to your SSO extension policy. Since it's a Microsoft app, the SSO extension will automatically work with it.  

## Set up JIT registration     
Create a single sign-on app extension policy that uses the Apple SSO extension to enable just-in-time (JIT) registration.  
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. [Create an iOS/iPadOS device configuration policy](../configuration/device-features-configure.md) under **Device features** > **Category** > [**Single sign-on app extension**](../configuration/device-features-configure.md#single-sign-on-sso).  
3. For **SSO app extension type**, select **Microsoft Entra ID**.  
4. Add the [app bundle IDs](../configuration/bundle-ids-built-in-ios-apps.md) for any non-Microsoft apps using single sign-on (SSO). The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add Microsoft apps to your policy.

    Don't add the Microsoft Authenticator app to the SSO extension either.  That app is added later in an app policy.

    To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

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
11. Go to **Apps** > **All Apps** and assign Microsoft Authenticator to groups as a required app. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md) and [Assign apps to groups](../apps/apps-deploy.md).  

## Next steps   
Create an enrollment profile for enrolling devices. The enrollment profile triggers the device user's enrollment experience, and enables them to initiate enrollment. For information about how to create a profile for supported enrollment types, see the following resources:  

* [Account driven user enrollment](apple-account-driven-user-enrollment.md)  
* [User enrollment with Company Portal](apple-user-enrollment-with-company-portal.md)  
* [Apple automated device enrollment for Setup Assistant with modern authentication](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) 
* [Web based device enrollment](web-based-device-enrollment-ios.md)
* [Device enrollment with Company Portal](ios-device-enrollment.md#app-or-web-based-enrollment)  
