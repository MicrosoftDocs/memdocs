---
# required metadata

title: Android apps with app protection policies
description: This topic describes what to expect when your app is managed by app protection policies.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/02/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# What to expect when your Android app is managed by app protection policies

This article describes the user experience for apps with app protection policies. App protection policies are applied only when apps are used in a work context: for example, when the user is accessing apps with a work account or accessing files that are stored in a OneDrive for Business location.

## Access apps

The Company Portal app is required for all apps that are associated with app protection policies on Android devices.

For devices that are not enrolled in Intune, the Company Portal app must be installed on the device. However, the user does not have to launch  or sign into the Company Portal app before they can use apps that are managed by app protection policies.

The Company Portal app is a way for Intune to share data in a secure location. Therefore, the Company Portal app is a requirement for all apps that are associated with app protection policies, even if the device is not enrolled in Intune.

## Use apps with multi-identity support

App protection polices are only applied in the work context. Therefore, the app might behave differently depending on whether the context is work or personal.

For example, the user gets a PIN prompt when accessing work data. For the **Outlook app**, the user is prompted for a PIN when they launch the app. For the **OneDrive app**, the user is prompted for the pin when they type in the work account. For Microsoft **Word**, **PowerPoint**, and **Excel**, the user is prompted for the pin when they access documents that are stored in the company OneDrive for Business location.

## Manage user accounts on the device

Multi-identity applications allow users to add multiple accounts.  Intune APP supports only one managed account.  Intune APP does not limit the number of unmanaged accounts.

When there is a managed account in an application:

* If a user attempts to add a second managed account, the user is asked to select which managed account to use.  The other account is removed.
* If the IT admin adds a policy to a second existing account, the user is asked to select which managed account to use.  The other account is removed.

Read the following example scenario to get a deeper understanding of how multiple user accounts are treated.

User A works for two companies—**Company X** and **Company Y**. User A has a work account for each company, and both use Intune to deploy app protection policies. **Company X** deploys app protection policies **before** **Company Y**. The account that's associated with **Company X** gets the app protection policy, but not the account that's associated with Company Y. If you want the user account that's associated with Company Y to be managed by the app protection policies, you must remove the user account that's associated with Company X and add the account that is associated with Company Y.

### Add a second account

#### Android

If you are using an Android device, you might see a blocking message with instructions to remove the existing account and add a new one.  To remove the existing account, go to **Settings  &gt;General &gt; Application Manager &gt;Company Portal.** Then choose **Clear Data**.

![Screenshot of the error message and instructions to remove the account](./media/end-user-mam-apps-android/Android_SwitchUser.png)

## View protected media files with the Azure Information Protection app

To view protected PDF and image files on iOS or Android devices, use the Azure Information Protection app, previously known as the Rights Management sharing app: [iTunes](https://apps.apple.com/app/microsoft-rights-management/id689516635) | [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)

For more information, see [Mobile viewer apps for Azure Information Protection on iOS and Android](/azure/information-protection/rms-client/mobile-app-faq).

## Next steps
[What to expect when your iOS/iPadOS app is managed by app protection policies](end-user-mam-apps-ios.md)
