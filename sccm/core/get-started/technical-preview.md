---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 01/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Technical preview for Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article provides details about the monthly technical preview branch of Configuration Manager. The technical preview introduces new functionality that Microsoft is working on. It introduces new features that aren't yet included in the current branch of Configuration Manager. These features might eventually be included in an update to the current branch. Before we finalize the features, we want you to try them out and give us feedback.  

Because this release is a technical preview, details and functionality are subject to change.  

This information applies to all versions of the Configuration Manager technical preview branch. This article lists each new feature along with the technical preview version in which it first appears. For example, version **1901** for January (01) of 2019 (19). Separate articles dedicated to each preview version detail the individual features.  

For information about what's new in the *current branch* of Configuration Manager, see [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Requirements and limitations  

> [!IMPORTANT]     
>  The technical preview is licensed for use only in a lab environment. Microsoft may not provide support services and certain features may not be available in the preview software. Additionally, the preview software may have reduced or different security, privacy, accessibility, availability, and reliability standards relative to commercially provided software.  

For most product prerequisites, use the information in the [Supported configurations](/sccm/core/plan-design/configs/supported-configurations). The following exceptions apply to the technical preview branch:  

-   Each install is active for 90 days before it becomes inactive.  

-   English is the only language supported.  

-   It only supports the following setup command-line parameters:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   The service connection point installs to online mode. It doesn't support offline mode.  

-   The separate articles for each specific version of the technical preview include additional limitations or requirements, as applicable.

-   The following features aren't supported with the technical preview branch:  

    - [Migration](/sccm/core/migration/migrate-data-between-hierarchies) to or from this preview branch.  

    - [Upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) to this preview branch.  

    - [Site recovery](/sccm/core/servers/manage/recover-sites) from the cd.latest folder.  <!--507106-->

-   There's no support for updating to current branch from this preview branch.  

    > [!Note]  
    > When updates are available for a preview version, you still find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.  

-   It only supports a standalone primary site. There's no support for a central administration site, multiple primary sites, or secondary sites.  

The technical preview branch of Configuration Manager supports the following products and technologies: 

-   It only supports the following versions of **SQL Server**:  

    -   SQL Server 2017 (with cumulative update 2, and later) beginning in Configuration Manager version 1710
    -   SQL Server 2016 (with no Service Pack, and later)
    -   SQL Server 2014 (with Service Pack 1, and later)
    -   SQL Server 2012 (with Service Pack 3, or later)  


-   The site supports up to 10 clients, which must run one of the following versions of Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> The inclusion of these products in this content doesn't imply an extension of support for a version that's beyond its support lifecycle. Configuration Manager doesn't support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Install and update  

The Configuration Manager technical preview branch for lab use is distinct from the Configuration Manager current branch for production use.  

First install a baseline version of the technical preview branch. After installing a baseline version, then use in-console updates to bring your installation up-to-date with the most recent preview version. Typically, new versions of the technical preview are available each month.

Microsoft supports each technical preview version up until three successive versions are available. For example, when version 1708 released, version 1704 was no longer in support. Versions 1705, 1706, and 1707 remained in support. When a baseline falls out of support, it's still supported for installing a new technical preview site, assuming you immediately update to a supported version. The older baseline is supported until a new baseline version is available. Update to the latest available version from the baseline, and then repeat the update process until you install the latest technical preview version.

> [!TIP]  
>  When you install an update to the technical preview, you update your preview installation to that new technical preview version. A technical preview installation never has the option to upgrade to a current branch installation. It also never receives updates from the current branch release. 
> 
> Several times throughout the year, there are technical preview branch and current branch versions with the same version number. For example, there is a technical preview version 1802 and a current branch version 1802. 


### Active baseline versions
   
Install a baseline version for up to one year after its release. When you install a new technical preview site, if more than one baseline version is currently available, use the latest baseline version.

