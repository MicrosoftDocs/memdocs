---
title: "Technical Preview for Configuration Manager | Microsoft Docs"
description: "Learn about the Technical Preview release that let's you test-drive new functionality and capabilities in System Center Configuration Manager."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Technical Preview for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

**Welcome to the System Center Configuration Manager Technical Preview**. This topic provides details about the evolving preview release that introduces new functionality and capabilities we are working on. With each version of the technical preview, new features are introduced that are not included in the current branch of System Center Configuration Manager at the time the technical preview version is made available. These features might eventually be included in an update to the current branch release, but before we finalize the features and add them, we want you to have a chance to try them out and give us feedback.  

 Because this is a technical preview, details and functionality are subject to change.  

 This topic contains information that applies to all versions of the Technical Preview, and also  lists each new capability (or feature) along with the  Technical Preview version in which the capability first appears, like version 1701 for January of 2017. The details for these capabilities are detailed in  separate topics dedicated to each preview version.  

 For information about what's new in the current branch of Configuration Manager, see [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requirements and limitations for the Technical Preview  

> [!IMPORTANT]     
>  The Technical Preview is licensed for use only in a lab environment.  Microsoft may not provide support services and certain features may not be available in the Preview software. Additionally, the Preview software may have reduced or different security, privacy, accessibility, availability and reliability standards relative to commercially provided software.  

 For most product prerequisites, use the information in the [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). The following exceptions apply to the Technical Preview releases:  

-   Each install remains active for 90 days before it becomes inactive.  

-   English is the only language supported.


-   Only the following install flags (switches) are supported:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   By default, when you use the technical preview, the service connection point is set to online mode when it installs, and does not support a change to offline mode.

-   When applicable, additional limitations or requirements are included with details for each specific version of the Technical Preview  

-   There is no support for migration to or from this preview build.  

-   There is no support for upgrade to this preview build.  

-   There is no support for upgrade to a production build (current branch) from this preview build. However, when updates are available for a preview version,  you can find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.  
-   Only a stand-alone primary site is supported. There is no support for a central administration site, multiple primary sites, or secondary sites.  

The following products and technologies are supported by this branch of Configuration Manager. However, their inclusion in this content does not imply an extension of support for a product or version that is beyond that product's individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information about Microsoft Support Lifecycles, visit the [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) website.  

-   Only the following versions of SQL Server are supported:  

    -   SQL Server 2016 (with no Service Pack, and later)
    -   SQL Server 2014 (with Service Pack 1, and later)
    -   SQL Server 2012 (with Service Pack 3, or later)


-   The site supports up to 10 clients, which must run one of the following:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Install and update the Technical Preview  
 The System Center Configuration Manager Technical Preview is distinct from the current release of System Center Configuration Manager.  

 To use the technical preview you must first install a **baseline version** of the technical preview build. After installing a baseline version, you then use **in-console updates** to bring your installation up to date with the most recent preview version.     Typically, new versions of the Technical Preview are available each month.

Each preview release is supported up until three successive releases are available. Meaning, when version 1702 releases, version 1610 would no longer be in support, but versions 1611, 1612, and 1701 would remain in support. When a baseline falls out of support (like version 1610), it is still supported for installing a new Technical Preview site until a new baseline version is available, so long as you then update that install to a supported version. When updating, if you don’t see the most recent version available in your console, update to the latest version offered and then repeat that process until you can install the most current version of the technical preview.

> [!TIP]  
>  When you install  an update to the  technical preview, you  update your preview installation to that new technical preview version.    A technical preview installation  never has the option to upgrade to a current branch installation, nor  receive updates from the current branch release.  

