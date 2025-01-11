---
# required metadata

title: Authentication methods for Apple automated device enrollment | Microsoft Intune
titleSuffix: Microsoft Intune
description: Describes the Intune-supported authentication methods you can use with automated device enrollment. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/23/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
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
- tier1
- M365-identity-device-management
- highpri
---

# Authentication methods for automated device enrollment in Intune    

*Applies to iOS/iPadOS*  

This article describes the authentication methods available for iOS/iPadOS devices enrolled in Intune via automated device enrollment. Available authentication methods include: 

* Intune Company Portal app 
* Setup Assistant with modern authentication
* Just in Time (JIT) Registration for Setup Assistant with modern authentication  
* Setup Assistant (legacy)

All methods are available for corporate-owned devices with user affinity and purchased through Apple Business Manager or Apple School Manager.   

## Option 1: Intune Company Portal app  

Use the Intune Company Portal app as the authentication method if you want to:  
 - Use multifactor authentication (MFA).
 - Prompt users to change their passwords when they first sign in.
 - Prompt users to reset their expired passwords during enrollment.  
 - Register devices in Microsoft Entra ID and use features available with Microsoft Entra ID, such as Conditional Access.
 - Automatically install the Company Portal app during enrollment. If your company uses the Volume Purchase Program (VPP), you can automatically install Company Portal app during enrollment without user Apple IDs. 
 - You want to lock the device until the Company Portal app installs.

> [!CAUTION]
> Intune will block an enrollment that uses this authentication method if the device user is targeted with an [account driven Apple user enrollment profile type](apple-account-driven-user-enrollment.md). This behavior is expected. The user receives an error message that says their account doesn't support enrollment through the Company Portal app, and that they need to enroll through the Company Portal website. To ensure successful enrollments via automated device enrollment, use [Option 2: Setup Assistant with modern authentication](automated-device-enrollment-authentication.md#option-2-setup-assistant-with-modern-authentication) as the authentication method when working with account driven Apple User Enrollment profile types.

## Option 2: Setup Assistant with modern authentication

This option provides the same security as Intune Company Portal authentication but is different because it lets the device user access parts of the device even if the Company Portal hasn't been installed.  Use this option for authentication when you want to:

* Wipe the device. 
* Use multifactor authentication (MFA).  
* Prompt users to change their passwords when they first sign in.
* Prompt users to reset their expired passwords during enrollment.  
* Register devices in Microsoft Entra ID and use features available with Microsoft Entra ID, such as Conditional Access. 
* Automatically install the Company Portal app during enrollment. If your company uses the Volume Purchase Program (VPP), you can automatically install Company Portal app during enrollment without user Apple IDs. 
* Allow users to use the device even when the Company Portal app isn't installed.  

Setup Assistant with modern authentication is supported on devices running iOS/iPadOS 13.0 and later. Older iOS/iPadOS devices that are assigned this type of profile will fall back on **Setup Assistant (legacy)** authentication. 

### Automatically install Company Portal app  

If your company uses the Volume Purchase Program (VPP), you can automatically install the Company Portal app during enrollment without user Apple IDs. To enable automatic installation in your enrollment profile, select **Yes** for **Install Company Portal with VPP**. We recommend using this option. 

If you don't use the VPP option, the device user must enter their Apple ID during Setup Assistant or when Intune tries to install Company Portal.  

In both scenarios, the Company Portal installation option is hidden from the device user, and the Company Portal becomes a required app on their device. When the user reaches the home screen, Intune automatically applies the correct app configuration policy to the device.  

>[!CAUTION]
>Don't send a separate app configuration policy to the Company Portal for iOS/iPadOS devices after enrolling with Setup Assistant with modern authentication. Doing so will result in an error.  

<a name='multi-factor-authentication'></a>

### Multifactor authentication  

Multifactor authentication (MFA) will be required if a [Conditional Access policy that requires it](multi-factor-authentication.md) is applied at enrollment or during Company Portal sign-in. However, MFA is optional, based on the Microsoft Entra settings in the targeted Conditional Access policy.  

External authentication methods are supported in Microsoft Entra ID, which means you can use your preferred MFA solution to facilitate MFA during device enrollment. If you choose to use a third-party MFA provider, before you deploy enrollment profiles to all devices, do a test run to ensure that both the Microsoft Entra MFA screen and MFA work during enrollment. For more information and support details about external authentication methods, see [Public preview: External authentication methods in Microsoft Entra ID](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/public-preview-external-authentication-methods-in-microsoft/ba-p/4078808).  

### Company Portal action required  

