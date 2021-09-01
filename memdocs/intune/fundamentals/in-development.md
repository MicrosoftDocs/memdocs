---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 9/1/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid:

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
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for more updates.
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
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->
## App management

### Export underlying discovered apps list data<!-- 9370255  -->

In addition to exporting the summarized discovered apps list data, you'll also be able export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the new experience will also provide the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data will be a list of every device and each app discovered for that device. This functionality is being added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset, which will be removed in an upcoming Intune service release. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Maximum OS version setting for app conditional launch<!-- 9493137  -->

Using iOS app protection policies in Microsoft Intune app protection policies, you'll be able to add a new conditional launch setting to ensure end users are not using a pre-release or beta OS build to access work or school account data. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you'll be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

### Unified delivery of Azure AD Enterprise and Office Online applications in the Android Company Portal<!-- 1817862  -->

Last year, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal website](../fundamentals/whats-new-archive.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal). This feature will be supported for users who get their apps directly from the Android Company Portal. On the **Customization** pane of Intune, select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Company Portal. Each end user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### New app categories available to better target app protection policies<!-- 4802581  -->

We have improved the UX of Microsoft Endpoint Manager by creating categories of apps that you can use to more easily and quickly target app protection policies. These categories are **All public apps**, **Microsoft apps**, and **Core Microsoft apps**. After you have created the targeted app protection policy, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy. As new apps are supported, we will dynamically update these categories to include those apps as appropriate, and your policies will be automatically applied to all apps in your selected category. If needed, you can continue to target policies for individual apps as well. For more information, see [How to create and assign app protection policies](../apps/app-protection-policies.md) and [Create and deploy Windows Information Protection (WIP) policy with Intune](../apps/windows-information-protection-policy-create.md).

<!-- ***********************************************-->
## Device configuration

### Use a Settings Catalog policy in a policy set for Windows and macOS devices<!-- 8851701  -->

In Intune, you can create a policy using [Settings Catalog](../configuration/settings-catalog.md), which lists all the settings you can configure. Now, you can use the Settings Catalog policy within a policy set.

For more information, see [Use policy sets to group collections of management objects](policy-sets.md).

Applies to:

- macOS
- Windows 10 and newer

### Settings catalog policies for policy sets<!-- 8683467  -->

In addition to profiles based on templates, you'll be able to add a profiles based on the **Settings catalog** to your policy sets. The **Settings catalog** is a list of all the settings you can configure. To create a policy set in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Policy sets** > **Policy sets** > **Create**. For more information, see [Use policy sets to group collections of management objects](../fundamentals/policy-sets.md) and [Use the settings catalog to configure settings on Windows and macOS devices - preview](../configuration/settings-catalog.md).

### Use filters on DFCI configuration profiles on Windows 10 RS5 (1809) and newer devices<!-- 8817773  -->

In Endpoint Manager, you can create filters to target devices based on different properties. When you create a Device Firmware Configuration Interface (DFCI) profile, you'll be able to use filters when assigning the profile.

