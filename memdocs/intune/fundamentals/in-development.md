---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 5/28/2021
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
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->
## App management

### Export underlying discovered apps list data<!-- 9370255  -->

In addition to exporting the summarized discovered apps list data, you will also be able export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the additional new experience will also provide the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data will be a list of every device and each app discovered for that device. This functionality is being added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset, which will be removed in the 2108 release. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Maximum OS version setting for app conditional launch<!-- 9493137  -->

Using iOS app protection policies in Microsoft Intune app protection policies, you will be able to add a new conditional launch setting to ensure end users are not using a pre-release or beta OS build to access work or school account data. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

### Updated default license type for Apple VPP apps<!-- 9914613  -->

When you create a new assignment for an Apple Volume Purchase Program (VPP) app, the default license type is now "device". Existing assignments remain unchanged. For more information about Apple VPP apps, see [How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ***********************************************-->
## Device configuration

### See policy compliance for a device in tenant attach in Endpoint Manager<!-- 9264837 -->

To manage your devices from the cloud, you can attach your Configuration Manager infrastructure to Endpoint Manager. When deploying Endpoint Security policy to tenant attached devices, you'll be able to see the overall compliance status for the policy. With device level reporting, you'll be able to see the compliance state for a policy at the device level in the Microsoft Endpoint Manager admin center.

For more information on what you can do in Endpoint Manager in a tenant attach setup, see [Microsoft Endpoint Manager tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

### Use a Settings Catalog policy in a policy set for Windows and macOS devices<!-- 8851701  -->

In Intune, you can create a policy using [Settings Catalog](../configuration/settings-catalog.md), which lists all the settings you can configure. Now, you can use the Settings Catalog policy within a policy set.

For more information, see [Use policy sets to group collections of management objects](policy-sets.md).

Applies to:

- macOS
- Windows 10 and newer

### Settings catalog policies for policy sets<!-- 8683467  -->

In addition to profiles based on templates, you will be able to add a profiles based on the **Settings catalog** to your policy sets. The **Settings catalog** is a list of all the settings you can configure. To create a policy set in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Policy sets** > **Policy sets** > **Create**. For more information, see [Use policy sets to group collections of management objects](../fundamentals/policy-sets.md) and [Use the settings catalog to configure settings on Windows and macOS devices - preview](../configuration/settings-catalog.md).

### Use the EnrollmentProfileName property when creating a filter for Android Enterprise<!-- 10022750  -->

In Endpoint Manager, you can create [filters](filters.md) to target devices based on different properties, including device name, manufacturer, and more. On iOS/iPadOS and Windows 10 and newer devices, you can create a filter using the enrollment profile name. The enrollment profile name property will be available for Android Enterprise devices.

To see the filter properties you can currently configure, go to [Device properties, operators, and rule editing when creating filters](filters-device-properties.md).

Applies to:

- Android Enterprise

### Use filters on Settings Catalog configuration profiles, and Risk Score and Threat Level compliance policy settings<!-- 10023995 7556913  -->

When you use [filters](filters.md) to assign your policies, you'll be able to:

- Use filters on compliance policies that use the **Risk Score** and **Threat Level** settings.
- Use filters on configuration profiles that use the **Settings Catalog** profile type.

For more information on what you can do, see [List of platforms, policies, and app types supported by filters](filters-supported-workloads.md).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

### New macOS device configuration profile settings, and iOS/iPadOS setting name is changing<!-- 9772945  -->

There are new settings you can configure on macOS 10.13 devices and newer (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates** > **Device restrictions** for profile type):

- **Block adding Game Center friends** (App Store, Doc Viewing, Gaming): Prevents users from adding friends to the Game Center.
- **Block Game Center** (App Store, Doc Viewing, Gaming): Disables the Game Center, and the Game Center icon is removed from the Home screen.
- **Block multiplayer gaming in the Game Center** (App Store, Doc Viewing, Gaming): Prevents multiplayer gaming when using the Game Center.
- **Block modification of wallpaper** (General): Prevents the wallpaper from being changed.

To see the settings you can currently configure, go to [macOS device settings to allow or restrict features](../configuration/device-restrictions-macos.md).

Also, the iOS/iPadOS **Block Multiplayer Gaming** setting name is changing to **Block multiplayer gaming in the Game Center** (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type).

For more information about this setting, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS
- macOS 10.13 and newer

### More iOS/iPadOS home screen layout grid size options<!-- 9569886  -->

On iOS/iPadOS devices, you can configure the grid size on the home screen (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). For example, you can set the grid size to 4 columns x 5 rows.

The grid size will have more options:

- 4 columns x 5 rows
- 4 columns x 6 rows
- 5 columns x 6 rows

To see the home screen layout settings you can currently configure, go to [device settings to use common iOS/iPadOS features in Intune](../configuration/ios-device-features-settings.md#home-screen-layout).

Applies to:

- iOS/iPadOS

<!-- ***********************************************-->
## Device enrollment

### Browser access automatically enabled during corporate Android enrollment<!--6613616 -->

Browser access will be automatically enabled during new enrollments of the following devices:

- Android dedicated devices
- Android fully managed devices
- Android corporate-owned work profile devices

With this upcoming change, compliant devices can use the browser to access resources protected by conditional access.

This change will have no impact on devices that are already enrolled.

<!-- ***********************************************-->
## Device management

### Tenant attach: Offboarding <!--9412904 -->

While we know customers get enormous value by enabling tenant attach with Configuration Manager, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard from the cloud following a disaster recovery scenario where the on-premises environment was removed. You'll soon be able to offboard a Configuration Manager environment from the Microsoft Endpoint Manager admin center.

<!-- ***********************************************-->
## Device security

### Settings catalog support for Microsoft Defender for Endpoint on macOS<!-- 5520115   -->

You'll soon be able to use the [settings catalog](../configuration/settings-catalog.md) to configure Microsoft Defender for Endpoint on macOS. (**Devices** > **Configuration profiles** > **Create profile** > **macOS** > **Settings catalog**).

Some of the settings we plan to make available from the settings catalog include:

**Microsoft Defender - Antivirus engine**:

- Allowed threats
- Enable passive mode
- Enable real-time protection
- Scan exclusions
- Threat type settings

**Microsoft Defender - Cloud delivered protection preferences**:

- Diagnostic collection level
- Enable - disable automatic sample submissions
- Enable - disable cloud delivered protection

**Microsoft Defender - EDR preferences**:

- Device tags
- Enable - disable early preview

**Microsoft Defender - User interface preferences**:

- Show - hide status menu icon

### Certificate Connector for Microsoft Intune combines separate certificate connectors<!-- 9843502  -->

The separate certificate connectors are being combined into a unified connector called **Certificate Connector for Microsoft Intune**. This unified connector replaces existing connectors, and includes the following new features:

- Configure SCEP, PKCS, PFX imported certs, and revocation in the same connector.
- Use normal Active Directory accounts or the system account for the connector service.
- Based on your tenant location, select government vs. commercial environments.
- Removes the need to select a client certificate for SCEP integration with NDES.
- Auto-updates to the latest version of the connector.
- Improved logging.

To use the **Certificate Connector for Microsoft Intune**:

1. Uninstall any existing certificate connectors.
2. Install the Certificate Connector for Microsoft Intune.

For more information on certificate connectors, see [Certificate connectors for Microsoft Intune](../protect/certificate-connectors.md).

<!-- ***********************************************-->
## Intune apps

### End users can restart an app install from the Company Portal<!-- 652935  -->

Using the Company Portal, end users will be able to restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.

### Intune management agent for macOS devices will be a universal app<!-- 9294405  -->

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. For related information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   -->

We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)

After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Export capability for Enrollment failures report<!-- 5491082  -->

You will be able to export data from the Enrollment failures operational report. This report will allow you to quickly export reporting data generated from any size tenant. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Enrollment failures** > **Export**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

### The Certificates report will be updated<!-- 10034112 -->

The **Certificates** report, which shows the current device certificates in use, will be updated to include better capabilities to search, page, sort, and export the report. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Certificates**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

<!-- ***********************************************-->
## Role-based access control

### Scope tags for Managed Google Play apps<!-- 6114508  -->

Scope tags determine which objects an admin with specific rights can view in Intune. Most newly-created items in Intune take on the scope tags of the creator. This is not the case for Managed Google Play Store apps. You will be able to optionally assign a scope tag to apply to all newly-synced Managed Google Play apps on the **Managed Google Play connector** pane. The chosen scope tag will only apply to new Managed Google Play apps, not Managed Google Play apps that have already been approved in the tenant. For related information see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md) and [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->

When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Intune Data Warehouse updates<!-- 9370034 -->

The  `applicationInventory`  entity will be removed from the Intune Data Warehouse with the 2108 service update of Intune. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
## Security

### New options for Tunnel Gateway server upgrades<!-- 8664465    -->

You'll soon be able to configure some aspects of Microsoft Tunnel Gateway server upgrades. (**Tenant administration** > **Microsoft Tunnel Gateway (preview)**)

Options include:

- Restrict the start of server upgrades to a specific time window.
- Configure servers at a site to upgrade manually, or require the admin to approve an upgrade before it can start.

We're also adding a new health check setting that helps you identify when a server is running the latest version of Tunnel Gateway.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
