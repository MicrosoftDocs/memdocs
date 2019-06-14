---
title: What's new in version 1906
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1906 of Configuration Manager current branch.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# What's new in version 1906 of Configuration Manager current branch

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1906 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1806, 1810, or 1902. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> This article summarizes the changes and new features in Configuration Manager, version 1906.  

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="bkmk_deprecated"></a> Deprecated features and operating systems

Learn about support changes before they're implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1906 drops support for the following features:  

- Classic service deployment to Azure for cloud management gateway and cloud distribution point. For more information, see [Plan for CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).



## <a name="bkmk_infra"></a> Site infrastructure

### Site server maintenance task improvements
<!--3555894-->

### Configuration Manager update database upgrade monitoring
<!--4200581-->

### Management insights rule for NTLM fallback
<!--4572953-->

### Add a SQL AlwaysOn node
<!--3127336-->



## <a name="bkmk_cloud"></a> Cloud-attached management

### Cloud services cost estimator
<!--3555774-->

### Azure Active Directory user group discovery
<!--3611956-->

### Synchronize collection membership results to Azure Active Directory groups
<!--3607475-->




## <a name="bkmk_da"></a> Desktop Analytics

### DALogsCollector tool
<!--4622989-->

### Changing the Desktop Analytics limiting collection on existing deployments
<!--3218073-->



## <a name="bkmk_real"></a> Real-time management

### CMPivot standalone
<!--3555890-->

### Add joins, additional operators and aggregators in CMPivot
<!--4054074-->

### Improvements to CMPivot
<!--4619340,4683130-->



## <a name="bkmk_content"></a> Content management

### Delivery Optimization download data in client data sources dashboard
<!--3555759-->

### Use your distribution point as an in-network cache server for Delivery Optimization
<!--3555764-->



## <a name="bkmk_client"></a> Client management

### Support for Windows Virtual Desktop
<!--3556025-->

### OneTrace (Preview)
<!--3555962-->

### 1906 client won't install on legacy OS (SHA-1)
<!--4222696-->

### Configure client cache minimum retention period
<!--4485509-->



## <a name="bkmk_comgmt"></a> Co-management

### Improvements to co-management auto-enrollment
<!--3555961-->

### Multiple pilot groups for co-management workloads
<!--3555750-->

### Co-management support for government cloud
<!--4075452-->



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->




## <a name="bkmk_app"></a> Application management

### Filter applications deployed to devices
<!--4451056-->

### Application groups
<!--3555907-->

### Retry the install of pre-approved applications
<!--4336307-->

### Install an application for a device
<!--4402180-->

### Improvements to app approvals
<!--4224910-->



## <a name="bkmk_osd"></a> OS deployment

### Task sequence debugger
<!--3612274-->

### Improvements to driver management
<!--3555958-->

### Clear app content from client cache during task sequence
<!--4485675-->

### Reclaim SEDO lock for task sequences
<!--3699337-->

### Pre-cache driver packages and OS images
<!--4224642-->

### Improvement to task sequence media creation
<!--4090666-->

### Improvements to OS deployment 
<!--2839943,4447680-->
<!--4512937,4224642-->
<!--4668846, 2840337, 4512937-->



## <a name="bkmk_userxp"></a> Software Center

### Improvements to Software Center tab customizations
<!--4063773-->

### Software Center infrastructure improvements
<!--3555950-->

### Redesigned notification for newly available software
<!--3555904-->

### More frequent countdown notifications for restarts
<!--3976435-->

### Direct link to custom tabs in Software Center
<!--4655176-->



## <a name="bkmk_sum"></a> Software updates

### Additional options for WSUS maintenance
<!--4110109-->

### Configure the default maximum run time for software updates
<!--3734426-->

### Configure dynamic update during feature updates
<!--4062619-->

### New Windows 10, version 1903 and later product category
<!--4682946-->

### Drill through required updates
<!--4224414-->



## <a name="bkmk_o365"></a> Office management

### Office 365 ProPlus upgrade readiness dashboard
<!--4021125-->



## <a name="bkmk_inv"></a> Inventory

### Improvement to Asset Intelligence
<!--4586547-->



<!-- ## <a name="bkmk_pod"></a> Phased deployments -->




## <a name="bkmk_protect"></a> Protection

### Windows Defender Application Guard file trust criteria
<!--3555858-->




## <a name="bkmk_admin"></a> Configuration Manager console

### Add SMBIOS GUID column to device and device collection nodes
<!--4526580-->

### RBAC on folders
<!--3600867-->

### Administration service support for security nodes
<!--4223683-->



<!--
## Other updates

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4498910).

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 1906 release notes](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->


## Next steps

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
> Learn more about:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
> - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

For known, significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist).
