---
title: "New version 1706 | Microsoft Docs"
description: "Get details about changes and new capabilities introduced in version 1706 of System Center Configuration Manager."
ms.custom: na
ms.date:  07/31/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# What&#39;s new in version 1706 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1706 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1606, 1610, or 1702.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1706 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1706 drops support for the following products:
-->


## Site infrastructure

### Client Peer Cache support for express installation files for Windows 10 and Office 365  
Beginning with this release, Peer Cache supports distribution of content express installation files for Windows 10, and of update files for Office 365. No additional configurations are required to support this change.

### Updates for the data warehouse
The data warehouse is no longer a pre-release feature. We have also updated the prerequisites to include support for the database on SQL Server Always on availability groups, and failover clusters. For more information, see [The Data Warehouse service point](/sccm/core/servers/manage/data-warehouse).

### Accessibility improvements
We have added additional improvements to accessibility for the Configuration Manager console. For details, see [Accessibility features](/sccm/core/understand/accessibility-features).

### Improvements  for SQL Server Always On Availability Groups
With this release, you can now use asynchronous commit replicas in the SQL Server Always On availability groups you use with Configuration Manager. This means you can add additional replicas to your availability groups to use as off-site (remote) backups, and then use them in a disaster recovery scenario.  
  -	  Configuration Manager supports using the asynchronous commit replica to recover your synchronous replica. See [site database recovery options](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) in the Backup and Recovery topic for information on how to accomplish this.
  -	  This release does not support failover to use the asynchronous commit replica as your site database.
For more information, see [Prepare to use Always On Availability Groups](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### Update reset tool
Beginning with version 1706, Configuration Manager primary sites, and central administration sites include the Configuration Manager Update Reset Tool, **CMUpdateReset.exe**. Use this tool with any version of the current branch that remains in support, to fix issues when in-console updates have problems downloading or replicating.  

For more infomration, see [Update replication tool](/sccm/core/serves/manage/update-reset-tool).


<!-- ## Migration  -->


<!-- ## Client management  -->


<!-- ## Compliance settings -->


<!-- ## Application Management  -->


<!--  ## Operating system deployment  -->

<!-- ## Software updates -->


<!-- ## Reporting  -->

<!-- ## Inventory  -->

<!--  ## Mobile device management  -->

<!--  ## Protect devices  -->
