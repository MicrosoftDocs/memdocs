---
title: Technical Preview releases
titleSuffix: Configuration Manager
description: Learn about the Technical Preview release to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 06/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Technical Preview for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

**Welcome to the System Center Configuration Manager Technical Preview**. This article provides details about the evolving preview release that introduces new functionality and capabilities we are working on. Each version of the technical preview introduces new features that are not included in the current branch of Configuration Manager at the time the technical preview version is made available. These features might eventually be included in an update to the current branch release, but before we finalize the features and add them, we want you to have a chance to try them out and give us feedback.  

 Because this release is a technical preview, details and functionality are subject to change.  

 This article contains information that applies to all versions of the Technical Preview. It also lists each new capability (or feature) along with the Technical Preview version in which the capability first appears, like version 1806 for June of 2018. These capabilities are detailed in separate topics dedicated to each preview version.  

 For information about what's new in the current branch of Configuration Manager, see [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requirements and limitations for the Technical Preview  

> [!IMPORTANT]     
>  The Technical Preview is licensed for use only in a lab environment.  Microsoft may not provide support services and certain features may not be available in the preview software. Additionally, the preview software may have reduced or different security, privacy, accessibility, availability, and reliability standards relative to commercially provided software.  

 For most product prerequisites, use the information in the [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). The following exceptions apply to the Technical Preview releases:  

-   Each install remains active for 90 days before it becomes inactive.  

-   English is the only language supported.


-   Only the following install flags (switches) are supported:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   By default, when you use the technical preview, the service connection point installs to online mode. It does not support changing to offline mode.

-   The separate articles for each specific version of the technical preview include additional limitations or requirements, as applicable.

-   There is no support for migration to or from this preview build.  

-   There is no support for upgrade to this preview build. 

-   There is no support for site recovery from the cd.latest folder.  <!--507106-->

-   There is no support for upgrade to a production build (current branch) from this preview build. However, when updates are available for a preview version,  you can find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.  
-   Only a stand-alone primary site is supported. There is no support for a central administration site, multiple primary sites, or secondary sites.  

The following products and technologies are supported by this branch of Configuration Manager. However, their inclusion in this content does not imply an extension of support for a product or version that is beyond that product's individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information about Microsoft Support Lifecycles, visit the [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) website.  

-   Only the following versions of SQL Server are supported:  

    -   SQL Server 2017 (with cumulative update 2, and later) beginning in Configuration Manager version 1710
    -   SQL Server 2016 (with no Service Pack, and later)
    -   SQL Server 2014 (with Service Pack 1, and later)
    -   SQL Server 2012 (with Service Pack 3, or later)


-   The site supports up to 10 clients, which must run one of the following versions of Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Install and update the Technical Preview  
 The System Center Configuration Manager Technical Preview is distinct from the current release of System Center Configuration Manager.  

 To use the technical preview, you must first install a **baseline version** of the technical preview build. After installing a baseline version, you then use **in-console updates** to bring your installation up-to-date with the most recent preview version. Typically, new versions of the Technical Preview are available each month.

Each preview release is supported up until three successive releases are available. Meaning, when version 1708 released, version 1704 was no longer  in support, but versions 1705, 1706, and 1707 remained in support. When a baseline falls out of support, it is still supported for installing a new Technical Preview site until a new baseline version is available, so long as you then update that install to a supported version. Update to the latest available version and then repeat that process until you can install the most current version of the technical preview.

> [!TIP]  
>  When you install an update to the technical preview, you update your preview installation to that new technical preview version. A technical preview installation never has the option to upgrade to a current branch installation, nor receive updates from the current branch release.  

**Active baseline versions of the Technical Preview:**
   
