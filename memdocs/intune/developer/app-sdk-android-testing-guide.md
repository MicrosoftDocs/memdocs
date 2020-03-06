---
# required metadata

title: Microsoft Intune App SDK for Android testing guide
description: The Microsoft Intune App SDK for Android testing guide helps you test your Intune-managed Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Microsoft Intune App SDK for Android testing guide

This guide helps developers test their Intune-managed Android apps.  

## Prerequisite test accounts
You can create new accounts with or without pre-generated data. To create a new account:
1. Go to the [Microsoft Demos](https://demos.microsoft.com/environments/create/tenant) site. 
2. [Set up Intune](../fundamentals/setup-steps.md) to enable mobile device management (MDM).
3. [Create users](../fundamentals/users-add.md).
4. [Create groups](../fundamentals/groups-add.md).
5. [Assign licenses](../fundamentals/licenses-assign.md) as appropriate for your testing.


## Azure portal policy configuration
[Create and assign app protection policies](../apps/app-protection-policies.md) in the [Azure portal's Intune blade](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview). You can also create and assign your [app configuration policy](../apps/app-configuration-policies-overview.md) in the Intune blade.

> [!NOTE]
> If your app isn't listed in the Azure portal, you can target it with a policy by selecting the **more apps** option, and providing the package name in the text box.

## Test cases

The following test cases provide configuration and confirmation steps. Use this guidance to help troubleshoot Intune-managed Android app issues.

### Required PIN and corporate credentials

You can require a PIN to access corporate resources. Also, you can enforce corporate authentication before users can use managed apps. Here's how:

1. Set **Require PIN for access** and **Require corporate credentials for access** to **Yes**. For more information, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Confirm the following conditions:
    - App launch should present a prompt for PIN input, or the production user that was used during enrollment with the Company Portal.
    - Failure to present a valid sign-in prompt might be due to an incorrectly configured Android manifest, specifically the values for Azure Active Directory Authentication Library (ADAL) integration (SkipBroker, ClientID, and Authority).
    - Failure to present any prompt might be due to an incorrectly integrated `MAMActivity` value. For more information about `MAMActivity`, see [Microsoft Intune App SDK for Android developer guide](app-sdk-android.md).

> [!NOTE] 
> If the preceding test isn't working, the following tests will likely also fail. Review [SDK](app-sdk-android.md#sdk-integration) and [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal) integration.

### Restrict transferring and receiving data with other apps
You can control data transfer between corporate managed applications, as follows:

1. Set **Allow app to transfer data to other apps** to **Policy-managed apps**.
2. Set **Allow app to receive data from other apps** to **All apps**. Use of intents and content providers are affected by these policies.
3. Confirm the following conditions:
    - Opening from an unmanaged app into your app functions correctly.
    - Sharing content between managed apps is allowed.
    - Sharing from managed apps to non-managed apps (for example, Chrome) is blocked.

### Restrict cut, copy, and paste
You can restrict the system clipboard to managed applications, as follows:

1. Set **Restrict cut, copy, and paste with other apps** to **Policy managed with paste in**.
2. Confirm the following conditions:
    - Copying text from your app into an unmanaged app (for example, Messages) is blocked.

### Prevent save
You can control **Save As** functionality, as follows:

1. If your app requires [integrated Save As controls](app-sdk-android.md#example-determine-if-saving-to-device-or-cloud-storage-is-permitted), set **Prevent 'Save As'** to **Yes**.
2. Confirm the following conditions:
    - Save is restricted to only appropriate managed locations.

### File encryption
You can encrypt data on the device, as follows:

1. Set **Encrypt app data** to **Yes**.
2. Confirm the following conditions:
    - Normal application behavior isn't affected.

### Prevent Android backups
You can control app backup, as follows:

1. If you have set [integrated backup restrictions](app-sdk-android.md#protecting-backup-data), set **Prevent Android backups** to **Yes**.
2. Confirm the following conditions:
    - Backups are restricted.

### Unenrollment
You can remotely wipe managed apps from containing corporate email and documents, and personal data is decrypted when it's no longer administered. Here's how:

1. From the Azure portal, [issue a wipe](../apps/apps-selective-wipe.md).
2. If your app doesn't register for any wipe handlers, confirm the following conditions:
    - A full wipe of the app occurs.
3. If your app has registered for `WIPE_USER_DATA` or `WIPE_USER_AUXILARY_DATA`, confirm the following conditions:
    - The managed content is removed from the app. For more information, see [Intune App SDK for Android developer guide - selective wipe](app-sdk-android.md#selective-wipe).

### Multi-identity support
Integrating [multi-identity support](app-sdk-android.md#multi-identity-optional) is a high risk change that needs to be thoroughly tested. The most common issues occur because of improperly setting the identity (context vs. threat level), and tracking files (`MAMFileProtectionManager`).

Minimally, confirm that:

- **Save As** policy is working correctly for managed identities.
- Copy and paste restrictions are correctly enforced from managed to personal.
- Only data belonging to the managed identity is encrypted, and personal files aren't modified.
- Selective wipe during unenrollment only removes the managed identity data.
- The user is prompted for conditional launch when changing from an unmanaged to a managed account (first time only).

### App configuration (optional)
You can configure behavior of managed apps. If your app consumes any app configuration settings, you should test that your app correctly handles all values that you (as the admin) can set. You can create and assign [app configuration policies](../apps/app-configuration-policies-overview.md) in Intune.

## Next steps

- [Add an Android line-of-business app to Microsoft Intune](../apps/lob-apps-android.md)
