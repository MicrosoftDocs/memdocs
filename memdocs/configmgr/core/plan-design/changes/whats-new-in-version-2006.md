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

### Tenant attach: ConfigMgr client details
<!--6374854-->

### Tenant attach: Device timeline in the admin center
<!--7141381-->

### Tenant attach: Install an application from the admin center
<!--6024389-->

### Tenant attach: CMPivot from the admin center
<!--6024392-->

### Tenant attach: Run Scripts from the admin center
<!--6234688-->


## <a name="bkmk_infra"></a> Site infrastructure

### VPN boundary type
<!--7020519-->


## <a name="bkmk_cloud"></a> Cloud-attached management

### Notification for Azure AD app secret key expiration
<!--6386392-->

### Improvements to cloud management gateway cmdlets
<!--6978300-->


<!--
## <a name="bkmk_da"></a> Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).
-->

## <a name="bkmk_real"></a> Real-time management

### Improvements to CMPivot
<!--6518631-->
<!-- include changes from 2003 and 2004 -->


<!--
## <a name="bkmk_content"></a> Content management
-->


## <a name="bkmk_client"></a> Client management

### Install and upgrade the client on a metered connection
<!--6976145-->


<!--
## <a name="bkmk_comgmt"></a> Co-management
-->



## <a name="bkmk_app"></a> Application management

### Improvements to Microsoft Edge Management dashboard
<!--5907383-->


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


## <a name="bkmk_userxp"></a> Software Center

### Azure AD authentication in Software Center
<!--6935376-->


<!-- 
## <a name="bkmk_sum"></a> Software updates
-->


## <a name="bkmk_o365"></a> Office management

### Microsoft 365 Apps for enterprise
<!--6298093-->


<!-- 
## Protection

## Reporting
-->

## <a name="bkmk_admin"></a> Configuration Manager console

### Community hub and GitHub
<!--3555935-->

### New feedback wizard
<!--3180826-->

### Query for feedback sent to Microsoft
<!--6488450-->

### Copy discovery data from the console
<!--6890051-->

### Notifications from Microsoft
<!--3953121-->

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
