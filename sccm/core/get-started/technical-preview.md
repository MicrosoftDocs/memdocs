---
title: "Technical Preview for System Center Configuration Manager | Microsoft Docs"
description: "Learn about the Technical Preview release that let's you test-drive new functionality and capabilities in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brendunsms.author: brendunsmanager: angrobe

---
# Technical Preview for System Center Configuration Manager*Applies to: System Center Configuration Manager (Technical Preview)*
**Welcome to the System Center Configuration Manager Technical Preview**. This topic provides details about the evolving preview release that introduces new functionality and capabilities we are working on. With each version of the technical preview, new features are introduced that are not included in the current branch of System Center Configuration Manager at the time the technical preview version is made available. These features might eventually be included in an update to the current branch release, but before we finalize the features and add them, we want you to have a chance to try them out and give us feedback.  

 Because this is a technical preview, details and functionality are subject to change.  

 This topic contains information that applies to all versions of the Technical Preview, and also  lists each new capability (or feature) along with the  Technical Preview version in which the capability first appears, like version 1512 for December of 2015. The details for these capabilities are detailed in  separate topics dedicated to each preview version.  

 For information about what's new in the current branch of Configuration Manager, see [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requirements and limitations for the Technical Preview  

> [!IMPORTANT]  
>  The Technical Preview is licensed for use only in a lab environment.  Microsoft may not provide support services and certain features may not be available in the Preview software. Additionally, the Preview software may have reduced or different security, privacy, accessibility, availability and reliability standards relative to commercially provided software.  

 For most product prerequisites, use the information in the [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). The following exceptions apply to the Technical Preview releases:  

-   Each install remains active for 90 days before it becomes inactive.  

-   English is the only language supported.  

-   Only a stand-alone primary site is supported. There is no support for a central administration site, multiple primary sites, or secondary sites.  

-   Only the following versions of SQL Server are supported:  

    -   SQL Server 2012 with cumulative update 2 or later  

    -   SQL Server 2014  

-   The site supports up to 10 clients, which must run one of the following:  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   Only the following install flags (switches) are supported:  

    -   **/silent**  

    -   **/testdbupgrade**  

-   When applicable, additional limitations or requirements are included with details for each specific version of the Technical Preview  

-   There is no support for migration to or from this preview build.  

-   There is no support for upgrade to this preview build.  

-   There is no support for upgrade to a production build (current branch) from this preview build. However, when updates are available for a preview version,  you can find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.  

##  <a name="bkmk_install"></a> Install and update the Technical Preview  
 The System Center Configuration Manager Technical Preview is distinct from the current release of System Center Configuration Manager.  

 To use the technical preview you must first install a **baseline version** of the technical preview build. After installing a baseline version, you then use **in-console updates** to bring your installation up to date with the most recent preview version.     Typically, new versions of the Technical Preview are available each month.  

> [!TIP]  
>  When you install  an update to the  technical preview, you  update your preview installation to that new technical preview version.    A technical preview installation  never has the option to upgrade to a current branch installation, nor  receive updates from the current branch release.  

 **Active baseline versions of the Technical Preview:**  
 You can install a baseline version for up to 1 year after its release.

-   **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 is available as both an in-console update for the Configuration Manager Technical Preview, and as a new baseline version that is available from the [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) website.

-   **Technical Preview 1603** as part of the **System Center Technical Preview 5** -  The Configuration Manager Technical Preview 1603  is available as both an in-console update for the Configuration Manager Technical Preview, and as a new baseline version that is included with System Center Technical Preview 5.    Only the version included with System Center Technical Preview 5 can be used for a baseline install.  

     About  the baseline version of the [Configuration Manager Technical Preview from System Center Technical Preview 5](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview):  

    -   Both Setup and the Configuration Manager console list the version as the System Center Configuration Manager Technical Preview 1603.  

    -   This baseline version functions as does the Configuration Manager Technical Preview 1603, including support for in-console updates.  


