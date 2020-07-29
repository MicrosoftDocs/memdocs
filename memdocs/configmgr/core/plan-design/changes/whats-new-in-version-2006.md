---
title: What's new in version 2006
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2006 of Configuration Manager current branch.
ms.date: 07/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby 
---

# What's new in version 2006 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2006 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1810 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->This article summarizes the changes and new features in Configuration Manager, version 2006.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2006](../../servers/manage/checklist-for-installing-update-2006.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

<!-- commenting this for now as it doesn't work 7422960
> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`
 -->

## <a name="bkmk_tenant"></a> Microsoft Endpoint Manager tenant attach

### Import previously created Azure AD application during tenant attach onboarding
<!--6479246-->
During a new onboarding, an administrator can specify a previously created application during onboarding to tenant attach. For more information, see [Microsoft Endpoint Manager tenant attach: Device sync and device actions](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="bkmk_infra"></a> Site infrastructure

### VPN boundary type

<!--7020519-->

To simplify managing remote clients, you can now create a new boundary type for VPNs. Previously, you had to create boundaries for VPN clients based on the IP address or subnet. This configuration could be challenging or not possible because of the subnet configuration or the VPN design.

Now when a client sends a location request, it includes additional information about its network configuration. Based on this information, the server determines whether the client is on a VPN.

For more information, see [Define boundaries](../../servers/deploy/configure/boundaries.md).

### Management insights to optimize for remote workers

<!--6982226-->

This release adds a new group of management insights, **Optimize for remote workers**. These insights help you create better experiences for remote workers and reduce load on your infrastructure. The insights in this release primarily focus on VPN:

- **Define VPN boundary groups**
- **Configure VPN connected clients to prefer cloud based content sources**
- **Disable peer to peer content sharing for VPN connected clients**

For more information, see [Management insights](../../servers/manage/management-insights.md).

### Improved support for Windows Virtual Desktop

<!--6527576-->

The **Windows 10 Enterprise multi-session** platform is available in the list of supported OS versions on objects with requirement rules or applicability lists.

For more information on Configuration Manager's support for Windows Virtual Desktop, see [Supported OS versions for clients and devices](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="bkmk_cloud"></a> Cloud-attached management

### Notification for Azure AD app secret key expiration

<!--6386392-->

If you configure Azure services to cloud-attach your site, the Configuration Manager console now displays notifications for the following circumstances:

- One or more Azure AD app secret keys will expire soon
- One or more Azure AD app secret keys have expired

For more information, see [Renew secret key](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### Improvements to cloud management gateway cmdlets
<!--6978300-->


<!--
## <a name="bkmk_da"></a> Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).
-->

## <a name="bkmk_real"></a> Real-time management

### Improvements to CMPivot
<!--6518631-->
The following improvements have been made in CMPivot:
- CMPivot from the console and CMPivot standalone have been converged
- Run CMPivot from an individual device or multiple devices without having to select or create a collection
- From CMPivot query results, you can select an individual device or multiple devices then launch a separate CMPivot instance for your selection.

For more information, see [CMPivot starting in version 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006)


<!--
## <a name="bkmk_content"></a> Content management
-->


## <a name="bkmk_client"></a> Client management

### Install and upgrade the client on a metered connection

<!--6976145-->

Previously, if the device was connected to a metered network, new clients wouldn't install. Existing clients only upgraded if you allowed all client communication. For devices that are frequently roaming on a metered network, they would be unmanaged or on an older client version. Starting in this release, client install and upgrade both work when you set the client setting **Client communication on metered internet connections** to **Allow** or **Limit**. With this setting, you can allow the client to stay current, but still manage the client communication on a metered network.

To define the behavior for a new client installation, there's a new ccmsetup parameter **/AllowMetered**. When you allow client communication on a metered network for ccmsetup, it downloads the content, registers with the site, and downloads the initial policy. Any further client communication follows the configuration of the client setting from that policy.

For more information, see the following articles:

- [About client settings](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md#allowmetered)


## <a name="bkmk_comgmt"></a> Co-management

### Use Microsoft Azure China 21Vianet for co-management
<!--7133238-->
You can now select the Azure China Cloud as your Azure environment when enabling co-management. For more information, see [How to enable co-management](../../../comanage/how-to-enable.md).


## <a name="bkmk_app"></a> Application management

### Improvements to Microsoft Edge Management dashboard
<!--5907383-->

### Improvements to available apps via CMG

<!--7033501-->
An internet-based, domain-joined device that isn't joined to Azure Active Directory (Azure AD) and communicates via a cloud management gateway (CMG) can now get apps deployed as available. The Active Directory domain user of the device needs a matching Azure AD identity. When the user starts Software Center, Windows prompts them to enter their Azure AD credentials. They can then see any available apps.

<!--6935376-->
This release also fixes an issue with Software Center and Azure Active Directory (Azure AD) authentication. For a client detected as on the intranet but communicating via the cloud management gateway (CMG), previously Software Center would use Windows authentication. When it tried to get the list of user-available apps, it would fail. It now uses Azure Active Directory (Azure AD) identity for devices joined to Azure AD. These devices can be cloud-joined or hybrid-joined.

For more information, see [Deploy user-available apps](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).


## <a name="bkmk_osd"></a> OS deployment

### New SDK method for task sequence progress
<!--6448458-->

### Improvements to OS deployment
<!--6452769-->

### PowerShell cmdlets for task sequence deployment types
<!--7019342-->

### Improvement to Format and Partition Disk task sequence step
<!--6610288-->

### Management insight rules for OS deployment
<!--6982275-->

### Remove command prompt during Windows 10 in-place upgrade
<!--2837795-->

### Improvements to BitLocker task sequence steps
<!--6995601-->

### Task sequence media support for cloud-based content
<!--6209223-->

### Improvements to task sequences via CMG
<!--6983320-->

## <a name="bkmk_userxp"></a> User experience

### Use the Company Portal app on co-managed devices
<!--3601237-->

### Improvements to managing device restarts

<!--3601213-->

Configuration Manager provides many options to manage device restart notifications. You can now configure the client setting **Configuration Manager can force a device to restart** to prevent devices from automatically restarting when a deployment requires it. By default, Configuration Manager can still force devices to restart.

For more information, see [device restart notifications](../../clients/deploy/device-restart-notifications.md).



## <a name="bkmk_sum"></a> Software updates

### Intranet clients can use a CMG software update point
<!--7102873-->



## <a name="bkmk_o365"></a> Office management

### Microsoft 365 Apps for enterprise
<!--6298093-->
Office 365 ProPlus was renamed to Microsoft 365 Apps for enterprise on April 21, 2020. Starting in version 2006, the following changes have been made:

- The Configuration Manager console has been updated to use the new name.
   - This change also includes update channel names for Microsoft 365 Apps.
- A banner notification was added to the console to notify you if one or more automatic deployment rules reference obsolete channel names in the **Title** criteria for Microsoft 365 Apps updates.

For more information, see [Microsoft 365 Apps channel names](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) and [Microsoft 365 Apps readiness dashboard](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## Protection

### CMG support for endpoint protection policies

<!--4773948-->

While the cloud management gateway (CMG) has supported endpoint protection policies, devices required access to on-premises domain controllers. Starting in this release, clients that communicate via a CMG can immediately apply endpoint protection policies without an active connection to Active Directory.

For more information, see [CMG support for Configuration Manager features](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### BitLocker management support for hierarchies

<!-- 5925693 -->

You can now install the BitLocker self-service portal and the administration and monitoring website at the central administration site.

For more information, see [Set up BitLocker portals](../../../protect/deploy-use/bitlocker/setup-websites.md).


<!-- 
## Reporting
-->

## <a name="bkmk_admin"></a> Configuration Manager console

### Community hub and GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(First introduced in June 2020)*

The IT admin community has developed a wealth of knowledge over the years. Rather than reinventing items like scripts and reports from scratch, we've built a Configuration Manager **Community hub** where you can share with each other. By leveraging the work of others, you can save hours of work. The Community hub fosters creativity by building on others' work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the Community hub will leverage those tools directly in the Configuration Manager console as foundational pieces for driving this new community. For the initial release, the content made available in the Community hub will be uploaded only by Microsoft.

For more information, see [Community hub and GitHub](../../servers/manage/community-hub.md).

### New feedback wizard
<!--3180826-->

### Query for feedback sent to Microsoft
<!--6488450-->

### Copy discovery data from the console
<!--6890051-->

### Notifications from Microsoft
<!--3953121-->
You can now choose to receive notifications from Microsoft in the Configuration Manager console. These notifications help you stay informed about new or updated features, changes to Configuration Manager and attached services, and issues that require action to remediate.

For more information, see [Configure a site to receive messages from Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### Report setup and upgrade failures to Microsoft
<!--5622909-->


## Tools

### Support for PowerShell version 7
<!--6023299-->

### Improvements to the content library cleanup tool
<!--6887878-->


## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

<!-- ### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956--> -->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 2006 release notes](https://docs.microsoft.com/powershell/sccm/2006-release-notes?view=sccm-ps).

For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md#bkmk_2006).

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## Next steps

At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring).

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).
