---
title: "New version 1710 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1710 of System Center Configuration Manager."
ms.custom: na
ms.date:  11/20/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# What&#39;s new in version 1710 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1710 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1610, 1702, or 1706.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1710 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1710 drops support for the following products:
-->


## Site infrastructure

### Updates for Peer Cache  
Beginning with this release, Peer Cache is no longer a pre-release feature.  No other changes for Peer Cache are introduced with this release. For more information, see  [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).

### Cloud distribution point support for Azure Government Cloud
You can now use [cloud-based distribution points](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in the Azure Government cloud.   


<!-- ## Migration  -->


## Client management

### Co-management for Windows 10 devices    
<!-- 1350871 -->
Starting with the Windows 10, version 1607 (also known as the Anniversary Update), you can join a Windows 10 device to on-premises Active Directory (AD) and cloud-based Azure AD at the same time (hybrid Azure AD). Co-management takes advantage of this improvement and enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Intune. It’s a solution that provides a bridge from traditional to modern management and gives you a path to make the transition using a phased approach. For details, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview.md).


<!--  ## Compliance settings  -->


<!-- ## Application Management  -->



## Operating system deployment
 > [!TIP]
 > Beginning with the Windows 10, version 1709 (also known as the Fall Creators Update) release, Windows media includes multiple editions. When configuring a task sequence to use an operating system upgrade package or operating system image, be sure to select an [edition that is supported for use by Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).


## Software updates    

### Surface Device dashboard
The Surface Device dashboard provides information about the Surface devices found in your environment. In the console, go to **Monitoring** > **Surface Devices**. For details, see [Surface Device dashboard](/sccm/sum/deploy-use/monitor-software-updates.md#surface-device-dashboard).

<!--  ## Reporting  -->


<!-- ## Inventory  -->


<!--  ## Mobile device management  -->


<!--  ## Protect devices   -->


## Next Steps
When your ready to install this version, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
