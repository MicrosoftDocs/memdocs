---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 4/30/2021
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

### Export underlying discovered apps list data<!-- 9370255  -->

In addition to exporting the summarized discovered apps list data, you will also be able export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the additional new experience will also provide the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data will be a list of every device and each app discovered for that device. This functionality is being added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset, which will be removed in the 2108 release. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Maximum OS version setting for app conditional launch<!-- 9493137  -->

Using iOS app protection policies in Microsoft Intune app protection policies, you will be able to add a new conditional launch setting to ensure end users are not using a pre-release or beta OS build to access work or school account data. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

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

<!-- ***********************************************-->
<!--
## Device enrollment
-->

<!-- ***********************************************-->
## Device management

### Tenant attach: Offboarding <!--9412904 -->

While we know customers get enormous value by enabling tenant attach with Configuration Manager, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard from the cloud following a disaster recovery scenario where the on-premises environment was removed. You'll soon be able to offboard a Configuration Manager environment from the Microsoft Endpoint Manager admin center.

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

### Organizational report focused on device configuration<!-- 8455708  -->

We'll be releasing a new **Device configuration** organizational report. This report will replace the existing **Assignment status** report found in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Monitor**. The **Device configuration** report will allow you to generate a list of profiles in the tenant that have devices in a state of success, error, conflict, or not applicable. You can use filters for the profile type, OS, and state. The returned results will provide search, sort, filter, pagination, and export capabilities. In addition to device configuration details, this report will provide resource access details, and new Settings Catalog profile details. For related information, see [Intune Reports](../fundamentals/reports.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

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
