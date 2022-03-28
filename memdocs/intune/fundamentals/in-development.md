---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 03/31/2022
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

### Enterprise feedback policies for Web Company Portal<!-- 9846764 -->
Feedback settings will be provided to address M365 enterprise feedback policies for the currently logged in user via the Microsoft 365 Apps Admin Center. The settings are used to determine whether feedback can be enabled or must be disabled for a user in the Web Company Portal.

### iOS Company Portal minimum required version<!-- 13016075 -->
With an upcoming release of the MS Authenticator app, users will be required to update to v5.2204 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

### Improvements to Win32 App Log collection<!-- 9978316 -->
Win32 App Log collection via Intune Management Extension has moved to the Windows 10 device diagnostic platform, reducing time to collect logs from 1-2 hours to 20 minutes.  We've also increased the size from 60mb to 250mb.  Along with performance improvements, the app logs will also be available under the **Device diagnostics monitor** action for each device, as well as the managed app monitor. For information about how to collect diagnostics, see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md) and [Troubleshooting Win32 app installations with Intune](/troubleshoot/mem/intune/troubleshoot-win32-app-install).

### Uninstall DMG-type applications on managed macOS devices (Public preview)<!-- 13155022 -->
You will be able to use the Uninstall assignment type to remove DMG-type applications on managed macOS devices from Microsoft Endpoint Manager. You can find macOS DMG apps in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **macOS app (.DMG)**. For related information, [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

### Update to the App configuration policies list<!-- 13903969 -->
In Intune, the **Assigned** column in the **App configuration policies** list will be removed. To view the assigned groups for an app configuration policy, navigate to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **App configuration policies** > *select a policy* > **Overview**.

<!-- ***********************************************-->

## Device enrollment

### Improvements for enrollment profiles for Apple’s Automated Device Enrollment (Public preview)<!-- 10111795 -->
As a public preview, we’re adding new Setup Assistant screens you can configure when [creating enrollment profiles](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) for Apple’s Automated Device Enrollment (ADE). The following new screens will be available on the *Setup Assistant* tab for both iOS/iPadOS and macOS as follows:  
 
- iOS/iPadOS 13 and later - **Get Started (preview)**
  - Default – Show
  - Admin can configure to hide the Get Started pane (Setup Assistant screen) during ADE enrollment.
 
- macOS 12 and later - **Auto Unlock with Apple Watch (preview)**
  - Default – Show
  - Admin can configure to hide the Unlock Your Mac with your Apple Watch pane (Setup Assistant screen) during ADE enrollment.

<!-- ***********************************************-->

## Device management

### Updating the device diagnostics folder structure<!-- 8504019 -->
We’re updating how Intune exports [Windows Device Diagnostic data](../remote-actions/collect-diagnostics.md). Today, the zip file is flat structure of numbered folders that doesn’t identify their contents. Once updated, the logs collected will be named to match the data that was collected, and if multiple files are collected a folder will be created.

To take advantage of this diagnostic logging update, devices must install one of the following updates:
- Windows 11 - KB5011563
- Windows 10 - KB5011543

These updates are expected to be made available through Windows Updates on April 12, 2022.

<!-- ***********************************************-->

## Device configuration

### New wired networks device configuration profile for Windows devices<!-- 1746923 -->
There will be a new **Wired Networks** device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

Use this profile to configure common wired network settings, including authentication, EAP type, server trust, and more.

Applies to:
- Windows 11
- Windows 10

### Import custom ADMX and ADML administrative templates to create a device configuration profile that you can assign and manage<!-- 4970862 -->
You can create a device configuration policy that uses built-in ADMX templates (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative templates**).

You'll be able to import custom and 3rd party/partner ADMX and ADML templates into the Endpoint Manager admin center. Once imported, you can create a device configuration policy, assign the policy to your devices, and manage the settings in the policy.

For information on the built-in ADMX templates, see [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:
- Windows 11
- Windows 10

### Create a Settings Catalog policy using your imported GPOs with Group Policy analytics (public preview)<!-- 6379751 -->
Using Group Policy analytics, you can import your on-premises GPO, and see the settings that are supported in Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers.

When the analysis runs, you'll see the settings that are ready for migration. There will be a **Migrate** option (public preview) that creates a Settings Catalog profile using these settings. Then, you can assign the profile to your groups.

For more information on what you can do now, see [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager](../configuration/group-policy-analytics.md).

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

## Device security

### Microsoft Defender for Endpoint as the Tunnel client app for iOS will soon be out of Preview<!-- 9849514 --> 
The preview version of Microsoft Defender for Endpoint that supports [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md) on iOS/iPadOS will soon be out of preview and become generally available.

When the Microsoft Defender for Endpoint app with support for Microsoft Tunnel becomes generally available for iOS, the standalone tunnel client app for iOS will be deprecated with support ending 60 days later.

If you are using the standalone tunnel app for iOS, prepare for this change by planning to [migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md) before support for the standalone app ends.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