After they go through the Setup Assistant screens, the device user lands on the home page. At this point, their user affinity is established. However, until the user signs in to the Company Portal using their Microsoft Entra credentials and selects **Begin**, the device:

- Won’t be fully registered with Microsoft Entra ID.  
- Won’t show up in the user’s device list in Microsoft Entra ID.   
- Won’t have access to resources protected by Conditional Access.  
- Won’t be evaluated for device compliance.  
- Will be redirected to the Company Portal from other apps if the user tries to open any managed applications that are protected by Conditional Access.  

## Option 3: Just in Time Registration for Setup Assistant with modern authentication

This option is the same as Setup Assistant with modern authentication, except that Company Portal isn't required for Microsoft Entra registration or compliance. Instead, Microsoft Entra registration and compliance checks are fully integrated in a designated Microsoft or non-Microsoft app that's configured with the Apple single sign-on (SSO) app extension. The extension reduces authentication prompts and establishes SSO across the whole device. JIT Registration prompts users to authenticate twice:

* One authentication handles enrollment and user-device affinity, and happens when the device user turns on their device and signs into Setup Assistant.  
* Another authentication handles Microsoft Entra registration and happens when the user signs into the designated app. Compliance checks are also done in this app. 

> [!NOTE]
> If your organization uses Microsoft Defender for Endpoint, for JIT registration and compliance remediation to work as expected, make sure the Microsoft Defender for Endpoint app **isn't** the first app users open.

Once the device user reaches the home screen, they can sign in to any work or school app that's configured with the SSO extension to complete Microsoft Entra registration and compliance checks. SSO signs the user into all apps that are a part of your SSO extension policy. At that point, they can also manually sign into any app that isn’t configured to use the SSO extension.  

To set up JIT Registration with automated device enrollment:

1. Create a device configuration policy and configure the settings under the **Single sign-on app extension** category. For steps, see [Set up just in time registration](set-up-just-in-time-registration.md).  
2. [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) and select **Setup Assistant with modern authentication** as the authentication method. An active automated device enrollment token from Apple Business Manager or Apple School Manager must be present in Intune to complete this step. 
3. When you get to the **Assignments** page in the enrollment profile, assign the profile to the devices synced from Apple Business Manager and Apple School Manager. After you assign the profile, employees and students can complete setup and authentication on their devices.    

   > [!NOTE]  
   > The Company Portal is still sent to devices as a required app, even though it isn't required for Microsoft Entra registration or compliance. Device users can use the Company Portal app to [gather and upload logs](../user-help/send-logs-to-microsoft-ios.md) if they experience issues in the app.  

### Example of successful authentication

The following sequence of events describes an example of what a successful authentication looks like with JIT Registration for Setup Assistant with modern authentication. Your organization's experience may be different depending on your automated device enrollment configurations.    

1. The device user turns on the device.
2. Setup Assistant begins. The device user authenticates with their Microsoft Entra credentials in Setup Assistant.
3. The device user completes multifactor authentication if that's required in the Conditional Access policy. 
4. The device finishes enrolling in Intune and user-device affinity is established. 
5. The device user lands on the home screen and opens Microsoft Teams or another Office app and signs in with their work account. If the device meets all compliance requirements, the device user will have access to their messages and calendar right away.  

   > [!NOTE]
   > During Microsoft Entra registration, the device user may see a short spinner while Intune finishes the compliance checks. This is expected behavior.

6. The SSO extension establishes single sign-on in all other targeted apps and all Microsoft apps.  
7. The device is registered with Microsoft Entra ID and compliant. You can view the status of the device in the admin center and Microsoft Entra ID. The device user can view the status in Intune Company Portal and use Company Portal for compliance, app inventory, device syncs, and log sharing.    
8. The device user opens Teams and is automatically signed in.
   
## Option 4: Setup Assistant (legacy)

Use the legacy Setup Assistant if you want users to experience the typical, out-of-box-experience for Apple products. This option installs standard preconfigured settings when the device enrolls in Intune. Use this option for authentication when: 

 * You want to wipe a device. 
 * You don't want modern authentication features such as multifactor authentication.
 * You don't want to register devices in Microsoft Entra ID. Setup Assistant (legacy) authenticates the user with the Apple .p7m token. 

 If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. For more information, see [Get-AdfsEndpoint](/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true) in our Windows PowerShell Reference guide.  

## Next steps

Now that you know which authentication method you're using, [create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) and select the authentication method when prompted. An active automated device enrollment token from Apple Business Manager or Apple School Manager must be present in Intune to complete this step.
