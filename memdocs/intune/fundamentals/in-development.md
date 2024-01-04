---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 01/05/2024
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
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## App management  

### End-user app PIN reset<!-- 24605159   -->  
For managed apps that require a PIN to access, allowed end-users will be able to reset the app PIN at any time. You can require an app PIN in Intune by selecting the **PIN for access** setting in iOS/iPadOS and Android app protection policies. For more information about app protection policies, see [App protection policies overview](../apps/app-protection-policy.md).

#### Intune support of store-signed LOB apps for Surface Hub devices<!-- 25865620  -->  
Intune will support the deployment of store-signed LOB apps (single file *.appx*, *.msix*, *.appxbundle*, and *.msixbundle*) to Surface Hub devices. The support for store-signed LOB apps will enable offline store apps to be deployed to Surface Hub devices following the retirement of the Microsoft Store for Business.

### Route SMS/MMS messages to specific app<!-- 24594466  -->  
You will be able to configure an app protection policy to determine which SMS/MMS app must be used when the end-user intends to send a SMS/MMS message after getting redirected from a policy managed app. When the end-user clicks on a number with the intent of sending an SMS/MMS message, the app protection settings are used to redirect to the configured SMS/MMS app. This capability applies to both Android and iOS/iPadOS platforms.

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Enterprise application management<!-- 10986080  -->  
Enterprise Application Management provides a catalog of prepackaged applications designed to simplify discovery, delivery, and updates for third and first party apps. Enterprise Application Management will be generally available in early Q1 2024.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!-- 17016690  -->  
You'll be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:

- **iOS/iPadOS**

<!-- *********************************************** -->

## Device configuration

### Import up to 20 custom ADMX and ADML administrative templates<!-- 25780608  -->  
You can import custom ADMX and ADML administrative templates in Microsoft Intune. Currently, you can import up to 10 files.

You'll be able to upload 20 files.

For more information on this feature, go to [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../configuration/administrative-templates-import-custom.md).

Applies to:

- Windows 10/11

### New setting that disables location on Android Enterprise devices<!-- 21060837  -->  

On Android Enterprise devices, there's a new setting that allows admins to control the location (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device Restrictions** for profile type > **General**):

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

For more information on the settings you can currently configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise

### The macOS Company Portal app will support platform SSO (public preview)<!-- 24325427  -->  
In Intune, you can configure the Enterprise single sign-on (SSO) plug-in on Apple devices using a device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates > Device features** for profile > **Single sign-on app extension**).

The Company Portal app version will support the platform SSO settings for macOS 13 and later. Platform SSO allows you to sync your Microsoft Entra ID password to local accounts on Macs using the Enterprise Single Sign-On extension.

For more information on the Enterprise SSO plug-in, go to:

- [Use Intune to deploy the Microsoft Enterprise SSO plug-in for Apple devices](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
- [Entra ID and the Microsoft Enterprise SSO plug-in overview for Apple devices](/azure/active-directory/develop/apple-sso-plugin)

Applies to:

- macOS 13 and later

### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705   -->  
You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information about assignment filters, go to [Use filters when assigning your apps, policies, and profiles in Intune](filters.md).

Applies to:

- Windows 10/11

<!-- *********************************************** -->

## Device enrollment

### RBAC changes coming to enrollment settings for Windows Hello for Business<!-- 25661866   -->  
We're updating RBAC in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business will be read-only for all roles except the Intune Service Administrator. The Intune Service Administrator will be able to edit enrollment settings.



<!-- *********************************************** -->

## Device management

#### Improvements to new device experience in admin center (public preview) <!-- 23692982   -->  
After hearing your feedback, we're rearranging the tabs in the new Devices experience so that you can focus on management first, and monitoring second. When you select a workload, instead of landing on the **Monitor** tab, which is the current default experience in public preview, you will land on the primary management tab, such as **Policies** or **Update rings**.  Monitoring will still be available but will change from being the first tab in the list to the last.


### Introducing a remote action to pause the config refresh enforcement interval<!--24249019  -->  
In the Windows Settings Catalog you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check-in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action will be added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings will be enforced again.

The remote action **Pause config refresh** can be accessed from the device summary page.

For information on currently available Remote actions, see [Remote actions](../remote-actions/device-management.md).

<!-- *********************************************** -->

## Device security

### HTML formatting supported in noncompliance email notifications <!-- 24197255   -->  
HTML formatting will be supported in noncompliance email notifications for all platforms. You'll be able to use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

### Support for Intune Device control and Defender Update control policies for devices managed by Microsoft Defender for Endpoint<!-- 25470154, 15466620 -->  
You’ll soon be able to use the Device control and Defender Update control profiles from the Microsoft Intune admin center with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** profiles are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

  Applies to:
  - Windows 10/11

- **Defender Update control** profiles are part of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md).

  Apples to:
  - Linux
  - macOS
  - Windows 10/11

Prepare for January 2024. This policy change is expected to be released with the January 2024 service update for Intune. When this change takes effect, devices that are managed by Defender for Endpoint but not enrolled with Intune, and that are assigned to either kind of profile, will start applying the settings from those profiles. Check your profiles to make sure only the devices you intend to receive these policies will get them.

<!-- *********************************************** -->

## Monitor and troubleshoot

### Exported report data maintains search results<!-- 17723620  -->  
Intune will maintain your report search results when exporting report data. For example, when you use the [Noncompliant devices and settings](../fundamentals/reports.md#noncompliant-devices-and-settings-report-organizational) report, set the OS filter to "Windows", and search for "PC", the exported data will only contain Windows devices with "PC" in their name. This capability will also be available when calling the ExportJobs API directly.

### Battery report<!-- 9747162 -->  
We're working on a battery health report to provide visibility into the health of batteries in your organization’s devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

The battery health report is a part of the advanced analytics features and will be included as an Intune-add on under [Microsoft Intune Suite](../fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Intune.

### Monitoring reports for devices<!-- 17744651 -->  
In Intune, you will be able to view a new list of all device monitoring reports. You will be able to find these reports in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**. The **Monitor** pane will provide reports related to configuration, compliance, enrollment, and software updates. Additionally, there will be other reports that you can view, such as **Device actions**.

### Run on-demand pivot queries on single devices<!--16719466  -->  
Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device Intune will run a query in real time. The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

Applies to:

- Windows devices

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
