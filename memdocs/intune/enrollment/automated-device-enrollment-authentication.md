---
# required metadata

title: Authentication methods for automated device enrollment 
titleSuffix: Microsoft Intune
description: Describes the Intune-supported authentication methods you can use with automated device enrollment. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/19/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Authentication methods for automated device enrollment  

*Applies to iOS/iPadOS*  

This article describes the authentication methods available for iOS/iPadOS devices enrolled in Intune via automated device enrollment. During authentication, users sign in and devices go through Azure AD registration, Intune enrollment, and Intune compliance checks. 

Available authentication methods include: 

* Intune Company Portal app 
* Setup Assistant with modern authentication
* Just in Time (JIT) Registration for Setup Assistant with modern authentication 
* Setup Assistant (legacy)

All methods are for corporate-owned devices with user affinity and purchased through Apple Business Manager or Apple School Manager.   

## Intune Company Portal app  

Use the Intune Company Portal app as the authentication method if you want to:  
 - Use multifactor authentication.
 - Prompt users to change their passwords when they first sign in.
 - Prompt users to reset their expired passwords during enrollment.  

These features aren't supported in Apple Setup Assistant authentication methods. 

## Setup Assistant (legacy)  
 Use the legacy Setup Assistant if you want users to experience the typical, out-of-box-experience for Apple products. This option installs standard preconfigured settings when the device enrolls in Intune. If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. [Learn more](/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true). 


## Setup Assistant with modern authentication  
This method provides the same security as Company Portal authentication but lets the device user access parts of the device even if the Company Portal hasn't been installed. Setup Assistant with modern authentication is supported on devices running iOS/iPadOS 13.0 and later. Older iOS/iPadOS devices given this type of profile will fall back to **Setup Assistant (legacy)** authentication. 

### Install Company Portal with VPP (recommended)  

Sometimes the option to install Company Portal is hidden from users, and the app is installed without user interaction. The app is automatically installed in two situations where Setup Assistant with modern authentication is used:  

 - You select **Install Company Portal with VPP** in the same enrollment profile. We recommend selecting this option. 
 - An employee or student sets up their Apple ID account during Setup Assistant.

In both of these situations, the Company Portal becomes a required app on the device. When the device user reaches the home screen, Intune automatically applies the correct app configuration policy to the device. 

>[!CAUTION]
>Don't send a separate app configuration policy to the Company Portal for iOS/iPadOS devices after enrolling with Setup Assistant with modern authentication. Doing so will result in an error.  

If you don't use the VPP option, the device user must enter an Apple ID to install Company Portal. They can enter it during Setup Assistant or when Intune tries to install Company Portal. 

### Multi-factor authentication  

Multi-factor authentication is required if a conditional access policy that requires [multi-factor authentication (MFA)](multi-factor-authentication.md) is applied at enrollment or during Company Portal sign-in. However, MFA is optional based on the Azure AD settings in the targeted Conditional Access policy.  

### Authentication in Company Portal  

After they go through the Setup Assistant screens, the device user lands on the home page. At this point, their user affinity is established. However, until the user signs in to the Company Portal using their Azure AD credentials and selects **Begin**, the device:

- Won’t be fully registered with Azure AD.  
- Won’t show up in the user’s device list in the Azure AD portal.  
- Won’t have access to resources protected by conditional access.  
- Won’t be evaluated for device compliance.  
- Will be redirected to the Company Portal from other apps if the user tries to open any managed applications that are protected by conditional access.  

## Just in Time (JIT) Registration for Setup Assistant with modern authentication
This option is the same as Setup Assistant with modern authentication, except that Company Portal isn't required to register or enroll a device with this option. Instead, enrollment, Azure AD registration, and compliance checks can be fully integrated with any Office app.  

Intune uses Apple single sign-on (SSO) extension functionality to reduce authentication prompts and establish SSO across the whole device.
* The first authentication handles enrollment and user-device affinity, and happens when the device user turns on their device and signs into Setup Assistant.  
* The second authentication handles Azure AD registration and happens when the user signs into the designated Office app. Compliance checks are also done right in the Office app.   

