---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 12/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page: 

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**This article was last updated on the date listed under the title above.**

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
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## App management


### Android Enterprise system app support in work profiles<!-- 5291507  -->
You'll be able to deploy Android Enterprise system apps for Android Enterprise Work Profile devices. System apps are apps that do not appear in the Managed Google Play Store and come pre-installed on the device. Once a system app is deployed, you'll be unable to uninstall, hide, or otherwise remove the system app. Note that this feature is planned to be released on or near the 2101 release timeframe. For related information about system apps, see [Add Android Enterprise system apps to Microsoft Intune](../apps/apps-ae-system.md).

### New app categories to target app protection policies more easily<!-- 4802581  -->
We've improved the UX of Microsoft Endpoint Manager by creating categories of apps that you can use to more easily and quickly target app protection policies. These categories are **All public apps**, **Microsoft apps**, and **Core Microsoft apps**. After you have created the targeted app protection policy, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy. As new apps are supported, we'll dynamically update these categories to include those apps as appropriate, and your policies will be automatically apply to all apps in your selected category. If needed, you can continue to target policies for individual apps as well. For more information, see [How to create and assign app protection policies](../apps/app-protection-policies.md) and [Create and deploy Windows Information Protection (WIP) policy with Intune](../apps/windows-information-protection-policy-create.md).


<!-- ***********************************************-->
## Device configuration

### Use Cisco AnyConnect as a VPN connection type for Windows 10 and newer<!-- 2605377 idready-->
You'll be able to create VPN profiles using Cisco AnyConnect as a connection type (**Devices** > **Device configuration** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Cisco AnyConnect** for connection type) without needing to use custom profiles.

This policy configures the Cisco AnyConnect app available in the Microsoft store. It doesn't configure the Cisco AnyConnect desktop application.

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Windows 10 and newer
- Windows Holographic for Business
 
### Run Microsoft Edge version 87 and newer in single app kiosk mode on Windows 10 devices<!-- 8271248 idready-->
On Windows 10 and newer devices, you configure a device to run as a kiosk that runs one app, or runs many apps (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Kiosk** for profile). When you select single app mode, you can:

- Run Microsoft Edge version 87 and newer.
- Select **Add Microsoft Edge legacy browser** to run Microsoft Edge version 77 and older.

For more information on the settings you can configure in kiosk mode, see [Kiosk settings for Windows 10 and newer devices](../configuration/kiosk-settings-windows.md).

Applies to:
- Windows 10 and newer in single-app kiosk mode
 
<!-- ***********************************************-->
## Device enrollment

### Ending support for iOS 11<!--7327321 -->
After iOS 14 releases, Intune enrollment and the Company Portal app will support iOS versions 12 and later. Older versions won't be supported but will continue to receive policies.

### Ending support for macOS 10.12<!--7327326 -->
After macOS 11 releases, Intune enrollment and the Company Portal will support macOS versions 10.13 and later. Older versions won't be supported.

### Microsoft Endpoint Manager ending support for Android 5.x<!--9058248 idready-->
In a future update, Microsoft Endpoint Manager will stop supporting Android 5.x devices.


<!-- ***********************************************-->
## Device management

### Windows 10 Enterprise multi-session support (public preview)<!--8666391 -->
This support will give users a familiar Windows 10 experience while you get the cost advantages of multi-session and existing per-user M365 licensing. This upcoming support will let you:

- Host multiple concurrent user sessions using the  new Remote Desktop Session Host exclusive to Windows Virtual Desktop on Azure.
- Manage multi-session remote desktops with device-based configurations like a shared, user-less Windows 10 Enterprise client.
- Automatically enroll Hybrid Azure AD joined virtual machines in Intune and target them with OS scope policies and apps.
 
### Collect logs remote actions<!--2167272 idready -->
A new remote action, *Collect logs*, will let you collect the logs from corporate devices without interrupting or waiting for the end user. Collected logs will include MDM, Autopilot, event viewers, key, Configuration Manager client, networking, and other critical troubleshooting logs.