- For more information about filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).
- For more information about the DFCI profile, see [Use Device Firmware Configuration Interface profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:

- Windows 10 RS5 (1809) and newer on supported UEFI

### Use filters to assign Endpoint analytics proactive remediations scripts and Endpoint Security policies in Endpoint Manager admin center - public preview<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Endpoint analytics proactive remediations Windows PowerShell scripts](../../analytics/proactive-remediations.md) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint Security policies](../protect/endpoint-security-policy.md), including Account protection, Antivirus, Attack surface reduction, and more.

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS
- Windows 10 and newer

### Manage Windows 10 security updates for Windows 10 Enterprise multi-session VMs<!-- 8682461  -->

You’ll soon be able to use the Settings Catalog to deploy Windows 10 quality updates to Windows 10 Enterprise multi-session virtual machines. (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 or later** > **Settings catalog**)

To find the relevant settings, in the Settings Catalog, [use the Settings filter to focus on the OS type of Enterprise multi-session](../fundamentals/azure-virtual-desktop-multi-session.md#to-configure-policies). Then select the Windows Update for Business category where you’ll now see only those settings that are supported for multi-session VMs.

The Windows Update settings for quality updates that you’ll soon be able to use with multi-session VMs include:

- Active Hours End
- Active Hours Max Range
- Active Hours Start
- Block "Pause Updates" ability
- Configure Deadline Grace Period
- Defer Quality Updates Period (Days)
- Pause Quality Updates Start Time
- Quality Update Deadline Period (Days)

<!-- ***********************************************-->
## Device enrollment

### Four new Shared iPad enrollment settings<!--9684925 -->

Four new settings will be available for Shared iPad devices. These settings get applied at the time of Automated Device Enrollment.

- For iPadOS 14.5 and later in Shared iPad mode:
  - Require Shared iPad temporary setting only: When set to Yes, users only see the Guest Welcome pane, and can only sign in as a guest user. Users can't sign in with a Managed Apple ID.
  - Maximum seconds of inactivity until temporary session logs out: If there isn't any activity after the value you enter, then the temporary session automatically signs out.
  - Maximum seconds of inactivity until user session logs out: If there isn't any activity after the value you enter, then the user session automatically signs out.
- For iPadOS 13.0 and later in Shared iPad mode:
  - Maximum seconds after screen lock before password is required for Shared iPad.

### New device restrictions setting prevents sharing work profile contacts with paired Bluetooth devices  <!-- 8630136  -->

A new device restrictions setting for corporate-owned work profile devices will prevent users from sharing their work profile contacts with paired Bluetooth devices, such as cars or mobile devices.  The new setting will be available in **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device restrictions** for profile.  

- Setting name:  **Contact sharing via Bluetooth (work profile-level)**
- Setting toggles:  
- **Block**: Blocks users from sharing work profile contacts via Bluetooth.
- **Not configured**:  Doesn't enforce any restrictions on the device, so users might be able to share their work profile contacts via Bluetooth.

<!-- ***********************************************-->
## Device management

### Tenant attach: Offboarding <!--9412904 -->

While we know customers get enormous value by enabling tenant attach with Configuration Manager, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard from the cloud following a disaster recovery scenario where the on-premises environment was removed. You'll soon be able to offboard a Configuration Manager environment from the Microsoft Endpoint Manager admin center.

### Intune moving to support iOS/iPadOS 13 and higher later this year<!-- 9964998 idrady-->

Later this year, Apple is expected to release iOS 15. Microsoft Intune, including the Intune Company Portal and Intune app protection policies will require [iOS/iPadOS 13 and higher](supported-devices-browsers.md) shortly after the release of iOS 15.

### Intune moving to support  macOS 10.15 and later with the release of macOS 12<!-- 10154527 -->

Apple is expected to release macOS 12 (Monterey) in the fall of 2021. Microsoft Intune, including the Company Portal and Intune MDM agent, will require macOS 10.15 (Catalina) and later shortly after the release of macOS 12.

### New Android device filtering options<!--7479654 -->

You'll be able to choose the following Android enrollment types when filtering by OS in the **All devices** list in Intune:

- Android (personally-owned work profile)
- Android (corporate-owned work profile)
- Android (fully managed)
- Android (dedicated)
- Android (device administrator)

### Support for Locate device remote action on Android Enterprise dedicated devices<!--8589952 -->

You'll be able to use the **Locate device** remote action to get the current location of a lost or stolen Android Enterprise dedicated device that is online. For an offline device, you can get the last known location (for a limited time). For more information, see [Locate lost or stolen devices](../remote-actions/device-locate.md).

### Android Enterprise dedicated devices will support the Rename remote action<!--8590028 -->

You'll be able to use the Rename remote action on Android Enterprise dedicated devices. You can rename devices individually and in bulk. When using bulk Rename actions, you must include either a random number or the device's serial number.

### New device restriction setting for Android Enterprise: Developer settings<!--10510385 -->

A new Android Enterprise device restriction setting will be available: Developer settings. When set to **Allow**, the setting lets users access developer settings on the device. By default, it's set to **Not configured**.

### New iOS device restriction settings for connected devices, doc viewing  <!--10119553 -->

There will be two new device restriction settings you can configure on iOS devices (**Devices** > **iOS/iPadOS** > **Configuration profiles** > **Create profile**  and select **Device restrictions** for profile) in Intune.  

- **Block Siri for translation** (Connected devices): Disables the connection to Siri servers so that users can't use Siri to translate text. Applies to iOS and iPadOS versions 15 and later.  
- **Allow copy/paste to be affected by managed open-in** (App Store, Doc Viewing, Gaming): Enforces copy/paste restrictions based on how you configured **Block viewing corporate documents in unmanaged apps**  and **Block viewing non-corporate documents in corporate apps**.

For more information about iOS device restriction profiles in Intune, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

### New macOS device restriction setting blocks users from erasing all content and settings on device<!--10131859 -->

When creating a device restriction policy for macOS devices, there will be a new general setting available (**Devices** > **macOS** > **Configuration profiles** > **Create profile** > and then select **Templates** > **Device restrictions** for profile) that lets you Block users from erasing all content and settings on device. Use this setting to disable the reset option on supervised devices, so that users can't reset their device to factory settings.

For more information about macOS device restriction profiles in Intune, see [macOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-macos.md).

Applies to:

- macOS version 12 and later

### New software update restriction settings for macOS<!--10255184 -->

There will be five new software update settings available when configuring a macOS device restriction profile (**Devices** > **macOS** > **Configuration profiles** > **Create profile** > and then select **Templates** > **Device restrictions** for profile) in Intune.  

- **Defer software updates** (General): Prevents users from seeing certain types of newly released updates until after a deferral period. Deferring software updates doesn't stop or change scheduled updates. Types of software updates you can defer include: **Major OS software updates**, **Minor OS software updates**, **Non-OS software updates**, or any combination of the three.

- **Delay default visibility of software updates**(General): Defers the default visibility of all software updates for up to 90 days.  After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 10.13.4 and later.  
- **Delay visibility of major OS software updates**(General):  Delays visibility of major OS software updates for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 11.3 and later.  

- **Delay visibility of minor OS software updates**(General): Delays visibility of minor OS software updates for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to  macOS, version 11.3 and later.  
- **Delay visibility of non OS software updates**(General): Delays visibility of non-OS software updates (such as Safari updates) for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 11.0 and later.

For more information about macOS device restriction profiles in Intune, see [macOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-macos.md).  

<!-- ***********************************************-->
## Intune apps

### Intune management agent for macOS devices will be a universal app<!-- 9294405  -->

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. For related information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

### Syncing the iOS/iPadOS/macOS Company Portal version<!-- 10535709  -->

The version of the iOS/iPadOS Company Portal and the macOS Company Portal syncing to version 5.2019 for the next release. Going forward, the iOS/iPadOS and macOS Company Portal apps will have the same version number. For related information, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Improved flow when saving logs in Android Company Portal app<!-- 10414688  -->

In the Android Company Portal app, when users need to download a copy of the Android Company Portal logs they will be prompted to choose a folder location. In the Android Company Portal app, users will select **Settings** > **Diagnostic logs** > **SAVE LOGS** to choose the folder location.

#### Notifications from the iOS/iPadOS Company Portal app<!-- 10565849 -->

Notifications from the iOS/iPadOS Company Portal app will now be delivered to devices using the default Apple sound, rather than being delivered silently. To turn the notification sound off from the iOS/iPadOS Company Portal app, select **Settings** > **Notifications** > **Comp Portal** and select the **Sound** toggle. For related information, see [Company Portal app notifications](../apps/company-portal-app.md#company-portal-app-notifications).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   -->

We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)

After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Filter evaluation report will be improved<!-- 9974516   -->

The **Filter evaluation** page, which shows every app or policy that was filtered, will be improved to include results for available app assignments. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > *select a device* > **Filter evaluation**.

### Device filter evaluation reports now include filter results for assigned apps<!-- 9974516   -->

If you’re using filters for assigning apps as available, you can now use the filter evaluation report on a device to determine if an app has been made available for install. You can see this report per device, under **Devices > All Devices > select a device > Filter evaluation (preview)**.

- For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).
- For more information on filter reports, see [Filter reports and troubleshooting in Microsoft Endpoint Manager](filters-reports-troubleshoot.md).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

### Update to the Assignment failures operational report<!-- 6473096  -->

We will be adding [security baselines](../protect/security-baselines.md) and endpoint security profiles to the existing **Assignment failures** report. Role-based access control (RBAC) permissions will be applied to the report to filter on the set of policies that an admin can see. The profile types are differentiated using the **Policy type** column with the ability to filter. The report will show the number of devices in a state of error and conflict for a given profile, with the ability to drill down into a detailed list of those devices or users and further into the setting details. You can find the **Assignment failures** report in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**, or by selecting **Endpoint Security** > **Monitor**. For more information, see [Assignment failures report (Operational)](../fundamentals/reports.md#assignment-failures-report-operational).

### Organizational report focused on device configuration<!-- 8455708  -->

We will be releasing a new **Device configuration** organizational report. This report will replace the existing **Assignment status** report found in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Monitor**. The **Device configuration** report will allow you to generate a list of profiles in the tenant that have devices in a state of success, error, conflict, or not applicable. You can use filters for the profile type, OS, and state. The returned results will provide search, sort, filter, pagination, and export capabilities. In addition to device configuration details, this report will provide resource access details, and new settings catalog profile details. For related information, see [Intune Reports](../fundamentals/reports.md).

<!-- ***********************************************
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->

When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Intune Data Warehouse updates<!-- 9370034 -->

The  `applicationInventory`  entity will be removed from the Intune Data Warehouse in an upcoming Intune service release. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
## Security

### Attack Surface Reduction profiles for  Configuration Manager tenant attach<!--7323386  -->

We’re adding two endpoint security profiles for *Attack Surface Reduction* to Intune in support of  [Configuration Manager tenant attach](../protect/tenant-attach-intune.md). (**Endpoint security** > **Create Policy** > **Attack surface reduction**)

The new profiles:

- **Exploit Protection** - This profile will allow a device that connects to Intune via tenant attach to receive and apply the exploit protection profile.
- **Web Protection** - This profile will allow a device that connects to Intune though tenant attach to receive and apply the web protection profile.

For more information about these profiles, see [Attack surface reduction profiles](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles).

### Expanded support for Windows Defender Security Center  for tenant attach devices<!-- 7323443   -->

Today Intune supports Tamper Protection on [tenant attached devices](../protect/tenant-attach-intune.md) through the *Windows Security Experience* profile, which is part of endpoint security Antivirus policy.  

Soon, we'll add additional settings to that profile to configure the Windows Defender Security Center.  (**Endpoint security** > **Antivirus** > **Create Policy** > Platform **Windows 10, and Windows Server (ConfigMgr)** > Profile:
**Windows Security experience**).

### See policy compliance for a device in tenant attach in Endpoint Manager<!-- 9264837 -->

To manage your devices from the cloud, you can attach your Configuration Manager infrastructure to Endpoint Manager. When deploying Endpoint Security policy to tenant attached devices, you can see the overall compliance status for the policy. With device level reporting, you can see the compliance state for a policy at the device level in the Microsoft Endpoint Manager admin center.

For more information on what you can do in Endpoint Manager in a tenant attach setup, see [Microsoft Endpoint Manager tenant attach](/mem/configmgr/tenant-attach/device-sync-actions).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
