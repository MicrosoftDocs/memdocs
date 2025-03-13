---
# required metadata

title: Set up personal device for work | Microsoft Docs
description: Describes how to enroll and register a personal iPhone or iPad for work or school using Intune Company Portal.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/13/2025
ms.topic: end-user-help
ms.localizationpriority: high
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 6eeec7aa-1b07-4ce3-894c-13e09b89bdd4
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience: 

ms.reviewer: rishitasarin 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Set up personal iOS device for work or school      

**Applies to iOS/iPadOS**  
Enroll and register your iPhone or iPad for work or school to access apps, Wi-Fi, and other resources. This article describes how to enroll your personal device using the following enrollment options:

- Account driven user enrollment 
- Device enrollment with Microsoft Intune Company Portal app
- Web enrollment
- Determine based on your choice 

Typically, your organization decides which method to use. Refer to your organization's onboarding documentation to find out which method to use. To enroll a brand new corporate-owned device, see [Set up access on new work or school device](enroll-your-device-dep-ios.md).    

> [!IMPORTANT]
> We don't sell any data collected by our service to any third parties for any reason.  

> [!NOTE]
> If you tried to access your work email in the Mail app, and received a prompt to get your device managed, you're in the right place. Follow the instructions in this article to regain access to your email and other work resources on your iOS device.   

## Account driven user enrollment    
Initiate enrollment in the Settings app by signing in with your work or school account, or organization-provided Apple ID. After you approve remote management, the enrollment profile silently installs and your organization's Intune policies apply, enabling you to sign in to apps such as Microsoft Teams and Microsoft Outlook with your work account. For this process, you need: 

- Safari web browser  
- iOS/iPadOS version 15 or later  
- Stable Wi-Fi connection  

If this method is unavailable on your device, enroll your device with the Company Portal app or via web enrollment.    

1. Open the Settings app on your device.  

1. Go to **General** > **VPN & Device Management**.  

1. Tap the option to sign in with your work or school account. Sign in with your work or school account, or with the Apple ID provided to you by your organization.  

1. Sign in to iCloud. Enter the password for the username that appears onscreen. Then select **Continue**.  

1. Tap **Allow Remote Management**.      

1. Wait a few minutes while your device is configured and the configuration profile is installed.  

1. To confirm your device is ready to use for work, return to **VPN & Device Management** in your Settings app. Confirm that your work account is listed as a managed account.  

1. Microsoft Authenticator is required to access work apps. Wait a few minutes after enrollment for Authenticator to install on your device. An error message appears if you try to sign in to a work app without Authenticator.  

1. Approve other work apps, as necessary. As you receive each prompt, select **Install** to approve its installation. 

1. Sign in to a work app, such as Microsoft Teams, with your work or school account. The first time you sign in, your device will be checked to ensure it meets your organization's device and security policies. If your device is compliant, you can access your work account. If not, you receive a prompt to update your device settings.


## Device enrollment with Company Portal app  

Initiate enrollment in the Intune Company Portal app. The Company Portal app is used to enroll and manage your device, install work apps, and get IT support. The app supports devices running iOS 14.0 and later.   Maintain a Wi-Fi connection until all steps are complete. Pausing for more than a few minutes during device enrollment might cause the Company Portal app to close or end setup. If this happens, reopen the app and try again.    
 
For this process, you need: 


- Safari web browser  
- iOS/iPadOS version 14 or later  
- Stable Wi-Fi connection  
- [Intune Company Portal app](https://apps.apple.com/us/app/intune-company-portal/id719171358)(opens the Apple App Store) 
- Latest version of the Microsoft Authenticator app

1. Open the Company Portal app, and sign in with your work or school account (example: user@contoso.com).  

1. Sign in to the Company Portal app with your work or school account. Example: jojordan@contoso.com  

1. On the **How to set up your device** screen, review the enrollment steps and information about what your organization can see and do on an enrolled device. Then select **Get started**.

1. The Safari web browser opens the Intune Company Portal website. When prompted to, select **Allow** to download the Intune configuration profile for your device.

1. A pop-up appears when installation is complete. Select **Close**.   

1. Open the Settings app on your device and go to **Profile Downloaded**.   
    - If this option isn't available, go to **General** > **VPN & Device Management**.  

1. Tap **Management Profile**. Then tap **Install**. 

1. You might need to reenter your passcode. Then tap **Install** again.   

1. When prompted to, read the remote management warning. Tap **Install** again to continue. Then tap **Trust**.  

1. Wait while the management profile installs. Tap **Done** when installation is complete.  

1. Return to the Company Portal app and go to **Notifications**. Under pending requirements, tap the option to register your device. 

1. Wait a few minutes while your device receives apps and policies from your organization.  
    - After enrollment, you might receive prompts from your organization to install required apps. Tap **Install** on the app prompts to install the apps.     

    - If you already installed Microsoft Authenticator on your device, you're prompted to allow Microsoft to take management of the Microsoft Authenticator app. Tap **Manage** to allow. 

    - Your organization might require a mobile threat defense app on your device, which monitors your work apps for threats and viruses. Tap **Install** to proceed with installation. If the app is a requirement and you skip installation, you might not be allowed to access work resources. 

1. Go to a work app like Microsoft Teams or Microsoft Outlook and sign in with your work or school account to confirm that you have access.  
    1. If access is limited due to compliance requirements, you receive an in-app prompt upon sign-in. Tap **Check compliance** to open Company Portal and review pending notifications and requirements. 

    1. After you update device settings, tap **Retry** to recheck and refresh your compliance status. If the retry fails right away, wait a few minutes for your most recent changes to register with Microsoft. Then try again. 

## Web enrollment  
Initiate enrollment on the Intune Company Portal website. For this process, you need: 

- Safari web browser  
- iOS/iPadOS version 15 or later  
- Stable Wi-Fi connection  

1. Open Safari and go to https://portal.manage.microsoft.com/enrollment/webenrollment/ios. Sign in with your work or school account.  

1. When prompted to, download the configuration profile. Wait in Safari while Company Portal downloads the profile.  

1. Open the Settings app on your device and go to **General** > **VPN & Device Management** to view and install the new configuration profile.
    1. Select **Profile Downloaded**.
    2. Select **Install** and follow the onscreen instructions to install the profile.  

1. Wait until Microsoft Authenticator is installed on the device before signing into a work or school app. The device won't be ready for work use until Authenticator is on the device, which can take a few minutes. To verify that Authenticator installed, open your device settings and go to **Profile** > **Management Profile** > **Single Sign On Extension**. Authenticator should be listed as the SSO extension. 

1. Sign in to a work app, such as Microsoft Teams, with your work account.  

1. Wait while the app identifies required setting updates. For example, you may be required to update your device's operating system before you can use the app. Check the app you're signed into for pending action items. When you're done making changes, select Recheck.

## Determine based on user choice  


## IT administrator support  
If you're an IT administrator and run in to problems while enrolling devices, see [Troubleshooting iOS device enrollment problems in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors). This article lists common errors, their causes, and steps to resolve them.  

## Next steps  
Find apps that will help you at work or school. Learn [how apps are made available](use-managed-apps-on-your-device-ios.md) to you through Company Portal.  

Still need help? Check in with your company support. You can find their contact information on the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
