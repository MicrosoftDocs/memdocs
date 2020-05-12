---
# required metadata

title: iOS/iPadOS apps with app protection policies
description: This topic describes what to expect when your iOS/iPadOS app is managed by app protection policies.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: b57e6525-b57c-4cb4-a84c-9f70ba1e8e19

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: andcerat
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# What to expect when your iOS/iPadOS app is managed by app protection policies

Intune app protection policies apply to apps that used for work or school. This means that when your employees and students use their apps in a personal context, they may notice no difference in their experience. In the work or school context, however, they might receive prompts to make account decisions, update their settings, or contact you for help. Use this article to learn what your users experience when they try to access and use Intune-protected apps.  

## Access apps

If the device is **not enrolled in Intune**, the user is asked to restart the app when they first use it. A restart is required so that app protection policies can be applied to the app.

<!--- The following screenshot from the Skype app illustrates this restart request: --->

<!---  ![Screenshot of the iOS/iPadOS device showing PIN prompt](./media/end-user-mam-apps-ios/iOS_AppPINPrompt.png) --->

For devices that are **enrolled for management in Intune**, the user sees a message that their app is now managed.

## Use apps with multi-identity support

Apps that support multi-identity let you use different work and personal accounts to access the same apps. App protection policies, like entering a device PIN, are activated when users access these apps in a work or school context.   

Users might experience the PIN prompt differently across all of their apps, depending on how you configure the policies.  For example, you might configure your policies so that:       
* Microsoft Outlook prompts the user for a PIN when they launch the app. 
* OneDrive prompts the user for a pin when they sign in to their work account.  
* Microsoft Word, PowerPoint, and Excel prompts the user for a pin when they access documents that are stored in the company OneDrive for Business location.  

- Learn more about the apps that support [app protection and multi-identity](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) with Intune.  

## Manage user accounts on the device  

Intune app protection policies limit users to one managed work or school account per app. App protection policies don't limit the number of unmanaged accounts a user can add.   

- If a user attempts to add a second managed account, the user is asked to select which managed account to use. If the user adds the second account, the first account is removed.
- If you add protection policies to another one of your user's accounts, the user is asked to select which managed account to use. The other account is removed. 

Some users won't get the option to switch or select between managed accounts. The option is not available on devices that are:
* Managed by Intune  
* Managed by third-party enterprise mobility management solutions and configured with the IntuneMAMUPN setting 

The following example scenario describes how multiple user accounts are treated:  

User A works for two companies—**Company X** and **Company Y**. User A has a work account for each company, and both use Intune to deploy app protection policies. **Company X** deploys app protection policies **before** **Company Y**. The account that's associated with **Company X** gets the app protection policy first. If you want the user account that's associated with Company Y to be managed by the app protection policies, you must remove the user account that's associated with Company X and add the user account that's associated with Company Y.  

## Next steps

[What to expect when your Android app is managed by app protection policies](end-user-mam-apps-android.md)
