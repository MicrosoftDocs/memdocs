---
# required metadata

title: Microsoft Intune App SDK for Android developer testing guide
description: The Microsoft Intune App SDK for Android testing guide helps you test your Intune-managed Android app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- M365-identity-device-management
- Android
---

# Microsoft Intune App SDK for Android developers testing guide

The Microsoft Intune App SDK for Android testing guide is designed to help you test your Intune-managed Android app.

## Demo tenant setup
If you do not already have a tenant with your company, you can create a demo tenant with or without pre-generated data. You must register as a [Microsoft partner](https://partner.microsoft.com/business-opportunities/why-microsoft) to access Microsoft CDX. To create a new account:
1. Navigate to the [Microsoft CDX tenant creation site](https://cdx.transform.microsoft.com/my-tenants/create-tenant) and create a Microsoft 365 Enterprise tenant.
2. [Set up Intune](../fundamentals/setup-steps.md) to enable mobile device management (MDM).
3. [Create users](../fundamentals/users-add.md).
4. [Create groups](../fundamentals/groups-add.md).
5. [Assign licenses](../fundamentals/licenses-assign.md) as appropriate for your testing.


## App protection policy configuration
[Create and assign app protection policies](../apps/app-protection-policies.md) in the Microsoft Endpoint Manager admin center. In addition to creating app protection policies, you can create and assign an [app configuration policy](../apps/app-configuration-policies-overview.md) in Endpoint Manager.

> [!NOTE]
> If your app isn't listed in the Microsoft Endpoint Mangager portal, you can target it with a policy by selecting the **more apps** option and providing the package name in the text box.

## Test Cases

The following test cases provide configuration and confirmation steps. Use these tests to verify your newly integrated Android app.

### Required PIN and corporate credentials

You can require a PIN to access corporate resources. Also, you can enforce corporate authentication before users can use managed apps. Here's how:

1. Set **Require PIN for access** and **Require corporate credentials for access** to **Yes**. For more information, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Confirm the following conditions:
    - App launch should present a prompt for PIN input, or the production user that was used during enrollment with the Company Portal.
    - Failure to present a valid sign-in prompt might be due to an incorrectly configured Android manifest, specifically the values for MSAL integration (SkipBroker, ClientID, and Authority).
    - Failure to present any prompt might be due to an incorrectly integrated `MAMActivity` value. For more information about `MAMActivity`, see [Microsoft Intune App SDK for Android developer guide](app-sdk-android.md).

> [!NOTE] 
> If the preceding test isn't working, the following tests will likely also fail. Review [SDK](app-sdk-android.md#sdk-integration) and [MSAL configuration](app-sdk-android.md#configure-microsoft-authentication-library-msal) integration.

### Restrict transferring and receiving data with other apps
You can control data transfer between corporate managed applications, as follows:

1. Set **Allow app to transfer data to other apps** to **Policy-managed apps**.
2. Set **Allow app to receive data from other apps** to **All apps**. 

Use of intents and content providers are affected by these policies.
3. Confirm the following conditions:
    - Opening from an unmanaged app into your app functions correctly.
    - Sharing content between your app and managed apps is allowed.
    - Sharing from your app to non-managed apps (for example, Chrome) is blocked.

#### Restrict receiving data from other apps

1. Set **Send org data to other apps** to **All apps**.
2. Set **Receive data from other apps** to **Policy managed apps**. 
3. Confirm the following conditions:
    - Sending to an unmanaged app from your app functions correctly.
    - Sharing content between your app and managed apps is allowed.
    - Sharing from non-managed apps (for example, Chrome) to your app is blocked.

If your app requires [integrated 'open from' controls](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location), you can control **open from** functionality as follows:

1. Set **Receive data from other apps** to **Policy managed apps**. 
2. Set **Open data into org documents** to **Block**. 
3. Confirm the following conditions:
    - Opening is restricted to only appropriate managed locations.

### Restrict cut, copy, and paste
You can restrict the system clipboard to managed applications, as follows:

1. Set **Restrict cut, copy, and paste with other apps** to **Policy managed with paste in**.
2. Confirm the following conditions:
    - Copying text from your app into an unmanaged app (for example, Messages) is blocked.

### Prevent save
If your app requires [integrated Save As controls](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations), you can control **Save As** functionality, as follows:

1. Set **Prevent 'Save As'** to **Yes**.
2. Confirm the following conditions:
    - Save is restricted to only appropriate managed locations.

### File Encryption
You can encrypt data on the device, as follows:

1. Set **Encrypt app data** to **Yes**.
2. Confirm the following conditions:
    - Normal application behavior isn't affected.

### Prevent Android Backups
You can control app backup, as follows:

1. If you have set [integrated backup restrictions](app-sdk-android.md#protecting-backup-data), set **Prevent Android backups** to **Yes**.
2. Confirm the following conditions:
    - Backups are restricted.

### Wipe
You can remotely wipe managed apps from containing corporate email and documents. Personal data is decrypted when it's no longer administered. Here's how:

1. From the Endpoint Manager admin center, [issue a wipe](../apps/apps-selective-wipe.md).
2. If your app doesn't register for any wipe handlers, confirm the following conditions:
    - A full wipe of the app occurs.
3. If your app has registered for `WIPE_USER_DATA` or `WIPE_USER_AUXILARY_DATA`, confirm the following conditions:
    - The managed content is removed from the app. For more information, see [Intune App SDK for Android developer guide - Selective Wipe](app-sdk-android.md#selective-wipe).

### Multi-Identity support
Integrating [multi-identity support](app-sdk-android.md#multi-identity-optional) 
is a high risk change that needs to be thoroughly tested. The most common issues occur because
of improperly setting the active identity (`Context` vs. thread level) or improperly tracking file
identities (`MAMFileProtectionManager`).

Minimally, confirm that:

- **Save As** policy is working correctly for managed identities.
- Copy and paste restrictions are correctly enforced from managed to personal.
- Only data belonging to the managed identity is encrypted, and personal files are not modified.
- Selective wipe during unenrollment only removes the managed identity data.
- The end user is prompted for conditional launch when changing from an unmanaged to a managed account (first time only).

### App configuration (optional)
You can configure behavior of managed apps. If your app consumes any app configuration settings, you should test that your app correctly handles all values that you (as the admin) can set. You can create and assign [app configuration policies](../apps/app-configuration-policies-overview.md) in Intune.