The new remote action will be located at [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **All devices** > choose a device > **Collect logs**.

<!-- ***********************************************-->
## Intune apps

 ### Win32 app download progress bar<!-- 5145837  -->
End users will see a progress bar in the Windows Company Portal while a Win32 app is being downloaded. This feature will help customer better understand the app installation progress.

### Update to Android Company Portal app icon<!-- 7114401  -->
We'll be updating the Android Company Portal app icon to create a more modern look and feel. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### End users can restart an app install from the Company Portal<!-- 652935  -->
Using the Company Portal, end users will be able to restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.

### Application icon update for iOS, macOS, and web Company Portal<!-- 7113985 -->
We'll be updating the app icon used by the Company Portal for iOS, macOS, and web. This new icon is currently used by the Company Portal for Windows. End users will see the new icon in their device's application launcher and home screen, in Apple's App Store, and experiences within the Company Portal apps.

### Company Portal website improved load performance<!-- 8765415 idready -->
To improve page load performance, app icons will load in batches. End users may see a placeholder icon for some of their applications when visiting the Company Portal website. The related icons will load shortly after. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) and [Manage apps from the Company Portal website](../user-help/manage-apps-cpweb.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   --> 
We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)
 
After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Organizational report focused on device configuration<!-- 8455708 idready --> 
We will be releasing a new **Device configuration** organizational report. This report will replace the existing **Assignment status** report found in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Monitor**. The **Device configuration** report will allow you to generate a list of profiles in the tenant that have devices in a state of success, error, conflict, or pending. You can use filters for the profile type, OS, and state. The returned results will provide search, sort, filter, pagination, and export capabilities. In addition to device configuration details, this report will provide resource access details, and new settings catalog profile details. For related information, see [Intune Reports](../fundamentals/reports.md).


<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->
When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).


### Export localized Intune report data using Graph APIs<!-- 8612346 -->
You'll be able to specify that the report data that you export from the Microsoft Endpoint Manager reporting export [API](../fundamentals/reports-export-graph-apis.md) can contain localized columns only, or localized and non-localized columns. The localized and non-localized columns option will be selected by default for most reports, which will prevent breaking changes. For more information about reports, see [Intune reports](../fundamentals/reports.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Role-based access permissions update for Microsoft Tunnel Gateway<!-- 8554762 -->
We’re adding a new permissions group that you’ll be able to add to custom roles to grant users permission to manage [Microsoft Tunnel Gateway](/protect/microsoft-tunnel-overview) configurations.  (**Tenant administration** > **Microsoft Tunnel Gateway**)
 
The new group will be scoped to only the Microsoft Tunnel Gateway, and will support the actions to create, read, update or modify, and delete, the Microsoft Tunnel Gateway.

<!-- ***********************************************-->
## Security

### Improved flow for conditional access on Surface Duo devices<!-- 7552043  -->
We’re streamlining the conditional access flow on Surface Duo devices. These changes happen automatically and won't require any configuration updates by administrators. (**Endpoint security** > **Conditional access**)

- We’re improving the redirection to the Company Portal app when access to a resource is blocked by conditional access. Instead of being sent to the Google Play store listing of the Company Portal app, users will be sent directly to the Company Portal app that’s preinstalled on their Duo device.
- For devices that are enrolled as personally-owned work profile, when a user tries to sign in to a personal version of an app using their work credentials, they will be sent to the work version of Company Portal where guidance messaging is shown. Currently, the user is sent to the Google Play store listing of the personal version of the Company Portal app, where they must reenable the personal Company Portal to see the guidance messaging.

### New setting for Attack surface reduction rules to block malware from gaining persistence through WMI<!-- 8902661  -->
We're adding a new setting to the Attack surface reduction rule profile, part of Attack surface reduction policy, to help prevent malware from abusing WMI to gain persistence on a device. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Attack surface reduction rule**)

This new setting can help protect against fileless malware threats that abuse the WMI repository and event model to stay hidden. For more information see [Block persistence through MI event subscription](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-persistence-through-wmi-event-subscription) in the Windows security documentation.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
