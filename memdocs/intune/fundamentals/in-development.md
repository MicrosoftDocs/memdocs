---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 02/01/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->

## App management

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

<!-- ***********************************************-->

## Device configuration

### On Android Enterprise, use the Connect Automatically setting on enterprise Wi-Fi profiles<!-- 10697036 -->

On Android Enterprise devices, you can create Wi-Fi profiles that include common enterprise Wi-Fi settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned work profile** > **Wi-Fi** for profile type > **Enterprise** for Wi-Fi type).

You can configure the **Connect automatically** setting that automatically connects to your Wi-Fi network when devices are in range.

To see the settings you can currently configure, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:

- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

### New macOS settings in the Settings Catalog<!-- 12987685 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. When you create a Settings Catalog policy, there are new settings available for macOS devices (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog (preview)** for profile type).

New settings include:

- Accounts > Caldav:
  - Cal DAV Account Description
  - Cal DAV Host Name
  - Cal DAV Password
  - Cal DAV Port
  - Cal DAV Principal URL
  - Cal DAV Username
  - Cal DAV Use SSL

- Accounts > Carddav:
  - Card DAV Account Description
  - Card DAV Host Name
  - Card DAV Password
  - Card DAV Port
  - Card DAV Principal URL
  - Card DAV Username
  - Card DAV Use SSL

- Networking > Domains > Email Domains

- Printing > Printing:
  - Allow Local Printers
  - Default Printer
    - Device URI
    - Display Name
  - Footer Font Name
  - Footer Font Size
  - Print Footer
  - Print MAC Address
  - Require Admin To Add Printers
  - Require Admin To Print Locally
  - Show Only Managed Printers
  - User Printer List
    - Device URI
    - Display Name
    - Location
    - Model
    - PPD URL
    - Printer Locked

- Profile Removal Password > Removal Password

- Proxies > Global HTTP Proxy:
  - Proxy Captive Login Allowed
  - Proxy PAC Fallback Allowed
  - Proxy PAC URL
  - Proxy Password
  - Proxy Server
  - Proxy Server Port
  - Proxy Type
  - Proxy Username

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

<!-- ***********************************************-->

## Device enrollment

### Enforce Azure AD terms of use with Microsoft Intune or Microsoft Intune Enrollment cloud apps<!-- 12522105 -->
Use the Microsoft Intune cloud app or Microsoft Intune Enrollment cloud app to enforce a conditional access, Azure AD Terms of Use policy on iOS and iPadOS devices during automated device enrollment.  Both apps will ensure that users accept the terms of use before enrolling if required by your conditional access policy. This functionality will be available when you select Setup Assistant with modern authentication as the authentication method.  

<!-- ***********************************************-->

## Device management

### Create terms of use for Android (AOSP) user-associated devices<!-- 8506575 -->
Require Android (AOSP) users to accept your organization's terms and conditions before using the Intune Company Portal app. This feature will be available for corporate-owned, user-associated devices only. For more information about creating terms of use in Intune, see [Terms and conditions for user access](../enrollment/terms-and-conditions-create.md).

<!-- ***********************************************-->

## Device security

### Manage the app inventory data for iOS/iPadOS devices that Intune sends to third-party MTD partners<!-- 10722315 -->

You’ll soon have more control over the application inventory data for personally-owned iOS/iPadOS devices that Intune sends to your chosen third-party Mobile Threat Defense (MTD) partner. You’ll configure what data is sent with a new setting that’s available when you configure the [Mobile Threat Defense connector](../protect/mtd-connector-enable.md#to-enable-the-mobile-threat-defense-connector). The new setting is **Send full application inventory data on personally-owned iOS/iPadOS Devices**.

For personally-owned iOS/iPadOS devices:

- When set to **On**: If your MTD partner syncs app data and requests a list of the iOS/iPadOS applications from Intune, that list includes unmanage apps (those not deployed through Intune) in addition to those deployed through Intune.  This is the current behavior.
- When set to **Off**: Data on unmanaged apps won’t be provided, and the MTD partner only receives details about apps that were deployed through Intune.

For corporate devices, data about managed and unmanaged apps continues to be included with requests for app data by your MTD vendor.  


<!-- ***********************************************-->

## Scripting

### Intune Data Warehouse updates<!-- 9370034 -->

The `applicationInventory` entity will be removed from the Intune Data Warehouse in an upcoming Intune service release. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
<!--## Security-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
