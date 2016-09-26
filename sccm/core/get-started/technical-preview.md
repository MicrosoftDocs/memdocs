---
title: "Technical Preview for System Center Configuration Manager"
description: "Learn about the Technical Preview release that let's you test-drive new functionality and capabilities in System Center Configuration Manager."
ms.custom: na
ms.date: 08/22/2016
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

---
# Technical Preview for System Center Configuration Manager
**Welcome to the System Center Configuration Manager Technical Preview**. This topic provides details about the evolving preview release that introduces new functionality and capabilities we are working on. With each version of the technical preview, new features are introduced that are not included in the current branch of System Center Configuration Manager at the time the technical preview version is made available. These features might eventually be included in an update to the current branch release, but before we finalize the features and add them, we want you to have a chance to try them out and give us feedback.  

 Because this is a technical preview, details and functionality are subject to change.  

 This topic contains information that applies to all versions of the Technical Preview, and also  lists each new capability (or feature) along with the  Technical Preview version in which the capability first appears, like version 1512 for December of 2015. The details for these capabilities are detailed in  separate topics dedicated to each preview version.  

 For information about what's new in the current branch of Configuration Manager, see [What's new in System Center Configuration Manager](What%E2%80%99s%20new%20in%20System%20Center%20Configuration%20Manager%20incremental%20versions.md).

> [!NOTE]  
>  For information about what's in System Center Configuration Manager Technical Preview 4 (and earlier previews), see [Technical Previews for the pre-release of System Center Configuration Manager](https://technet.microsoft.com/library/dn965439.aspx)  



##  <a name="bkmk_reqs"></a> Requirements and limitations for the Technical Preview  

> [!IMPORTANT]  
>  The Technical Preview is licensed for use only in a lab environment.  Microsoft may not provide support services and certain features may not be available in the Preview software. Additionally, the Preview software may have reduced or different security, privacy, accessibility, availability and reliability standards relative to commercially provided software.  

 For most product prerequisites, use the information in the [!INCLUDE[cm6long] (../Token/cm6long_md.md)] [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). The following exceptions apply to the Technical Preview releases:  

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

-   **Technical Preview 1603** as part of the **System Center Technical Preview 5** -  The Configuration Manager Technical Preview 1603  is available as both an in-console update for the Configuration Manager Technical Preview, and as a new baseline version that is included with System Center Technical Preview 5.    Only the version included with System Center Technical Preview 5 can be used for a baseline install.  

     About  the baseline version of the [Configuration Manager Technical Preview from System Center Technical Preview 5](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview):  

    -   Both Setup and the Configuration Manager console list the version as the System Center Configuration Manager Technical Preview 1603.  

    -   This baseline version functions as does the Configuration Manager Technical Preview 1603, including support for in-console updates.  

    -   You can install this baseline version for up to 9 months after the release of System Center Technical Preview 5.  

    -   You can run this baseline version for 90 days before you must update it to a later version. (Typically, versions of the Configuration Manager Technical Preview run for 60 days before you must update them to a later version.)  

