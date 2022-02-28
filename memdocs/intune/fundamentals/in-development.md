---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 03/03/2022
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

### iOS Company Portal minimum required version<!-- 13016075 -->
With an upcoming release of the MS Authenticator app, users will be required to update to v5.2204 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

### Improvements to Win32 App Log collection<!-- 9978316 -->
Win32 App Log collection via Intune Management Extension has moved to the Windows 10 device diagnostic platform, reducing time to collect logs from 1-2 hours to 20 minutes.  We've also increased the size from 60mb to 250mb.  Along with performance improvements, the app logs will also be available under the **Device diagnostics monitor** action for each device, as well as the managed app monitor. For information about how to collect diagnostics, see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md) and [Troubleshooting Win32 app installations with Intune](/troubleshoot/mem/intune/troubleshoot-win32-app-install).

### Feedback settings for Company Portal and Microsoft Intune apps<!-- 10012370 -->
Feedback settings will be provided to address M365 enterprise feedback policies for the currently logged in user via the Microsoft 365 Apps admin center. The settings are used to determine whether feedback can be enabled or must be disabled for a user. The feature will be available for Intune Company Portal and Microsoft Intune apps.

### Apps UI when using Android 12L OS<!-- 12536901 -->
The Android 12L OS contains new features designed to improve the Android 12 experience on large and folding dual-screen devices. Intune apps will support Android 12L when the update is released to devices.

### Uninstall DMG-type applications on managed macOS devices<!-- 13155022 -->
You will be able to use the **Uninstall** assignment type to remove DMG-type applications on managed macOS devices from Microsoft Endpoint Manager. You can find macOS DMG apps in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS**. For related information, [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

### Deploy macOS LOB apps by uploading PKG-type installer files (Public preview)<!-- 13155147 -->
You will be able to upload and deploy PKG-type installer files as macOS line-of-business apps. You can add a macOS LOB app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **Add** > **Line-of-business app**. For more information about macOS LOB apps, see [How to add macOS line-of-business apps to Microsoft Intune](../apps/lob-apps-macos.md).

<!-- ***********************************************-->

## Device management

### Android (AOSP) users can view all devices in Intune app<!-- 10454654 -->
AOSP device users will be able to view a list of their managed devices and device properties in the Microsoft Intune app. This feature will be available on devices enrolled in Intune as user-associated (Android) AOSP devices.

### New reporting experience for device configuration profiles<!-- 8466004 -->
You can now expect a new reporting experience for device configuration profiles. This reporting experience excludes ADMX, OEM Config, DFCI profile types.

We are continuing to update Intune's report experience to enhance consistency, accuracy, organization, and data representation, which will give an overall "facelift" of Intune's per policy reporting. The new experience will update the per policy overview page to shift away from donut charts to a sleeker overview chart that quickly updates as devices/users check in. There are three reports available from the per policy view:

- **Device and user check in status** - This report shows the full list of devices and users that have checked into using the policy and also provides the related status.
- **Device assignment status** - This new report shows the list of devices and the last logged on user of the device to provide the latest device status. This report includes devices in a pending state and provides the denominator of total assigned devices and assigned users.
- **Per setting status** - This report shows the state of the aggregate of devices/users that have checked in per setting. The states include error, conflict, and success.

More drilldowns are available and additional assignment filters are supported. For related information about reporting, see [Intune reports](../fundamentals/reports.md).

### See the IPv4 address and Wi-Fi subnet ID on Andriod Enterprise devices<!-- 12396463 -->
Customers will now have the ability to see IPv4 address and Wi-Fi subnet ID reported for AE corporate-owned fully managed, dedicated, and work profile devices.

<!-- ***********************************************-->

## Device configuration

### Endpoint security profiles support filters; See the filter status on a device configuration profile report<!-- 11889620 -->
There are some new features when using filters:
- When you create a device configuration profile for Windows devices, a per-policy report will show reporting information in the **Device and user check-in status** (**Devices** > **Configuration profiles** > Select an existing policy).

  When you select **View report**, the report has an **Assignment Filter** column. Use this column to determine if a filter successfully applied to your policy.

- Endpoint Security policies will support filters. So, when you assign an endpoint security policy, you can use filters to assign the policy based on rules you create. 
- When you create a new endpoint security policy, it will automatically use the [new device configuration profile reporting](ErikRe: Add shortcut to https://msazure.visualstudio.com/Intune/_workitems/edit/8466004 header). When you look at the per-policy report, it also has an **Assignment Filter** column (**Devices** > **Configuration profiles** > Select an existing endpoint security policy > **View report**). Use this column to determine if a filter successfully applied to your policy.

For more information on filters, see:
- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [List of platforms, policies, and app types supported by filters](filters-supported-workloads.md)

Applies to:
- All platforms

Does not apply to:
- Administrative Templates (Windows 10/11)
- Device Firmware Configuration Interface (DFCI) (Windows 10/11)
- OEMConfig (Android Enterprise)

### New wired networks device configuration profile for Windows devices<!-- 1746923 -->
There will be a new **Wired Networks** device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

Use this profile to configure common wired network settings, including authentication, EAP type, server trust, and more.

Applies to:
- Windows 11
- Windows 10

### Use the Settings Catalog to create a Universal Print policy on Windows 11 devices<!-- 5513123 -->
Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution for Microsoft 365 customers. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure. When Universal Print is deployed with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. 

In the Endpoint Manager admin center, you'll be able to use the Settings Catalog to create a printer policy (**Device configuration** > **Create profile** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Printer provisioning**). When you deploy the policy, users select the printer from a list of registered Universal Print printers, and can also select a default printer.

Currently, you must use the [Universal Print printer provisioning tool](/universal-print/fundamentals/universal-print-intune-tool), which requires more manual steps, and has some limitations.

Applies to:
- Windows 11

<!-- ***********************************************-->

## Monitor and troubleshoot

### AppxPackaging event viewer is part of collect diagnostics<!-- 12809781 --> 
 Intune's remote action to [Collect diagnostics](../remote-actions/collect-diagnostics.md) will soon collect additional details from Windows devices.  (**Devices** > **Windows** > *select a Windows device* > **Collect diagnostics**) 
 
The new details include the **Microsoft-Windows-AppxPackaging/Operational** Event Viewer and the following office log files to assist in troubleshooting office installation issues:
`%windir%\temp\%computername%*.log`
`%windir%\temp\officeclicktorun*.log`

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
