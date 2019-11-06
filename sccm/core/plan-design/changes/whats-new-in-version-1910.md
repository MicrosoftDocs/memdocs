---
title: What's new in version 1910
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1906 of Configuration Manager current branch.
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# What's new in version 1910 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 1910 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1806 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> This article summarizes the changes and new features in Configuration Manager, version 1910.  

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`


## Requirement changes

## <a name="bkmk_infra"></a> Site infrastructure

### Reclaim SEDO lock
<!--4786915-->

### Extend and Migrate on-premises Configuration Manager environment to Microsoft Azure
<!--3556022-->

## <a name="bkmk_cloud"></a> Cloud-attached management



## <a name="bkmk_da"></a> Desktop Analytics



## <a name="bkmk_real"></a> Real-time management

### Optimizations to the CMPivot engine that pushes more of the processing to the ConfigMgr client
<!--3197353-->


### Enable ATP and CMPivot to link to each other
<!--4775821--?-->

### Additional CMPivot Entities and Enhancements
<!--5410930-->


## <a name="bkmk_content"></a> Content management


## <a name="bkmk_client"></a> Client management

### Include custom configuration baselines as part of compliance policy assessment
<!--3608345-->

### Enable user policy for Windows 10 Enterprise multi-session
<!--4737447-->

## <a name="bkmk_comgmt"></a> Co-management




## <a name="bkmk_app"></a> Application management

### Deploy Microsoft Edge, version 77 and later
<!--4561024-->

### Improvements to application groups
<!--4760058-->

## <a name="bkmk_osd"></a> OS deployment

### Output the results of a Run Command Line step to a variable during a task sequence
<!--4977616-->

### Import a single index of an OS upgrade package
<!--4931110-->

### Custom default keyboard layout in boot image properties
<!--4910348-->

### Improvements to the task sequence editor

- **Search the task sequence editor**<!--4621085-->: If you have a large task sequence with many groups and steps, it can be difficult to find specific steps. You can now search in the task sequence editor. This action lets you more quickly locate steps in the task sequence.

- **Copy and paste task sequence conditions**<!--4621098-->: If you want to reuse the conditions from one task sequence step to another, you can now copy and paste conditions in the task sequence editor.

For more information, see the new article on how to [Use the task sequence editor](/sccm/osd/understand/task-sequence-editor).

### Task sequence performance improvements - power plans
<!--3555926-->

### Task sequence download on demand over the internet

<!--3601238-->

You can use the task sequence to deploy Windows 10 in-place upgrade via cloud management gateway (CMG). However, it requires the deployment to download all content locally before starting the task sequence.

Starting in this release, the task sequence engine can download packages on-demand from a content-enabled CMG or a cloud distribution point. This change provides additional flexibility with your Windows 10 in-place upgrade deployments to internet-based devices.

For more information, see [Deploy Windows 10 in-place upgrade via CMG](/configmgr/osd/deploy-use/deploy-a-task-sequence#deploy-windows-10-in-place-upgrade-via-cmg).

### Set keyboard layout during OS deployment
<!--5138936-->

### Improvements to task sequence debugger
<!-- 5012536, 5012509 -->

### Improved language support in task sequence
<!--5411057-->

### New variable for Windows 10 in-place upgrade
<!--4680263-->

## <a name="bkmk_userxp"></a> Software Center


## <a name="bkmk_sum"></a> Software updates

### Additional options for third-party update catalogs
<!--4469002-->

### Use Delivery Optimization for all Windows updates
<!--4699118-->

### Additional software update filter for ADRs
<!--4852033-->


## <a name="bkmk_o365"></a> Office management

### Office 365 ProPlus Health Dashboard
<!--4488301-->

### Office 365 ProPlus Pilot and Health Dashboard
<!--4488272-->

## <a name="bkmk_protect"></a> Protection

### BitLocker Management (MBAM)
<!--3601034-->


## <a name="bkmk_admin"></a> Configuration Manager console

### View active consoles and message administrators through Console Connections
<!--4923997-->

### Client Diagnostics Actions
<!--4433455-->

### Attach files to feedback
<!--3556011-->

## Other updates

### Extend and migrate on-premises site to Microsoft Azure
<!--3556022-->

This new tool helps you to programmatically create Azure virtual machines (VMs) for Configuration Manager. It can install with default settings site roles like a passive site server, management points, and distribution points. Once you validate the new roles, use them as additional site systems for high availability. You can also remove the on-premises site system role and only keep the Azure VM role. For more information, see [Extend and migrate on-premises site to Microsoft Azure](/sccm/core/support/azure-migration-tool).

### Improvements to console search
<!--4640570-->

## Other updates

As of this version, the following features are no longer pre-release:
<!--
- [SMS Provider administration service](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)
- [Device Guard management](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4514258).

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 1906 release notes](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->


## Next steps

At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](/sccm/core/servers/manage/checklist-for-installing-update-1910#early-update-ring). 
<!--As of August 16, 2019, version 1906 is globally available for all customers to install.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
> Learn more about:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
> - [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines)  

For known, significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).
