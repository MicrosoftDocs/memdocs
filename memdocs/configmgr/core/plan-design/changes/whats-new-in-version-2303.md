---
title: What's new in version 2303
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2303 of Configuration Manager current branch.
ms.date: 03/31/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2303 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2303 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2111 or later. <!-- baseline only statement: When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update.--> This article summarizes the changes and new features in Configuration Manager, version 2303.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2211](../../servers/manage/checklist-for-installing-update-2211.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2211.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Cloud-attached management

### Improvements to Cloud Sync (Collections to Azure Active Directory Group Synchronization) feature
Starting Configuration Manager version 2303, the scalability of this feature has been improved with better throttling and error handling. Additionally, dedicated dashboards for user collections and device collections are added in Monitoring workspace to show Cloud Sync status. The dashboard displays the Cloud Sync status per collection with the mapped Azure AD group, total member count, synced member count, status (success, failed, in progress) and last sync details. 

For more information, see [Synchronize collections to Azure Active Directory Group](../../clients/manage/collections/synchronize-collections-aad-group.md).

## Site infrastructure
<!--14538358-->

### Network Access Account (NAA) account usage alert

If your site is configured with NAA account, you see this new prerequisite warning added. To improve the security of distribution points configured with NAA account, review the existing accounts and their relevant permissions. If it has more than minimal required permission, then remove and add a minimal permission account. Don't configure any administrator level permission accounts on the NAA. If the site server is configured with HTTPS / EHTTP, it's recommended to remove the NAA account, which is unused.

For more information, see the description of this [permissions-for-the-network-access-account](../../plan-design/hierarchy/accounts.md#permissions-for-the-network-access-account)

<!--14959706-->

### Distribution point content migration

DP content migration support is now available for migrating content from one DP to another DP using PowerShell cmdlets. You can also monitor the DP migration status using these PowerShell cmdlets.

For more information, see the description of this [content migration](../../servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

<!--## Client management-->

<!--## Collections-->

## Software Center

### <a name="bkmk_featured-apps-software-center"></a> Featured Apps in Software Center
<!--3601183-->
We are now adding the **Featured** tab in Software Center where we are displaying the featured apps. Using this, IT admins can mark apps as "featured" and encourage end users to use the app. Currently, this feature is available only for "User Available" apps. Also, admins can make the **Featured** tab of Software Center as the default tab from Client Settings. 

For more information, see the [Software Center in Configuration Manager](../../understand/software-center.md).

<!--## Software updates-->

<!--## OS deployment-->

<!--## Endpoint Protection-->

<!--## Application management-->

<!--## Community hub-->

## Configuration Manager console

### Enhancements in console search experience

<!--14908615-->
When performing a search on any node in the console, the hint text in the search bar will now indicate the scope of the search. Also, search experience related issues have been fixed.
 - By default, all subfolders are searched when you perform a search in any node that contains subfolders. You can narrow down the search by selecting the “Current Node” option from the search toolbar.
 - If you want to expand the search to include all nodes, then select the “All Objects” button in the ribbon.

For more information, see [Console changes and tips](../../servers/manage/admin-console-tips.md#configuration-manager-console-changes-and-tips).

### Dark theme is now extended to more dashboards

The dark theme has been available as a prerelease feature since 2203. We've extended the dark theme to more components such as buttons, context menus, and hyperlinks. Enable this prerelease feature to experience the dark theme.
In this release we've extended the dark theme to more dashboards, which previously didn't display the dark theme correctly. For example, the O365 Updates Dashboard, PCM Dashboard, and Health Attestation dashboard will now display according to the dark theme, when it's enabled. Pop-ups in the Health attestation dashboard will now adhere to the dark theme.

Enable this pre-release feature to experience the dark theme. For more information, see [Dark theme for the console](../../servers/manage/admin-console.md#bkmk_dark).
  
<!--## Tools-->

<!--## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.

As previously announced, version 2207 drops support for the following features:
-->

## Other updates

### Resolved duplicate entries for co-managed device in Intune portal 

Previously, device entities of the co-managed devices appeared as two separate entries on Intune portal. One entry corresponding to Intune and another corresponding to ConfigMgr appeared after enrollment. The entries were permanent in some cases. Various scenarios like device entity counts and policy targeting were impacted. The entries were duplicated because Intune is not aware of the AAD ID of devices coming from ConfigMgr. Intune becomes aware only after the daily discovery cycle runs and reports to Intune via CMGS.

The issue is fixed by propagating correct AAD device ID from ConfigMgr during Intune enrollment. This leads to merged entities for co-managed devices in a short period of time (30-40 mins). We no longer have to wait for discovery cycle to run.

### Starting with this version, Configuration Manager client doesn’t support the following server 

 -	Windows Server 2008 SP2 Extended Security Updates (ESU Azure Only)
      
If you have these server’s client running, please don’t upgrade to 2211 client version. For more information on supported clients and devices, see, supported-operating-systems-for-clients-and-devices[supported-operating-systems-for-clients-and-devices](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

<!--Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):
-->

<!--For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2207 release notes](/powershell/sccm/2207-release-notes).-->

<!--

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2111/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2111 | May 11, 2021 | No |
-->

## Next steps
At this time, version 2211 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2211.md#early-update-ring).

<!-- As of December 19, 2022, version 2211 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2211](../../servers/manage/checklist-for-installing-update-2211.md).).-->

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2211.md#post-update-checklist).
