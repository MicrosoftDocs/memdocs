---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 12/13/2021
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

### Device compliance status on the Company Portal website<!-- 8782968 -->
Users will be able to more easily see the compliance status of their devices from the [Company Portal](https://portal.manage.microsoft.com/devices) website. Users can go to the Company Portal website and select the **Devices** page to see device status. Devices will be listed with a status of **Can access company resources**, **Checking access**, or **Can't access company resources**. 

For related information, see [Manage apps from the Company Portal website](../user-help/manage-apps-cpweb.md) and [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to warn, wipe data, or block the user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

<!-- ***********************************************-->

## Device security

### BlackBerry Cylance: New Mobile Threat Defense partner<!-- 7822722  IDready -->
You'll soon be able to use [BlackBerry's Cylance AI](https://www.blackberry.com/us/en/products/unified-endpoint-security/cylance-ai) offering as an integrated Mobile Threat Defense (MTD) partner. Intune will help you control mobile device access to corporate resources by offering Conditional Access based on risk assessment.

For more information about MTD partners for Intune, see [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md).

<!-- ***********************************************-->

## Device configuration

### New option to see the number of profiles with an error or conflict in device configuration profiles<!-- 9142810 -->
In the Endpoint Manager admin center, there's a new option that states something like "X policies with error or conflict." When you select this option, you automatically go to the **Devices** > **Monitor** > **Assignment Failures** report. This report helps you troubleshoot errors and conflicts.

This new option is available in the following locations in the Endpoint Manager admin center:
- Home page
- Dashboard

For more information, see [Monitor device profiles in Microsoft Intune](../configuration/device-profile-monitor.md) and [Assignment failures report](reports.md#assignment-failures-report-operational).

Applies to:
- Windows 10 and later

### New Timeout and Block iCloud Private Relay settings for iOS/iPadOS and macOS devices<!-- 10370284 -->
On iOS/iPadOS and macOS devices, you can create a device restrictions policy that manages features on the device (**Devices** > **Configuration Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Device restrictions**).

There are new settings:
- iOS/iPadOS:
  - **Block iCloud Private Relay**: On supervised devices, this setting prevents users from using the [iCloud Private Relay](https://support.apple.com/HT212614) (opens Apple's website).
- macOS:
  - **Block iCloud Private Relay**: On supervised devices, this setting prevents users from using the [iCloud Private Relay](https://support.apple.com/HT212614) (opens Apple's website).
  - **Timeout**: Users can unlock their devices by using a touch ID, such as a fingerprint. Use this setting to require users to enter their password after a period of inactivity. The default inactivity period is 48 hours. After 48 hours of inactivity, the device prompts for the password instead of a touch ID.

Applies to:
- iOS/iPadOS 15 and later
- macOS 12 and later

### New device restriction settings for Android Enterprise corporate-owned devices with a work profile<!-- 10982232 -->
On Android Enterprise devices, you can configure settings that control features on devices (**Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Device restrictions** for profile type).

For Android Enterprise corporate-owned devices with a work profile, there are new settings:
- Restrict searching work contacts and displaying caller ID for work contacts in a personal profile
- Restrict copy and paste between work and personal profiles
- Restrict data sharing between work and personal profiles

For more information on the settings that you can currently configure, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise corporate-owned work profile (COPE)

### Settings catalog will soon be supported on US Government GCC High and DoD<!-- 12389409 -->
The settings catalog will soon be available and supported on US Government GCC High and DoD.

For more information on the settings catalog, see [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md).

Applies to:
- macOS
- Windows 10 and later

### Entry of the certificate common name in Wi-Fi profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile devices<!-- 12439458  -->
On Android Enterprise devices, you can create a Wi-Fi profile that configures enterprise Wi-Fi settings (**Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

When you select **Enterprise**, there's a new **Server names** setting. This setting is the DNS name used in the certificate that the RADIUS server presents during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

If you have multiple RADIUS servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

When you enter this value, user devices can bypass the dynamic trust dialog that sometimes appears when a device is connecting to the Wi-Fi network. 

New Wi-Fi profiles that target Android 11 or later might require this setting to be configured. Otherwise, the devices might not connect to your Wi-Fi network.

For more information on the settings that you can currently configure, see [Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile settings](../configuration/wi-fi-settings-android-enterprise.md#fully-managed-dedicated-and-corporate-owned-work-profile).

Applies to:
- Android Enterprise corporate-owned work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise dedicated devices (COSU)

### New Administrative Templates settings for Microsoft Edge 96 and Microsoft Edge updater on Windows devices<!-- 12442597 -->
In Intune, you can use **Administrative Templates** to configure Microsoft Edge settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative Templates** for profile type).

There are new **Administrative Templates** settings for Microsoft Edge 96 and the Microsoft Edge updater, including **Target Channel override** support. Use **Target Channel override** so users get the **Extended Stable** release cycle option. You can set this option by using Group Policy or Intune.

For related information, see:
- [Configure Microsoft Edge policy settings in Microsoft Intune](../configuration/administrative-templates-configure-edge.md)
- [Overview of the Microsoft Edge channels](/deployedge/microsoft-edge-channels)
- [Microsoft Edge browser policy documentation](/deployedge/microsoft-edge-policies)

Applies to:
- Windows 10 and later
- Microsoft Edge

### Use filters to assign proactive remediation scripts for endpoint analytics and to assign endpoint security policies in the Endpoint Manager admin center (public preview)<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Windows PowerShell scripts for proactive remediations in endpoint analytics](../../analytics/proactive-remediations.md) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint security policies](../protect/endpoint-security-policy.md), such as account protection, antivirus, and attack surface reduction

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS
- Windows 10 and later

<!-- ***********************************************-->
## Device enrollment

### Use filters on Windows Enrollment Status Page profile assignments<!-- 7423484  -->

Filters allow you to include or exclude devices in policy or app assignments based on device properties. After you create an Enrollment Status Page (ESP) profile, you'll be able to use filters when assigning the profile. The **All users** and **All devices** assignment options will also be available. 

You'll be able to find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Enroll devices** > **Enrollment Status Page** > **Create**. For more information about filters, see [Use filters when assigning your apps, policies, and profiles](../fundamentals/filters.md). For more information about ESP profiles, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).   

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot  

### Changes to the account protection policy in endpoint security<!--  7492116   -->

We're reworking the account protection policy in endpoint security to use the new API for Windows Hello for Business. The new API will result in a more consistent experience. 

The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts. This API replaces *./User/Vendor/MSFT/PassportForWork*  (**Endpoint security** > **Account protection**).

After the change, only new policies that you create will use the new API. Your existing policies won't be affected by this change and will continue to use the older API.

<!-- ***********************************************
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Intune Data Warehouse updates<!-- 9370034 -->

The `applicationInventory` entity will be removed from the Intune Data Warehouse in an upcoming Intune service release. We're introducing a more complete and accurate dataset that will be available in the UI and via an export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
<!--## Security-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