**Active baseline versions of the Technical Preview:**  
You can install a baseline version for up to 1 year after its release. However, when you install a new technical preview site, we recommend you use the latest baseline version that is available.
-  **Technical Preview 1703** - The Configuration Manager Technical Preview 1703 is available as both an in-console update for the Configuration Manager Technical Preview, and as a new baseline version that is [available from the TechNet Evaluation Center website](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-  **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 was available as both an in-console update for the Configuration Manager Technical Preview, and as a baseline version. If you have media for installing 1610, we recommend you download version 1703 and install that version instead.




##  <a name="BKMK_TPFeedback"></a> Providing feedback  
 We would love to hear your feedback about our technical previews. To submit feedback about the capabilities in each preview, follow the link to our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) page on the Microsoft Connect site.  

 And, if you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our user voice page](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capabilities delivered in the most recent technical preview  
 The following are the  capabilities delivered  with each Configuration Manager technical preview release.  Capabilities that are available beginning in a version of the technical preview remain available in later versions. Similarly, capabilities that have been added to the System Center Configuration Manager Release (current branch) remain  available in subsequent technical previews.  Click through to the content for each preview version to learn more about a specific capability.  

 |Capability |Technical Preview version |Current Branch version|  
 |----------------|---------------------|--------------------|
 |Client Peer Cache support for express installation files for Windows 10 and Office 365|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|![Not added](media/Red_X.gif)|
 |Surface Device dashboard|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![Not added](media/Red_X.gif)|
 |Configure and deploy Windows Defender Application Guard policies|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|![Not added](media/Red_X.gif)|
 |Add parameters when you deploy PowerShell scripts from Configuration Manager|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![Not added](media/Red_X.gif)|


## Capabilities delivered in previous technical previews
 When all features from a technical preview release are available in the minimum supported version of the Current Branch, details for that preview version are removed from the following table.  

 |Capability |Technical Preview version |Current Branch version|  
 |----------------|---------------------|--------------------|
 |New mobile application management policy settings|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![Not added](media/Red_X.gif)|
 |Improved boundary groups for software update points|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[Version 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |Site server role high availability|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Not added](media/Red_X.gif)|
 |Include trust for specific files and folders in a Device Guard policy|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|![Not added](media/Red_X.gif)|
 |Hide task sequence progress|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Not added](media/Red_X.gif)|
 |Specify a different content location for install content and uninstall content|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|![Not added](media/Red_X.gif)|
 |Accessibility improvements |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[Version 1706](/sccm/core/understand/accessibility-features)|
 |Azure Services Wizard support for Upgrade Readiness |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|![Not added](media/Red_X.gif)|
 |New client settings for cloud services|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|![Not added](media/Red_X.gif)|
 |Create and run PowerShell scripts from the Configuration Manager console|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|![Not added](media/Red_X.gif)|
 |PXE network boot support for IPv6 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Not added](media/Red_X.gif)|
 |Manage Microsoft Surface driver updates |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Configure Windows Update for Business deferral policies |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[Version 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |Android and iOS Enrollment Restrictions|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|![Not added](media/Red_X.gif)|
 |Android for Work application management policy for copy-paste|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|![Not added](media/Red_X.gif)|
 |New Windows configuration item settings|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|![Not added](media/Red_X.gif)|
 |New device compliance policy rules|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|![Not added](media/Red_X.gif)|
 |Device Health Attestation assessment for compliance policies for conditional access|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Not added](media/Red_X.gif)|
 |Support for Entrust certificate authorities|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|![Not added](media/Red_X.gif)|
 |Cisco (IPSec) support for macOS VPN profiles|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|![Not added](media/Red_X.gif)|