You can install a baseline version for up to one year after its release. However, when you install a new technical preview site, we recommend you use the latest baseline version that is available.
-  **Technical Preview 1804** - The Configuration Manager Technical Preview 1804 is available as both an in-console update and as a new baseline version. Download baseline versions [from the TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Providing feedback  
 We love to hear your feedback about the capabilities in our technical previews. For more information, see [Product feedback](../understand/find-help.md#product-feedback).

If you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our user voice page](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capabilities delivered in the most recent technical preview  
The following are the capabilities delivered with the most recent Configuration Manager technical preview release.  Capabilities that were available in a previous version of the technical preview remain available in later versions. Similarly, capabilities that have been added to the Configuration Manager current branch remain available in technical preview releases.  Click through to the content for each preview version to learn more about a specific capability.  

<!-- This is the full list of new features in the latest TP release -->

### Technical Preview version 1806
- [Configure Windows Defender SmartScreen settings for Microsoft Edge](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge) <!--1353701-->
- [Sync MDM policy from Microsoft Intune for a co-managed device](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device) <!--1357377-->
- [Package Conversion Manager](capabilities-in-technical-preview-1806.md#package-conversion-manager) <!--1357861-->
- [Deploy software updates without content](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content) <!--1357933-->
- [Improvements to cloud management gateway](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway) <!--1358215,503899--> 



## Capabilities delivered in recent supported technical previews
The following are the capabilities delivered with previous versions of the Configuration Manager technical preview release that are still supported. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Capability |Technical Preview version |Current Branch version|  
 |----------------|---------------------|--------------------|
 | Create a phased deployment with manually configured phases for a task sequence <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![Not added](media/Red_X.gif) |  
 | Cloud distribution point support for Azure Resource Manager <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![Not added](media/Red_X.gif) |  
 | Take actions based on management insights <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![Not added](media/Red_X.gif) |  
 | Transition device configuration workload to Intune using co-management <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![Not added](media/Red_X.gif) |  
 | Enable distribution points to use network congestion control <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![Not added](media/Red_X.gif) |  
 | Cloud management dashboard <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![Not added](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![Not added](media/Red_X.gif) |  
 | Improved secure client communications <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![Not added](media/Red_X.gif) |  
 | Improvements for enabling third-party software update support <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![Not added](media/Red_X.gif) |  
 | Improvements to Windows 10 in-place upgrade task sequence <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![Not added](media/Red_X.gif) |  
 | CMTrace installed with client <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![Not added](media/Red_X.gif) |  
 | Improvement to the Configuration Manager console <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![Not added](media/Red_X.gif) |  
 | Improvements to console feedback <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![Not added](media/Red_X.gif) |  
 | Improvements to PXE-enabled distribution points <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![Not added](media/Red_X.gif) |  
 | Improvement to hardware inventory for large integer values <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![Not added](media/Red_X.gif) |  
 | Improvement to WSUS maintenance <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![Not added](media/Red_X.gif) |  
 | Improvement to support for CNG certificates <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![Not added](media/Red_X.gif) |  
| Configure a remote content library for the site server <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![Not added](media/Red_X.gif) | 
 | Submit feedback from the Configuration Manager console <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![Not added](media/Red_X.gif) | 
 | Support Center <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Not added](media/Red_X.gif) | 
 | Configuration Manager Toolkit <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![Not added](media/Red_X.gif) | 
 | Uninstall application on approval revocation <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![Not added](media/Red_X.gif) | 
 | Exclude Active Directory containers from discovery <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![Not added](media/Red_X.gif) | 
 | Specify the visibility of the Application Catalog website link in Software Center <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![Not added](media/Red_X.gif) | 
 | Filter automatic deployment rules by software update architecture <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![Not added](media/Red_X.gif) | 
 | Improvements to OS deployment <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![Not added](media/Red_X.gif) | 
 | Pull-distribution points support cloud distribution points as source <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Not added](media/Red_X.gif) | 
 | Partial download support in client peer cache to reduce WAN utilization <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Not added](media/Red_X.gif) | 
 | Maintenance windows in Software Center <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Not added](media/Red_X.gif) | 
 | Custom tab for webpage in Software Center <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Not added](media/Red_X.gif) | 
 | Enable third party software update support on clients <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Not added](media/Red_X.gif) | 
 | Enable copy/paste of asset details from monitoring views <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Not added](media/Red_X.gif) | 
 | SCAP Extensions <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Not added](media/Red_X.gif) | 
 
  

## Capabilities delivered in previous technical previews
The following are specific capabilities delivered with previous versions of the Configuration Manager technical preview release. These capabilities remain available in later versions, but are not yet available in a current branch release. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Capability |Technical Preview version |  
 |----------------|---------------------|
 | Improvements to PXE-enabled distribution points <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | Product lifecycle dashboard <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
 | Client-based PXE responder service <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Site server role high availability <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE network boot support for IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Use Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Compliance assessment for Windows Update for Business updates <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData endpoint data access <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Improvements to Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |End users can install apps from the Company Portal <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## See Also  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> For more information on current branch features that require consent to enable, see [pre-release features](/sccm/core/servers/manage/pre-release-features).  
> For more information on current branch features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

