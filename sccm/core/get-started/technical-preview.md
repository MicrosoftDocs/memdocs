---
title: "Technical Preview releases"
titleSuffix: "Configuration Manager"
description: "Learn about the Technical Preview release that let's you test-drive new functionality and capabilities in System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Technical Preview for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

**Welcome to the System Center Configuration Manager Technical Preview**. This article provides details about the evolving preview release that introduces new functionality and capabilities we are working on. Each version of the technical preview introduces new features that are not included in the current branch of Configuration Manager at the time the technical preview version is made available. These features might eventually be included in an update to the current branch release, but before we finalize the features and add them, we want you to have a chance to try them out and give us feedback.  

 Because this release is a technical preview, details and functionality are subject to change.  

 This article contains information that applies to all versions of the Technical Preview. It also lists each new capability (or feature) along with the Technical Preview version in which the capability first appears, like version 1802 for February of 2018. These capabilities are detailed in separate topics dedicated to each preview version.  

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
>  When you install  an update to the  technical preview, you  update your preview installation to that new technical preview version.    A technical preview installation  never has the option to upgrade to a current branch installation, nor  receive updates from the current branch release.  

**Active baseline versions of the Technical Preview:**
   
You can install a baseline version for up to one year after its release. However, when you install a new technical preview site, we recommend you use the latest baseline version that is available.
-  **Technical Preview 1711** - The Configuration Manager Technical Preview 1711 is available as both an in-console update and as a new baseline version. Download baseline versions [from the TechNet Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Providing feedback  
 We love to hear your feedback about the capabilities in our technical previews. For more information, see [Product feedback](../understand/find-help.md#product-feedback).

If you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our user voice page](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capabilities delivered in the most recent technical preview  
The following are the capabilities delivered with the most recent Configuration Manager technical preview release.  Capabilities that were available in a previous version of the technical preview remain available in later versions. Similarly, capabilities that have been added to the Configuration Manager current branch remain available in technical preview releases.  Click through to the content for each preview version to learn more about a specific capability.  

<!-- This is the full list of new features in the latest TP release -->

### Technical Preview version 1802
- [Transition Endpoint Protection workload to Intune using co-management](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) <!-- 1357365 -->
- [Configure Windows Delivery Optimization to use Configuration Manager boundary groups](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) <!-- 1324696 --> 
- [Windows 10 in-place upgrade task sequence via cloud management gateway](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) <!-- 1357149 -->
- [Improvements to Windows 10 in-place upgrade task sequence](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!-- 1357425 --> 
- [Improvements to PXE-enabled distribution points](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) <!-- 1357580 --> 
- [Deployment templates for task sequences](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) <!-- 1357391 --> 
- [Product lifecycle dashboard](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) <!--1319632 --> 
- [Improvements to reporting](capabilities-in-technical-preview-1802.md#improvements-to-reporting) <!--1357653 --> 
- [Improvements to Software Center](capabilities-in-technical-preview-1802.md#improvements-to-software-center) <!--1357592 --> 
- [Improvements to Run Scripts](capabilities-in-technical-preview-1802.md#improvements-to-run-scripts) <!--1236459 --> 
- [Boundary group fallback for management points](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) <!-- 1324594 --> 
- [Improved support for CNG certificates](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) <!-- 1357314 --> 
- [Cloud management gateway support for Azure Resource Manager](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) <!-- 1324735 --> 
- [Approve application requests for users per device](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) <!-- 1357015 --> 
- [Use Software Center to browse and install user-available applications on Azure AD-joined devices](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) <!-- 1322613 --> 
- [Report on Windows AutoPilot device information](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) <!-- 1351442 --> 
- [Improvements to Configuration Manager Policies for Windows Defender Exploit Guard](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) <!-- 1356220 -->
- [Microsoft Edge browser policies](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) <!-- 1357310 -->
- [Report for default browser counts](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) <!-- 1357830 --> 
- [Support for Windows 10 ARM64 devices](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) <!-- 1353704 --> 
- [Changes to Phased Deployments](capabilities-in-technical-preview-1802.md#changes-to-phased-deployments) <!-- 1357405 -->



## Capabilities delivered in recent supported technical previews
The following are the capabilities delivered with previous versions of the Configuration Manager technical preview release that are still supported. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Capability |Technical Preview version |Current Branch version|  
 |----------------|---------------------|--------------------|
 |Create phased deployments <!-- 1357405 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments)  |![Not added](media/Red_X.gif)    |
 |Co-management reporting <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting)  |![Not added](media/Red_X.gif)    |
 |Improvements to automatic deployment rule evaluation schedule <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule)  |![Not added](media/Red_X.gif)    |
 |Reassign distribution point <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point)  |![Not added](media/Red_X.gif)    |
 |Improvements to hardware inventory <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory)  |![Not added](media/Red_X.gif)    |
 |Improvements to client settings for Software Center <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center)  |![Not added](media/Red_X.gif)    |
 |New settings for Windows Defender Application Guard <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard)  |![Not added](media/Red_X.gif)    |
 |Improvements to Run Scripts <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts)  |![Not added](media/Red_X.gif)    |
 |Do not automatically upgrade superseded applications <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![Not added](media/Red_X.gif)    | 
 |Install multiple applications in Software Center <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![Not added](media/Red_X.gif)    |
 |Client-based PXE responder service <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service)  |![Not added](media/Red_X.gif)    |
 |Change in the Configuration Manager client install <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![Not added](media/Red_X.gif)    | 
 |Change to the Surface device dashboard <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![Not added](media/Red_X.gif)    | 
 |Improvements to Office 365 Client Management dashboard <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![Not added](media/Red_X.gif)    | 
 |Improvements to the Configuration Manager console <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![Not added](media/Red_X.gif)    | 
 |Improvements to operating system deployment <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![Not added](media/Red_X.gif)    | 
 |Run task sequence step <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Allow user interaction when installing an application <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Not added](media/Red_X.gif)    |

 

## Capabilities delivered in previous technical previews
The following are specific capabilities delivered with previous versions of the Configuration Manager technical preview release. These capabilities remain available in later versions, but are not yet available in a current branch release. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Capability |Technical Preview version |  
 |----------------|---------------------|
 |Improved VPN Profile Experience in Configuration Manager Console <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |Management insights  <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Surface Device dashboard <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Site server role high availability <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE network boot support for IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Device Health Attestation assessment for compliance policies for conditional access <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Use Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Compliance assessment for Windows Update for Business updates <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData endpoint data access <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Improvements to Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |End users can install apps from the Company Portal <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## See Also  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)