-  **Technical preview version 1810.2**: The Configuration Manager technical preview version 1810.2 is available as both an in-console update and as a new baseline version. Download baseline versions from the [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Providing feedback  

We love to hear your feedback about the new features in the technical preview. For more information, see [Product feedback](/sccm/core/understand/find-help#product-feedback).

If you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our UserVoice page](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Features in the most recent version  

The following features are available with the most recent Configuration Manager technical preview version: 

<!-- This is the full list of new features in the latest TP release -->

### Technical Preview version 1901

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor)<!--ID-->


- [Client health dashboard](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health)<!--3599209-->  
- [Specify priority for feature updates in Windows 10 servicing](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo)<!--3734525-->  
- [Dedicated monitoring for phased deployments](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod)<!--3555949--> 
- [Run CMPivot from the central administration site](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot)<!--3610960-->  
- [Improvements to Run PowerShell Script task sequence step](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh)<!--3556028-->  
- [Office products on lifecycle dashboard](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle)<!--3556026-->  
- [Management insight rules for collections](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll)<!--3555752-->  
- [Search device views using MAC address](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac)<!--3600878-->  
- [Distribution point maintenance mode](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint)<!--3555754-->  
- [Optimized image servicing](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase)<!--3555951-->  
- [Import a single index of an OS image](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index)<!--3719699--> 
- [Use Azure Resource Manager for cloud services](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm)<!--3605704-->  
- [Confirmation of console feedback](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback)<!--3556010--> 
- [Create a Configuration Manager technical preview lab in Azure](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm)<!--3556017-->  
- [Specify a custom port for peer wakeup](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep)<!--3605925-->  
- [View recently connected consoles](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console)<!--3699367-->  
- [Stop cloud service when it exceeds threshold](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg)<!--3735092--> 
- [Client provisioning mode timeout](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov)<!--3197824-->
- [Improvements to OS deployment](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd)<!--3633146,3641475,3654172,3734270-->


> [!Note]  
> Features that were available in a previous version of the technical preview remain available in later versions. Similarly, features that are added to the Configuration Manager current branch remain available in the technical preview branch.   



## Features in recent supported technical previews

The following features were released with previous versions of the Configuration Manager technical preview branch that are still supported: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Feature | Technical preview version | Current branch version |  
 |---------|---------------------------|------------------------|
 | Improvements to Run PowerShell Script task sequence step <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![Not added](media/Red_X.gif) | 
 | Improvements to application approvals via email <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![Not added](media/Red_X.gif) | 
 | Configure user device affinity in Software Center <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![Not added](media/Red_X.gif) | 
 | Improvements to Configuration Manager console <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![Not added](media/Red_X.gif) | 
 | Download reports from the Community Hub<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Not added](media/Red_X.gif) | 
 | Don't load Windows PowerShell profiles <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Not added](media/Red_X.gif) | 
 | An Intune connection is no longer required for on-premises MDM <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Not added](media/Red_X.gif) | 
 | Configuration Manager console notifications <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Not added](media/Red_X.gif) | 
 | Improvements to task sequence media creation <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Not added](media/Red_X.gif) | 
 | Improvement to Run PowerShell Script task sequence step <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Not added](media/Red_X.gif) | 
 | Improvements to collection evaluation <!--1358981--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_colleval) | Version 1810 | 
 | Configuration Manager administrator authentication <!--1357013--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_auth) | Version 1810 | 
 | Management insights rule for peer cache source client version <!--1358008--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_insights) | Version 1810 | 
 | Improvements to internet-based client setup <!--1359181--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_cmg) | Version 1810 | 
 | Convert applications to MSIX <!--1359029--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_msix) | Version 1810 | 



## Features in previous technical previews

The following features were released with previous versions of the Configuration Manager technical preview branch. These features remain available in later versions, but aren't yet available in the current branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Feature        | Technical preview version |  
|----------------|---------------------------|
| In-console documentation dashboard <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| Community Hub <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Co-managed device sync activity with Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Client-based PXE responder service <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE network boot support for IPv6 <!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Use Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Compliance assessment for Windows Update for Business updates <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Improvements to Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| End users can install apps from the Company Portal <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## See also  

For more information, see the following articles:  

- [Evaluate Configuration Manager in a lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introduction to Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> For more information on current branch features that require consent to enable, see [pre-release features](/sccm/core/servers/manage/pre-release-features).  
> 
> For more information on current branch features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