To set up JIT Registration, you need create a device configuration policy and configure single sign on. Complete these steps before you create an enrollment profile.  For more information, see [Set up Just in Time Registration](automated-device-enrollment-authentication.md#set-up-just-in-time-registration) in the next section.  

## Set up Just in Time Registration 
Complete these steps to configure Just in Time (JIT) Registration for Setup Assistant with modern authentication. 

>[!Important]
>Before you begin, revisit all Conditional Access policies targeted at devices enrolling with JIT Registration, and exclude Microsoft Intune from each policy. 

1. Sign in to the Microsoft Endpoint Manager admin center. 
2. [Create an iOS/iPadOS device configuration policy](../configuration/device-features-configure.md) under **Device features** > **Category** > [**Single sign-on app extension**](../configuration/device-features-configure.md#single-sign-on-app-extension).  
3. For **SSO app extension type**, select **Microsoft Azure AD**.
4. Add the [app bundle IDs](../configuration/bundle-ids-built-in-ios-apps) for the apps using single sign-on (SSO). For best practices and important considerations, see [Best practices for SSO configuration](automated-device-enrollment-authentication.md#best-practices-for-sso-configuration) in this article.  
5. Under **Additional configuration**, add the required key value pair:  
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}}
4. (Recommended) Add the key value pair that enables SSO in the Safari browser for all apps in the policy: 
    * Key: browser_sso_interaction_enabled
    * Type: Integer
    * Value: 1
5. Designate the Microsoft Authenticator app as a required app and then assign it to a group. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md) and [Assign apps to groups](../apps/apps-deploy.md).  
6. [Create an enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) and select **Setup Assistant with modern authentication** as the authentication method. An active automated device token from Apple Business Manager or Apple School Manager must be present in Intune to create an enrollment profile.     
7. Finish configuring your enrollment profile and then on the **Assignments** page, assign the profile to the devices synced over from Apple Business Manager and Apple School Manager. 

>[!TIP]  
>The Company Portal is still sent the device as a required app, but with JIT Registration it isn't required for Azure AD registration or compliance. Instead, device users can use the Company Portal app to [gather and upload logs](../user-help/send-logs-to-microsoft-ios.md) if they experience issues in the app.   

Once the profile has been assigned, employees and students can complete setup and authentication on their devices. 

### Best practices for SSO configuration   
* You don't need to manually add apps that use the Microsoft Authentication Library (MSAL) to the device configuration policy. Apps that only use Azure Active Directory Authentication Library (ADAL) must be manually added. As more apps migrate over to MSAL, there will be less of a need to manually add apps to the policy.  

* To make the experience easier for device users, we recommend adding all Microsoft Office apps you want the SSO extension to apply to. The user's first sign-in has to happen in an app that's configured with the SSO extension. Otherwise, Azure AD registration can't be completed. For example, if you only add Microsoft Teams, it will be the only app that can initiate Azure AD registration with the SSO extension. In that scenario:     
    1. The device user tries to sign into a different app first, such as Microsoft Outlook.
    2. Conditional Access blocks the user from signing in.  
After the user signs in to the appropriate app, SSO signs the user into all apps that are a part of the SSO extension policy. At this point, the device user can manually sign into apps that that don't use the SSO extension.  

### Example of successful authentication  
The following sequence of events describe what a successful authentication looks like with JIT Registration for Setup Assistant with modern authentication.  

1. The device user turns on the device.
2. Setup Assistant begins. The device user authenticates with their Azure AD credentials in Setup Assistant.
3. The device user completes multi-factor authentication if that's required in the Conditional Access policy. 
4. The device finishes enrolling in Intune and user-device affinity is established. 
5. The device user lands on the home screen and opens Microsoft Outlook or another SSO-configured Office app and signs in with their work account. If the device meets all compliance requirements, the device user will have access to their email right away. 
6. The SSO extension establishes single sign-on in all other targeted apps.  
7. The device is registered with Azure AD and compliant. You can view the status of the device in the admin center and Azure AD.   
8. The device user opens Teams and is automatically signed in. The end user opens Word, PowerPoint, and Excel, and is automatically signed in.  