##  <a name="BKMK_TPFeedback"></a> Providing feedback  
 We would love to hear your feedback about our technical previews. To submit feedback about the capabilities in each preview, follow the link to our feedback form on the [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) page on the Microsoft Connect site.  

 And, if you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our user voice page](http://configurationmanager.uservoice.com).  

##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews  

-   **Technical Preview 1601:** By default, the service connection point is set to online mode when it installs, and does not support a change to offline mode.  

-   **Technical Preview 1602:** Beginning with Technical Preview 1602, you can in-place upgrade the operating system of a site system server that runs Windows 2008 Server R2 to Windows 2012 Server R2.  When you use the Windows Server 2012 R2 upgrade procedures, you do not need to run a Configuration Manager site server restore after the upgrade.  For upgrade procedures, see [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Before you upgrade to Windows Server 2012 R2, **you must uninstall WSUS 3.2** from the server.  
    >   
    >  For information about this critical step, see the New and changed functionality section  in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx) in the Windows Server documentation.  

-   **Technical Preview 1603:**  

    -   Beginning with Technical Preview 1603, you can configure software updates deployments to have clients run a software updates compliance scan immediately after a client installs software updates and restarts. This enables the client to check for additional software updates that become applicable after the client restarts, and to then install them (and become compliant) during the same maintenance window.  

         To configure this for a deployment, on the **User Experience** page of the Deploy Software Updates Wizard select the option **If any update in this deployment requires a system restart, run updates deployment evaluation cycle after restart**.  

    -   Beginning with Technical Preview 1603, the behavior for the SMSTSRebootDelay task sequence variable has changed. The  SMSTSRebootDelay variable specifies how many seconds to wait before the computer restarts. The task sequence manager will display a notification dialog before the restart if this variable is not set to 0.  
        When you configure a value for this variable, that value will persist until you configure a new value. The delay for all the subsequent computer restarts will have the same value. In Configuration Manager version 1602 and earlier, the variable is reset to the default value (30 seconds) after the computer restarts.   For more information, see [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).  

##  <a name="bkmk_tpCaps"></a> Capabilities delivered in technical previews  
 The following are the  capabilities delivered  with each Configuration Manager technical preview release.  Capabilities that are available beginning in a version of the technical preview remain available in later versions. Similarly, capabilities that have been added to the System Center Configuration Manager Release (current branch) remain  available in subsequent technical previews.  Click through to the content for each preview version to learn more about a specific capability.  

 |Capability|Technical Preview version|Current Branch version|  
 |----------------|---------------------|--------------------|
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](Capabilities%20in%20Technical%20Preview%201608%20for%20System%20Center%20Configuration%20Manager.md#Improvements-to-the-Prepare-ConfigMgr-Client-for-Capture-task-sequence-step)|![Not added](media/Red_X.gif)|
 |Improvements to Software Center|[Tech Preview 1608](Capabilities%20in%20Technical%20Preview%201608%20for%20System%20Center%20Configuration%20Manager.md#Improvements-to-Software-Center)|![Not added](media/Red_X.gif)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](Capabilities%20in%20Technical%20Preview%201608%20for%20System%20Center%20Configuration%20Manager.md#Improvements-to-Asset-Intelligence)|![Not added](media/Red_X.gif)|
 |Remote control keyboard translation|[Tech Preview 1608](Capabilities%20in%20Technical%20Preview%201608%20for%20System%20Center%20Configuration%20Manager.md#Remote-control-keyboard-translation)|![Not added](media/Red_X.gif)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](Capabilities%20in%20Technical%20Preview%201607%20for%20System%20Center%20Configuration%20Manager.md#dmp_edition)|![Not added](media/Red_X.gif)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](Capabilities%20in%20Technical%20Preview%201607%20for%20System%20Center%20Configuration%20Manager.md#Customizable-Branding-for-Software-Center-Dialogs)|![Not added](media/Red_X.gif)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](../Topic/Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#dmp_onprem)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#On-premises-Mobile-Device-Management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](../Topic/Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#dmp_category)|[Release 1606](How%20to%20automatically%20categorize%20devices%20into%20collections%20with%20System%20Center%20Configuration%20Manager.md) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](../Topic/Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#dmp_grace)|![Not added](media/Red_X.gif)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](../Topic/Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#dmp_devg)|![Not added](media/Red_X.gif)|
 |Cloud Proxy Service|[Tech Preview 1606](Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#cloud_proxy) | ![Not added](media/Red_X.gif)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#manage_o365) |[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#osdpreservedriveletter) |[Release 1606](Task%20sequence%20built-in%20variables%20in%20System%20Center%20Configuration%20Manager.md) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](Capabilities%20in%20Technical%20Preview%201606%20for%20System%20Center%20Configuration%20Manager.md#updatesandservicing)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Updates-and-Servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_PerAppVPN)|[Release 1606](How%20to%20Create%20VPN%20profiles%20in%20System%20Center%20Configuration%20Manager.md)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_InstallSU)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_PrepareConfigMgrClient)|![Not added](media/Red_X.gif) |
 |Grace period for required application deployments |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_Grace)|![Not added](media/Red_X.gif)|  
 |New experience for remote device actions |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_Remote)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_WSFB)|[Release 1606](Manage%20apps%20from%20the%20Windows%20Store%20for%20Business%20with%20System%20Center%20Configuration%20Manager.md)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_VPP2)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_VPP)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_End)|![Not added](media/Red_X.gif)|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_SW1)|[Release 1606 ](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Application-management)|  
 |Service a server group |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_ServerGroups)|[Release 1606](Service%20a%20server%20group.md)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_ATP)|[Release 1606](Windows%20Defender%20Advanced%20Threat%20Protection.md)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_RestartOptions)|[Release 1606](Plan%20for%20software%20updates%20in%20System%20Center%20Configuration%20Manager.md#Restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_DHA)|[Release 1606](Health%20attestation%20for%20System%20Center%20Configuration%20Manager.md)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](../Topic/Capabilities%20in%20Technical%20Preview%201605%20for%20System%20Center%20Configuration%20Manager.md#BKMK_IMEI)|[Release 1606](Predeclare%20devices%20with%20IMEI%20or%20iOS%20serial%20numbers.md)|  
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#BKMK_WindowsVPP)|[Release 1606](Manage%20apps%20from%20the%20Windows%20Store%20for%20Business%20with%20System%20Center%20Configuration%20Manager.md)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#BKMK_PFW)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#bkmk_switchsup)|[Release 1606](Plan%20for%20software%20updates%20in%20System%20Center%20Configuration%20Manager.md#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#bkmk_peercache)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Administration)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#bkmk_passport)|[Release 1606](How%20to%20create%20certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#bkmk_onpremdha)|[Release 1606](Health%20attestation%20for%20System%20Center%20Configuration%20Manager.md)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](../Topic/Capabilities%20in%20Technical%20Preview%201604%20for%20System%20Center%20Configuration%20Manager.md#BKMK_Smart)|[Release 1606](How%20to%20create%20configuration%20items%20for%20Android%20and%20Samsung%20KNOX%20devices%20managed%20without%20the%20System%20Center%20Configuration%20Manager%20client.md#Android-and-Samsung-KNOX-configuration-item-settings-reference)|  
 |Improvements to Software Center in the 1603 release|[Tech Preview 1603](../Topic/Capabilities%20in%20Technical%20Preview%201603%20for%20System%20Center%20Configuration%20Manager.md#BKMK_SC1603)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Application-management)|  
 |Improvements to remote control|[Tech Preview 1603](../Topic/Capabilities%20in%20Technical%20Preview%201603%20for%20System%20Center%20Configuration%20Manager.md#BKMK_RC1603)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Remote-Control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](../Topic/Capabilities%20in%20Technical%20Preview%201603%20for%20System%20Center%20Configuration%20Manager.md#BKMK_RamDiskTFTP)|[Release 1606](What's%20new%20in%20version%201606%20of%20System%20Center%20Configuration%20Manager.md#Operating-system-deployment)|  
 |Improvements to mobile device management]|[Tech Preview 1602](../Topic/Capabilities%20in%20Technical%20Preview%201602%20for%20System%20Center%20Configuration%20Manager.md#BKMK_MDM)|[Release 1602](Help%20protect%20iOS%20devices%20with%20Activation%20Lock%20bypass%20for%20Configuration%20Manager.md) |  
 |Improvements to Software Center in the 1602 release|[Tech Preview 1602](../Topic/Capabilities%20in%20Technical%20Preview%201602%20for%20System%20Center%20Configuration%20Manager.md#BKMK_SC1601)| [Release 1602](What's%20new%20in%20version%201602%20of%20System%20Center%20Configuration%20Manager.md#Client-management)|  
 |Improvements to Windows 10 Servicing|[Tech Preview 1602](../Topic/Capabilities%20in%20Technical%20Preview%201602%20for%20System%20Center%20Configuration%20Manager.md#BKMK_Win10Servicing)|[Release 1602](What's%20new%20in%20version%201602%20of%20System%20Center%20Configuration%20Manager.md#Operating-system-deployment) |  
 |Improvements to Microsoft Intune integration|[Tech Preview 1601](../Topic/Capabilities%20in%20Technical%20Preview%201601%20for%20System%20Center%20Configuration%20Manager.md#bkmk_hybrid1)|[Release 1602](What's%20new%20in%20version%201602%20of%20System%20Center%20Configuration%20Manager.md#Conditional-access)|  
 |Client online status|[Tech Preview 1601](../Topic/Capabilities%20in%20Technical%20Preview%201601%20for%20System%20Center%20Configuration%20Manager.md#bkmk_clientStatus)|[Release 1602](How%20to%20monitor%20clients%20in%20System%20Center%20Configuration%20Manager.md)|
 |Improvements to application management|[Tech Preview 1601](../Topic/Capabilities%20in%20Technical%20Preview%201601%20for%20System%20Center%20Configuration%20Manager.md#bkmk_appmgmt1601)|[Release 1602](What's%20new%20in%20version%201602%20of%20System%20Center%20Configuration%20Manager.md#Application-management)|  
 |Improvements to compliance settings|[Tech Preview 1601](../Topic/Capabilities%20in%20Technical%20Preview%201601%20for%20System%20Center%20Configuration%20Manager.md#bkmk_compliance1601)|[Release 1602](What's%20new%20in%20version%201602%20of%20System%20Center%20Configuration%20Manager.md#Compliance-settings)|  
 |Device Health Attestation|[Tech Preview 1512](../Topic/Capabilities%20in%20Technical%20Preview%201512%20for%20System%20Center%20Configuration%20Manager.md#bkmk_devicehealth)|[Release 1602](Health%20attestation%20for%20System%20Center%20Configuration%20Manager.md)|
 |In-console monitoring for terms and conditions|[Tech Preview 1512](../Topic/Capabilities%20in%20Technical%20Preview%201512%20for%20System%20Center%20Configuration%20Manager.md#bkmk_viewterms)|[Release 1602](Terms%20and%20Conditions%20in%20System%20Center%20Configuration%20Manager.md)|  
 |Improvements to Endpoint Protection policy settings|[Tech Preview 1512](../Topic/Capabilities%20in%20Technical%20Preview%201512%20for%20System%20Center%20Configuration%20Manager.md#bkmk_EPpolicy)|[Release 1602](How%20to%20create%20and%20deploy%20antimalware%20policies%20for%20Endpoint%20Protection%20in%20System%20Center%20Configuration%20Manager.md)|  
 |Integration with Windows Update for Business in Windows 10|[Tech Preview 1511](../Topic/Capabilities%20in%20Technical%20Preview%201511%20for%20System%20Center%20Configuration%20Manager.md#BKMK_WUfB)|[Release 1602](Integration%20with%20Windows%20Update%20for%20Business%20in%20Windows%2010.md)|  
 |Managing Office 365 ProPlus Client Update through System Center Configuration Manager|[Tech Preview 1511](../Topic/Capabilities%20in%20Technical%20Preview%201511%20for%20System%20Center%20Configuration%20Manager.md#BKMK_Office365ProPlus)|[Release 1602](Manage%20Office%20365%20ProPlus%20updates%20with%20Configuration%20Manager.md)|  
 |Support for SQL Server AlwaysOn for highly available databases|[Tech Preview 1511](../Topic/Capabilities%20in%20Technical%20Preview%201511%20for%20System%20Center%20Configuration%20Manager.md#BKMK_AlwasyOn)|[Release 1602](SQL%20Server%20AlwaysOn%20for%20a%20highly%20available%20site%20database%20for%20System%20Center%20Configuration%20Manager.md)|  
 |Service a server cluster|[Tech Preview 1511](../Topic/Capabilities%20in%20Technical%20Preview%201511%20for%20System%20Center%20Configuration%20Manager.md#BKMK_ClusterServerUpdates)|[Release 1606](Service%20a%20server%20group.md)|  
## See Also  
[What's new in System Center Configuration Manager](What%E2%80%99s%20new%20in%20System%20Center%20Configuration%20Manager%20incremental%20versions.md)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)