##  <a name="BKMK_TPFeedback"></a> Providing feedback  
 We would love to hear your feedback about our technical previews. To submit feedback about the capabilities in each preview, follow the link to our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) page on the Microsoft Connect site.  

 And, if you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our user voice page](http://configurationmanager.uservoice.com).  

##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews  

-   **Technical Preview 1603:**  

    -   Beginning with Technical Preview 1603, you can configure software updates deployments to have clients run a software updates compliance scan immediately after a client installs software updates and restarts. This enables the client to check for additional software updates that become applicable after the client restarts, and to then install them (and become compliant) during the same maintenance window.  

         To configure this for a deployment, on the **User Experience** page of the Deploy Software Updates Wizard select the option **If any update in this deployment requires a system restart, run updates deployment evaluation cycle after restart**.  

    -   Beginning with Technical Preview 1603, the behavior for the SMSTSRebootDelay task sequence variable has changed. The  SMSTSRebootDelay variable specifies how many seconds to wait before the computer restarts. The task sequence manager will display a notification dialog before the restart if this variable is not set to 0.  
        When you configure a value for this variable, that value will persist until you configure a new value. The delay for all the subsequent computer restarts will have the same value. In Configuration Manager version 1602 and earlier, the variable is reset to the default value (30 seconds) after the computer restarts.   For more information, see [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).

-   **Technical Preview 1602:** Beginning with Technical Preview 1602, you can in-place upgrade the operating system of a site system server that runs Windows 2008 Server R2 to Windows 2012 Server R2.  When you use the Windows Server 2012 R2 upgrade procedures, you do not need to run a Configuration Manager site server restore after the upgrade.  For upgrade procedures, see [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Before you upgrade to Windows Server 2012 R2, **you must uninstall WSUS 3.2** from the server.  
    >   
    >  For information about this critical step, see the New and changed functionality section  in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx) in the Windows Server documentation.  

-   **Technical Preview 1601:** By default, the service connection point is set to online mode when it installs, and does not support a change to offline mode.  





##  <a name="bkmk_tpCaps"></a> Capabilities delivered in technical previews  
 The following are the  capabilities delivered  with each Configuration Manager technical preview release.  Capabilities that are available beginning in a version of the technical preview remain available in later versions. Similarly, capabilities that have been added to the System Center Configuration Manager Release (current branch) remain  available in subsequent technical previews.  Click through to the content for each preview version to learn more about a specific capability.  

 |Capability|Technical Preview version|Current Branch version|  
 |----------------|---------------------|--------------------|
 |Windows Defender configuration settings|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Request policy sync from administrator console|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Version 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Additional security role support for All Corporate-owned Devices node|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|![Not added](media/Red_X.gif)|
 |Conditional access for Windows 10 VPN profiles|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|![Not added](media/Red_X.gif)|
 |Filter by content size in automatic deployment rules|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Improved functionality for required software dialogs|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Deny previously approved application requests|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Exclude clients from automatic upgrade|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![Not added](media/Red_X.gif)|
 |Improvements to Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Not added](media/Red_X.gif)|
 |Increased number of enrolled devices|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Not added](media/Red_X.gif)|
 |Additional Apple DEP settings|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![Not added](media/Red_X.gif)|
 |Enhancements to Windows Store for Business integration with Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Version 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |New compliance settings for configuration items|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integration with Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![Not added](media/Red_X.gif)|
 |Native Connection Types for Windows 10 VPN Hybrid Profiles|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Not added](media/Red_X.gif)|
 |Improvements for boundary groups|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Version 1610](sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)|
 |Office 365 Client Management dashboard|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Version 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Deploy Office 365 apps to clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![Not added](media/Red_X.gif)|
 |Improvements to BIOS to UEFI conversion|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|[Version 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune compliance charts|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Version 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![Not added](media/Red_X.gif)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Not added](media/Red_X.gif)|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Not added](media/Red_X.gif)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![Not added](media/Red_X.gif)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Not added](media/Red_X.gif)|
 |Cloud Proxy Service|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![Not added](media/Red_X.gif)|  
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
 |Improvements to mobile device management|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[Version 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |Improvements to Software Center in version 1602|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Improvements to Windows 10 Servicing|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Improvements to Microsoft Intune integration|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |Client online status|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[Version 1602](/sccm/core/clients/manage/monitor-clients)|
 |Improvements to application management|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |Improvements to compliance settings|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |Device Health Attestation|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[Version 1602](/sccm/core/servers/manage/health-attestation))|
 |In-console monitoring for terms and conditions|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[Version 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Improvements to Endpoint Protection policy settings|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[Version 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Integration with Windows Update for Business in Windows 10|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[Version 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |Managing Office 365 ProPlus Client Update through System Center Configuration Manager|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[Version 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |Support for SQL Server AlwaysOn for highly available databases|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[Version 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |Service a server cluster|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## See Also  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)