## Capabilities delivered in previous technical previews
 When all features from a technical preview release are available in the minimum supported version of the Current Branch, details for that preview version are removed from the following table.  

 |Capability |Technical Preview version |Current Branch version|  
 |----------------|---------------------|--------------------|
 |New capabilities for Azure AD and cloud management|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Configure and deploy Windows Defender Application Guard policies|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![Not added](media/Red_X.gif)|
 |Update reset tool  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[Version 1706](/sccm/core/servers/manage/update-reset-tool)|
 |High DPI console support  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |Peer Cache improvements  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[Version 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Improvements for SQL Server Always On Availability Groups |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[Version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Improved user notifications for Office 365 updates|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |![Not added](media/Red_X.gif)|
 |Use Azure Services Wizard to configure a connection to OMS|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |![Not added](media/Red_X.gif)|
 |Configure Android apps with app configuration policies  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Not added](media/Red_X.gif)|
 |Hardware inventory collects Secure Boot information |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![Not added](media/Red_X.gif)|
 |Add child task sequences to a task sequence|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Not added](media/Red_X.gif)|
 |Reload boot images with current Windows PE version |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![Not added](media/Red_X.gif)|
 |Improvements to operating system deployment|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Not added](media/Red_X.gif)|
 |Deploy volume-purchased iOS apps to device collections|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Version 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Direct links to applications in Software Center|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Not added](media/Red_X.gif)
 |PFX certificates for Configuration Manager Windows client computers|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Not added](media/Red_X.gif)|
 |Configure Azure Services wizard|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[Version 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Convert from BIOS to UEFI in an operating system upgrade task sequence| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Collapsible task sequence groups| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Not added](media/Red_X.gif)|
 |Client settings to configure Windows Analytics for Upgrade Readiness | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Not added](media/Red_X.gif)|
 |New compliance settings for iOS devices|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Version 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Create PFX certificates with S/MIME support|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Version 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Check for running executable files before installing an application|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Send feedback from the Configuration Manager console | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Changes for Updates and Servicing  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Peer Cache improvements  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Version 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Use Azure Active Directory  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Not added](media/Red_X.gif)|
 |Conditional access device compliance policy improvements | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Version 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Antimalware client version alert | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Version 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Compliance assessment for Windows Update for Business updates | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Not added](media/Red_X.gif)|
 |Improvements to Software Center settings and notification messages for high-impact task sequences|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Version 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android for Work support| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Version 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Boundary groups improvements for software update points | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Version 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |Hardware inventory collects UEFI information | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Improvements to operating system deployment| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Host software updates on cloud-based distribution points| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Not added](media/Red_X.gif) |
 |Validate device health attestation data via management points| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Version 1702](/sccm/core/servers/manage/health-attestation) |
 |OMS connector for Microsoft Azure Government cloud |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Version 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Android and iOS versions are no longer targetable in creation wizards |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Not added](media/Red_X.gif) |
 |OData endpoint data access |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Not added](media/Red_X.gif)|
 |Data Warehouse Service point |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Version 1702](/sccm/core/servers/manage/data-warehouse)|
 |Content library cleanup tool |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Version 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Improvements for in-console search |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Prevent installation of an application if a specified program is running|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |New Windows Hello for Business notification for end users|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Not added](media/Red_X.gif)|
 |Windows Store for Business support in Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Not added](media/Red_X.gif)|
 |Return to previous page when a task sequence fails|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Express installation files support for Windows 10 updates|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Version 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Azure Active Directory onboarding|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[Version 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Change to configuring multi-factor authentication for device enrollment|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Not added](media/Red_X.gif)|
 |Pre-cache content for deployments and task sequences |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Windows Defender configuration settings|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Request policy sync from administrator console|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Version 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Additional security role support for All Corporate-owned Devices node|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Version 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Conditional access for Windows 10 VPN profiles|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Version 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filter by content size in automatic deployment rules|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Improved functionality for required software dialogs|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Deny previously approved application requests|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Exclude clients from automatic upgrade|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Version 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Improvements to Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Version 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Increased number of enrolled devices|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Version 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Additional Apple DEP settings|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Version 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Enhancements to Windows Store for Business integration with Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Version 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |New compliance settings for configuration items|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integration with Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Version 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Native Connection Types for Windows 10 VPN Hybrid Profiles|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Not added](media/Red_X.gif)|
 |Improvements for boundary groups|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Version 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365 Client Management dashboard|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Version 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Deploy Office 365 apps to clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Version 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Improvements to BIOS to UEFI conversion|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Version 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune compliance charts|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Version 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Not added](media/Red_X.gif)|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Not added](media/Red_X.gif)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Not added](media/Red_X.gif)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Not added](media/Red_X.gif)|
 |Cloud management gateway (formerly Cloud Proxy Service)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Grace period for required application deployments |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Not added](media/Red_X.gif)|  
 |New experience for remote device actions |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Not added](media/Red_X.gif)|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Service a server group |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  

 <!--  TP 1604 and earlier has aged out of support and all features are in Current Branch builds:
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## See Also  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)
