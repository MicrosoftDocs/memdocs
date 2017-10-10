---
title: "Log files for Configuration Manager"
description: "Use log files to troubleshoot issues in a System Center Configuration Manager hierarchy."
ms.custom: na
ms.date: 7/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Log files in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager, client and site server components record process information in individual log files. You can use the information in the log files to help you troubleshoot issues that might occur in your Configuration Manager hierarchy. By default, client and server component logging is enabled in Configuration Manager.   

 The following sections provide details about the different log files available to you. You can use this information to view and monitor Configuration Manager client and server logs for operation details, and to identify error information that might help you troubleshoot any problems.  

-   [About Configuration Manager log files](#BKMK_AboutLogs)  

    -   [Configure logging options by using Configuration Manager Service Manager](#BKMK_LogOptions)  

    -   [Locating Configuration Manager logs](#BKMK_LogLocation)  

-   [Configuration Manager client logs](#BKMK_ClientLogs)  

    -   [Client operations](#BKMK_ClientOpLogs)  

    -   [Client installation log files](#BKMK_ClientInstallLog)  

    -   [Client for Linux and UNIX](#BKMK_LogFilesforLnU)  

    -   [Client for Mac computers](#BKMK_LogfilesforMac)  

-   [Configuration Manager site server log files](#BKMK_ServerLogs)  

    -   [Site server and site system server logs](#BKMK_SiteSiteServerLog)  

    -   [Site server installation log files](#BKMK_SiteInstallLog)  

    -   [Fallback status point log files](#BKMK_FSPLog)  

    -   [Management point log files](#BKMK_MPLog)  

    -   [Software update point log files](#BKMK_SUPLog)  

-   [Log files for Configuration Manager functionality](#BKMK_FunctionLogs)  

    -   [Application management](#BKMK_AppManageLog)  

    -   [Asset intelligence](#BKMK_AILog)  

    -   [Backup and recovery](#BKMK_BnRLog)  

    -   [Certificate enrollment](#BKMK_CertificateEnrollment)

    -   [Client notification](#BKMK_BGB)

    -   [Cloud management gateway](#cloud-management-gateway)

    -   [Compliance settings and company resource access](#BKMK_CompSettingsLog)  

    -   [Configuration Manager console](#BKMK_ConsoleLog)  

    -   [Content management](#BKMK_ContentLog)  

    -   [Discovery](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensions](#BKMK_Extensions)  

    -   [Inventory](#BKMK_InventoryLog)  

    -   [Metering](#BKMK_MeteringLog)  

    -   [Migration](#BKMK_MigrationLog)  

    -   [Mobile devices](#BKMK_MDMLog)  

    -   [Operating system deployment](#BKMK_OSDLog)  

    -   [Power management](#BKMK_PowerMgmtLog)  

    -   [Remote control](#BKMK_RCLog)  

    -   [Reporting](#BKMK_ReportLog)  

    -   [Role-based administration](#BKMK_RBALog)  

    -   [Service connection point](#BKMK_WITLog)  

    -   [Software updates](#BKMK_SU_NAPLog)  

    -   [Wake On LAN](#BKMK_WOLLog)  

    -   [Windows 10 servicing](#BKMK_WindowsServicingLog)

    -   [Windows Update Agent](#BKMK_WULog)  

    -   [WSUS server](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a> About Configuration Manager log files  
 Most processes in Configuration Manager write operational information to a log file that is dedicated to that process. The log files are identified by **.log** or **.lo_** file extensions. Configuration Manager writes to a .log file until that log reaches its maximum size. When the log is full, the .log file is copied to a file of the same name but with the .lo_ extension, and the process or component continues to write to the .log file. When the .log file again reaches its maximum size, the .lo_ file is overwritten and the process repeats. Some components establish a log file history by appending a date and time stamp to the log file name and by retaining the .log extension. An exception to the maximum size and use of the .lo_ file is the client for Linux and UNIX. For information about how the client for Linux and UNIX uses log files, see [Manage log files in the client for Linux and UNIX](#BKMK_ManageLinuxLogs) in this topic.  

 To view the logs, use the Configuration Manager log viewer tool CMTrace, located in the \\SMSSetup\\Tools folder of the Configuration Manager source media. The CMTrace tool is added to all boot images that are added to the Software Library.  

###  <a name="BKMK_LogOptions"></a> Configure logging options by using Configuration Manager Service Manager  
 In Configuration Manager, you can change where log files are stored, and you can change the log file size.  

 To modify the size of log files, change the name and location of the log file, or to force multiple components to write to a single log file, do the following steps.  

#### To modify logging for a component  

1.  In the Configuration Manager console, select **Monitoring**, select **System Status**, and then select either **Site Status** or **Component Status**.  
2.  On the **Home** tab, in the **Component** group, select **Start**, and then select **Configuration Manager Service Manager**.  
3.  When Configuration Manager Service Manager opens, connect to the site that you want to manage. If the site that you want to manage isn't shown, select **Site**, select **Connect**, and then enter the name of the site server for the correct site.  
4.  Expand the site and go to **Components** or **Servers**, depending on where the components that you want to manage are located.  
5.  In the right pane, select one or more components.  
6.  On the **Component** menu, select **Logging**.  
7.  In the **Configuration Manager Component Logging** dialog box, complete the available configuration options for your selection.  
8.  Select **OK** to save the configuration.  

###  <a name="BKMK_LogLocation"></a> Find Configuration Manager logs  
Configuration Manager log files are stored in various locations that depend on the process that creates the log file and on the configuration of your site systems. Because the location of the log on a computer can vary, use the search function to find the relevant log files on your Configuration Manager computers if you need to troubleshoot a specific scenario.  

##  <a name="BKMK_ClientLogs"></a> Configuration Manager client logs  
The following sections list the log files related to client operations and client installation.  

###  <a name="BKMK_ClientOpLogs"></a> Client operations  
The following table lists the log files located on the Configuration Manager client.  

|Log name|Description|  
|--------------|-----------------|  
|CAS.log|The Content Access service. Maintains the local package cache on the client.|  
|Ccm32BitLauncher.log|Records actions for starting applications on the client marked "run as 32bit".|  
|CcmEval.log|Records Configuration Manager client status evaluation activities and details for components that are required by the Configuration Manager client.|  
|CcmEvalTask.log|Records the Configuration Manager client status evaluation activities that are initiated by the evaluation scheduled task.|  
|CcmExec.log|Records activities of the client and the SMS Agent Host service. This log file also includes information about enabling and disabling wake-up proxy.|  
|CcmMessaging.log|Records activities related to communication between the client and management points.|  
|CCMNotificationAgent.log|Records activities related to client notification operations.|  
|Ccmperf.log|Records activities related to the maintenance and capture of data related to client performance counters.|  
|CcmRestart.log|Records client service restart activity.|  
|CCMSDKProvider.log|Records activities for the client SDK interfaces.|  
|CertificateMaintenance.log|Maintains certificates for Active Directory Domain Services and management points.|  
|CIDownloader.log|Records details about configuration item definition downloads.|  
|CITaskMgr.log|Records tasks that are initiated for each application and deployment type, such as content download and install or uninstall actions.|  
|ClientAuth.log|Records signing and authentication activity for the client.|  
|ClientIDManagerStartup.log|Creates and maintains the client GUID and identifies tasks performed during client registration and assignment.|  
|ClientLocation.log|Records tasks that are related to client site assignment.|  
|CMHttpsReadiness.log|Records the results of running the Configuration Manager HTTPS Readiness Assessment Tool. This tool checks whether computers have a public key infrastructure (PKI) client authentication certificate that can be used with Configuration Manager.|  
|CmRcService.log|Records information for the remote control service.|  
|ContentTransferManager.log|Schedules the Background Intelligent Transfer Service (BITS) or Server Message Block (SMB) to download or access packages.|  
|DataTransferService.log|Records all BITS communication for policy or package access.|  
|EndpointProtectionAgent|Records information about the installation of the System Center Endpoint Protection client and the application of antimalware policy to that client.|  
|execmgr.log|Records details about packages and task sequences that run on the client.|  
|ExpressionSolver.log|Records details about enhanced detection methods that are used when verbose or debug logging is turned on.|  
|ExternalEventAgent.log|Records the history of Endpoint Protection malware detection and events related to client status.|  
|FileBITS.log|Records all SMB package access tasks.|  
|FileSystemFile.log|Records the activity of the Windows Management Instrumentation (WMI) provider for software inventory and file collection.|  
|FSPStateMessage.log|Records the activity for state messages that are sent to the fallback status point by the client.|  
|InternetProxy.log|Records the network proxy configuration and use activity for the client.|  
|InventoryAgent.log|Records activities of hardware inventory, software inventory, and heartbeat discovery actions on the client.|  
|LocationCache.log|Records the activity for location cache use and maintenance for the client.|  
|LocationServices.log|Records the client activity for locating management points, software update points, and distribution points.|  
|MaintenanceCoordinator.log|Records the activity for general maintenance tasks for the client.|  
|Mifprovider.log|Records the activity of the WMI provider for Management Information Format (MIF) files.|  
|mtrmgr.log|Monitors all software metering processes.|  
|PolicyAgent.log|Records requests for policies made by using the Data Transfer Service.|  
|PolicyAgentProvider.log|Records policy changes.|  
|PolicyEvaluator.log|Records details about the evaluation of policies on client computers, including policies from software updates.|  
|PolicyPlatformClient.log|Records the process of remediation and compliance for all providers located in \Program Files\Microsoft Policy Platform, except the file provider.|  
|PolicySdk.log|Records activities for policy system SDK interfaces.|  
|Pwrmgmt.log|Records information about enabling or disabling and configuring the wake-up proxy client settings.|  
|PwrProvider.log|Records the activities of the power management provider (PWRInvProvider) hosted in the WMI service. On all supported versions of Windows, the provider enumerates the current settings on computers during hardware inventory and applies power plan settings.|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_1.log|Records the activity in Software Center for the specified user on the client computer.|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_2.log|Records the historical activity in Software Center for the specified user on the client computer.|  
|Scheduler.log|Records activities of scheduled tasks for all client operations.|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1.log|Records the activity for notifying users about software for the specified user.|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1-&lt;*date_time*>.log|Records the historical information for notifying users about software for the specified user.|  
|setuppolicyevaluator.log|Records configuration and inventory policy creation in WMI.|  
|SleepAgent_&lt;*domain*\>@SYSTEM_0.log|The main log file for wake-up proxy.|  
|smscliui.log|Records use of the Configuration Manager client in Control Panel.|  
|SrcUpdateMgr.log|Records activity for installed Windows Installer applications that are updated with current distribution point source locations.|  
|StatusAgent.log|Records status messages that are created by the client components.|  
|SWMTRReportGen.log|Generates a use data report that is collected by the metering agent. This data is logged in Mtrmgr.log.|  
|UserAffinity.log|Records details about user device affinity.|  
|VirtualApp.log|Records information specific to the evaluation of Application Virtualization (App-V) deployment types.|  
|Wedmtrace.log|Records operations related to write filters on Windows Embedded clients.|  
|wakeprxy-install.log|Records installation information when clients receive the client setting option to turn on wake-up proxy.|  
|wakeprxy-uninstall.log|Records information about uninstalling wake-up proxy when clients receive the client setting option to turn off wake-up proxy, if wake-up proxy was previously turned on.|  

###  <a name="BKMK_ClientInstallLog"></a> Client installation log files  
 The following table lists the log files that contain information related to the installation of the Configuration Manager client.  

|Log name|Description|  
|--------------|-----------------|  
|ccmsetup.log|Records ccmsetup.exe tasks for client setup, client upgrade, and client removal. Can be used to troubleshoot client installation problems.|  
|ccmsetup-ccmeval.log|Records ccmsetup.exe tasks for client status and remediation.|  
|CcmRepair.log|Records the repair activities of the client agent.|  
|client.msi.log|Records setup tasks performed by client.msi. Can be used to troubleshoot client installation or removal problems.|  

###  <a name="BKMK_LogFilesforLnU"></a> Client for Linux and UNIX  
 The Configuration Manager client for Linux and UNIX records information in the following log files.  

> [!TIP]  
>  Beginning with clients for Linux and UNIX from Cumulative Update 1, you can use CMTrace to view the log files for the client for Linux and UNIX.  

> [!NOTE]  
>  When you use the initial release of the client for Linux and UNIX and reference the documentation in this section, replace the following references for each file or process:  
>   
>  -   Replace **omiserver.bin** with **nwserver.bin**  
> -   Replace **omi** with **nanowbem**  

|Log name|Details|  
|--------------|-------------|  
|Scxcm.log|The log file for the core service of the Configuration Manager client for Linux and UNIX (ccmexec.bin). This log file contains information about the installation and ongoing operations of ccmexec.bin.<br /><br /> By default, this log file is located at **/var/opt/microsoft/scxcm.log**<br /><br /> To change the location of the log file, edit **/opt/microsoft/configmgr/etc/scxcm.conf** and change the **PATH** field. You do not need to restart the client computer or service for the change to take effect.<br /><br /> You can set the log level to one of four different settings.|  
|Scxcmprovider.log|The log file for the CIM service of the Configuration Manager client for Linux and UNIX (omiserver.bin). This log file contains information about the ongoing operations of nwserver.bin.<br /><br /> This log is located at**/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> To change the location of the log file, edit **/opt/microsoft/omi/etc/scxcmprovider.conf** and change the **PATH** field. You do not need to restart the client computer or service for the change to take effect.<br /><br /> You can set the log level to one of three settings.|  

 Both log files support several levels of logging:  

-   **scxcm.log**. To change the log level, edit **/opt/microsoft/configmgr/etc/scxcm.conf** and change each instance of the  **MODULE** tag to the log level you want:  

    -   ERROR: Indicates problems that require attention  

    -   WARNING: Indicates possible problems for client operations  

    -   INFO: More detailed logging that indicates the status of various events on the client  

    -   TRACE: Verbose logging that typically is used to diagnose problems  

-   **scxcmprovider.log**. To change the log level, edit **/opt/microsoft/omi/etc/scxcmprovider.conf** and change each instance of the **MODULE** tag to the log level you want:  

    -   ERROR: Indicates problems that require attention  

    -   WARNING: Indicates possible problems for client operations

    -   INFO: More detailed logging that indicates the status of various events on the client  

Under normal operating conditions, use the ERROR log level. This log level creates the smallest log file. As the log level is increased from ERROR to WARNING, to INFO, and then to TRACE, a larger log file is created as more data is written to the file.  

####  <a name="BKMK_ManageLinuxLogs"></a> Manage log files for the Linux and UNIX client  
The client for Linux and UNIX does not limit the maximum size of the client log files, nor does the client automatically copy the contents of its .log files to another file, such as to a .lo_ file. If you want to control the maximum size of log files, implement a process to manage the log files independent from the Configuration Manager client for Linux and UNIX.  

For example, you can use the standard Linux and UNIX command **logrotate** to manage the size and rotation of the client log files. The Configuration Manager client for Linux and UNIX has an interface that enables **logrotate** to signal the client when the log rotation completes, so the client can resume logging to the log file.  

For information about **logrotate**, see the documentation for the Linux and UNIX distributions that you use.  

###  <a name="BKMK_LogfilesforMac"></a> Client for Mac computers  
The Configuration Manager client for Mac computers records information in the following log files.  

|Log name|Details|  
|--------------|-------------|  
|CCMClient-&lt;*date_time*>.log|Records activities that are related to the Mac client operations, including application management, inventory, and error logging.<br /><br /> This log file is located in the /Library/Application Support/Microsoft/CCM/Logs folder on the Mac computer.|  
|CCMAgent-&lt;*date_time*>.log|Records information that is related to client operations, including user logon and logoff operations, and Mac computer activity.<br /><br /> This log file is in the ~/Library/Logs folder on the Mac computer.|  
|CCMNotifications-&lt;*date_time*>.log|Records activities that are related to Configuration Manager notifications displayed on the Mac computer.<br /><br /> This log file is located in the ~/Library/Logs folder on the Mac computer.|  
|CCMPrefPane-&lt;*date_time*>.log|Records activities related to the Configuration Manager preferences dialog box on the Mac computer, which includes general status and error logging.<br /><br /> This log file is located in the ~/Library/Logs folder on the Mac computer.|  

The log file SMS_DM.log on the site system server also records communication between Mac computers and the management point that is set up for mobile devices and Mac computers.  

##  <a name="BKMK_ServerLogs"></a> Configuration Manager site server log files  
 The following sections list log files that are on the site server or that are related to specific site system roles.  

###  <a name="BKMK_SiteSiteServerLog"></a> Site server and site system server logs  
 The following table lists the log files that are on the Configuration Manager site server and site system servers.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Records enrollment processing activity.|Site server|  
|ADForestDisc.log|Records Active Directory Forest Discovery actions.|Site server|  
|ADService.log|Records account creation and security group details in Active Directory.|Site server|  
|adsgdis.log|Records Active Directory Group Discovery actions.|Site server|  
|adsysdis.log|Records Active Directory System Discovery actions.|Site server|  
|adusrdis.log|Records Active Directory User Discovery actions.|Site server|  
|ccm.log|Records client push installation activities.|Site server|  
|CertMgr.log|Records certificate activities for intrasite communication.|Site system server|  
|chmgr.log|Records activities of the client health manager.|Site server|  
|Cidm.log|Records changes to the client settings by the Client Install Data Manager (CIDM).|Site server|  
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site server|  
|compmon.log|Records the status of component threads monitored for the site server.|Site system server|  
|compsumm.log|Records Component Status Summarizer tasks.|Site server|  
|ComRegSetup.log|Records the initial installation of COM registration results for a site server.|Site system server|  
|dataldr.log|Records information about the processing of MIF files and hardware inventory in the Configuration Manager database.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|despool.log|Records incoming site-to-site communication transfers.|Site server|  
|distmgr.log|Records details about package creation, compression, delta replication, and information updates.|Site server|  
|EPCtrlMgr.log|Records information about the syncing of malware threat information from the Endpoint Protection site system role server with the Configuration Manager database.|Site server|  
|EPMgr.log|Records the status of the Endpoint Protection site system role.|Site system server|  
|EPSetup.log|Provides information about the installation of the Endpoint Protection site system role.|Site system server|  
|EnrollSrv.log|Records activities of the enrollment service process.|Site system server|  
|EnrollWeb.log|Records activities of the enrollment website process.|Site system server|  
|fspmgr.log|Records activities of the fallback status point site system role.|Site system server|  
|hman.log|Records information about site configuration changes, and about the publishing of site information in Active Directory Domain Services.|Site server|  
|Inboxast.log|Records the files that are moved from the management point to the corresponding INBOXES folder on the site server.|Site server|  
|inboxmgr.log|Records file transfer activities between inbox folders.|Site server|  
|inboxmon.log|Records the processing of inbox files and performance counter updates.|Site server|  
|invproc.log|Records the forwarding of MIF files from a secondary site to its parent site.|Site server|  
|migmctrl.log|Records information for Migration actions that involve migration jobs, shared distribution points, and distribution point upgrades.|Top-level site in the Configuration Manager hierarchy, and each child primary site.<br /><br /> In a multi-primary site hierarchy, use the log file that is created at the central administration site.|  
|mpcontrol.log|Records the registration of the management point with Windows Internet Name Service (WINS). Records the availability of the management point every 10 minutes.|Site system server|  
|mpfdm.log|Records the actions of the management point component that moves client files to the corresponding INBOXES folder on the site server.|Site system server|  
|mpMSI.log|Records details about the management point installation.|Site server|  
|MPSetup.log|Records the management point installation wrapper process.|Site server|  
|netdisc.log|Records Network Discovery actions.|Site server|  
|ntsvrdis.log|Records the discovery activity of site system servers.|Site server|  
|Objreplmgr|Records the processing of object change notifications for replication.|Site server|  
|offermgr.log|Records advertisement updates.|Site server|  
|offersum.log|Records the summarization of deployment status messages.|Site server|  
|OfflineServicingMgr.log|Records the activities of applying updates to operating system image files.|Site server|  
|outboxmon.log|Records the processing of outbox files and performance counter updates.|Site server|  
|PerfSetup.log|Records the results of the installation of performance counters.|Site system server|  
|PkgXferMgr.log|Records the actions of the SMS_Executive component that is responsible for sending content from a primary site to a remote distribution point.|Site server|  
|policypv.log|Records updates to the client policies to reflect changes to client settings or deployments.|Primary site server|  
|rcmctrl.log|Records the activities of database replication between sites in the hierarchy.|Site server|  
|replmgr.log|Records the replication of files between the site server components and the Scheduler component.|Site server|  
|ResourceExplorer.log|Records errors, warnings, and information about running Resource Explorer.|Computer that runs the Configuration Manager console|  
|ruleengine.log|Records details about automatic deployment rules for the identification, content download, and software update group and deployment creation.|Site server|  
|schedule.log|Records details about site-to-site job and file replication.|Site server|  
|sender.log|Records the files that transfer by file-based replication between sites.|Site server|  
|sinvproc.log|Records information about the processing of software inventory data to the site database.|Site server|  
|sitecomp.log|Records details about the maintenance of the installed site components on all site system servers in the site.|Site server|  
|sitectrl.log|Records site setting changes made to site control objects in the database.|Site server|  
|sitestat.log|Records the availability and disk space monitoring process of all site systems.|Site server|  
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  
|SMSAWEBSVCSetup.log|Records the installation activities of the Application Catalog web service.|Site system server|  
|smsbkup.log|Records output from the site backup process.|Site server|  
|smsdbmon.log|Records database changes.|Site server|  
|SMSENROLLSRVSetup.log|Records the installation activities of the enrollment web service.|Site system server|  
|SMSENROLLWEBSetup.log|Records the installation activities of the enrollment website.|Site system server|  
|smsexec.log|Records the processing of all site server component threads.|Site server or site system server|  
|SMSFSPSetup.log|Records messages generated by the installation of a fallback status point.|Site system server|  
|SMSPORTALWEBSetup.log|Records the installation activities of the Application Catalog website.|Site system server|  
|SMSProv.log|Records WMI provider access to the site database.|Computer with the SMS Provider|  
|srsrpMSI.log|Records detailed results of the reporting point installation process from the MSI output.|Site system server|  
|srsrpsetup.log|Records results of the reporting point installation process.|Site system server|  
|statesys.log|Records the processing of state system messages.|Site server|  
|statmgr.log|Records the writing of all status messages to the database.|Site server|  
|swmproc.log|Records the processing of metering files and settings.|Site server|  

###  <a name="BKMK_SiteInstallLog"></a> Site server installation log files  
 The following table lists the log files that contain information related to site installation.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Records prerequisite component evaluation and installation activities.|Site server|  
|ConfigMgrSetup.log|Records detailed output from the site server setup.|Site Server|  
|ConfigMgrSetupWizard.log|Records information related to activity in the Setup Wizard.|Site Server|  
|SMS_BOOTSTRAP.log|Records information about the progress of launching the secondary site installation process. Details of the actual setup process are contained in ConfigMgrSetup.log.|Site Server|  
|smstsvc.log|Records information about the installation, use, and removal of a Windows service that is used to test network connectivity and permissions between servers, using the computer account of the server that initiates the connection.|Site server and site system server|  

###  <a name="BKMK_FSPLog"></a> Fallback status point log files  
 The following table lists the log files that contain information related to the fallback status point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Records details about communications to the fallback status point from mobile device legacy clients and client computers.|Site system server|  
|fspMSI.log|Records messages generated by the installation of a fallback status point.|Site system server|  
|fspmgr.log|Records activities of the fallback status point site system role.|Site system server|  

###  <a name="BKMK_MPLog"></a> Management point log files  
 The following table lists the log files that contain information related to the management point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Records client messaging activity on the endpoint.|Site system server|  
|MP_CliReg.log|Records the client registration activity processed by the management point.|Site system server|  
|MP_Ddr.log|Records the conversion of XML.ddr records from clients, and then copies them to the site server.|Site system server|  
|MP_Framework.log|Records the activities of the core management point and client framework components.|Site system server|  
|MP_GetAuth.log|Records client authorization activity.|Site system server|  
|MP_GetPolicy.log|Records policy request activity from client computers.|Site system server|  
|MP_Hinv.log|Records details about the conversion of XML hardware inventory records from clients and the copy of those files to the site server.|Site system server|  
|MP_Location.log|Records location request and reply activity from clients.|Site system server|  
|MP_OOBMgr.log|Records the management point activities related to receiving a OTP from a client.|Site system server|  
|MP_Policy.log|Records policy communication.|Site system server|  
|MP_Relay.log|Records the transfer of files that are collected from the client.|Site system server|  
|MP_Retry.log|Records hardware inventory retry processes.|Site system server|  
|MP_Sinv.log|Records details about the conversion of XML software inventory records from clients and the copy of those files to the site server.|Site system server|  
|MP_SinvCollFile.log|Records details about file collection.|Site system server|  
|MP_Status.log|Records details about the conversion of XML.svf status message files from clients and the copy of those files to the site server.|Site system server|  
|mpcontrol.log|Records the registration of the management point with WINS. Records the availability of the management point every 10 minutes.|Site server|  
|mpfdm.log|Records the actions of the management point component that moves client files to the corresponding INBOXES folder on the site server.|Site system server|  
|mpMSI.log|Records details about the management point installation.|Site server|  
|MPSetup.log|Records the management point installation wrapper process.|Site server|  

###  <a name="BKMK_SUPLog"></a> Software update point log files  
 The following table lists the log files that contain information related to the software update point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Records details about the replication of software updates notification files from a parent site to child sites.|Site server|  
|PatchDownloader.log|Records details about the process of downloading software updates from the update source to the download destination on the site server.|Computer that hosts the Configuration Manager console from which downloads are initiated|  
|ruleengine.log|Records details about automatic deployment rules for the identification, content download, and software update group and deployment creation.|Site server|  
|SUPSetup.log|Records details about the software update point installation. When the software update point installation completes, **Installation was successful** is written to this log file.|Site system server|  
|WCM.log|Records details about the software update point configuration and connections to the WSUS server for subscribed update categories, classifications, and languages.|Site server that connects to the WSUS server|  
|WSUSCtrl.log|Records details about the configuration, database connectivity, and health of the WSUS server for the site.|Site system server|  
|wsyncmgr.log|Records details about the software updates sync process.|Site system server|  
|WUSSyncXML.log|Records details about the Inventory Tool for the Microsoft Updates sync process.|Client computer configured as the sync host for the Inventory Tool for Microsoft Updates|  

##  <a name="BKMK_FunctionLogs"></a> Log files for Configuration Manager functionality  
 The following sections list log files related to Configuration Manager functions.  

###  <a name="BKMK_AppManageLog"></a> Application management  
 The following table lists the log files that contain information related to application management.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Records details about the current and intended state of applications, their applicability, whether requirements were met, deployment types, and dependencies.|Client|  
|AppDiscovery.log|Records details about the discovery or detection of applications on client computers.|Client|  
|AppEnforce.log|Records details about enforcement actions (install and uninstall) taken for applications on the client.|Client|  
|awebsctl.log|Records monitoring activities for the Application Catalog web service point site system role.|Site system server|  
|awebsvcMSI.log|Records detailed installation information for the Application Catalog web service point site system role.|Site system server|  
|Ccmsdkprovider.log|Records the activities of the application management SDK.|Client|  
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site system server|  
|ConfigMgrSoftwareCatalog.log|Records the activity of the Application Catalog, which includes its use of Silverlight.|Client|  
|portlctl.log|Records the monitoring activities for the Application Catalog website point site system role.|Site system server|  
|portlwebMSI.log|Records the MSI installation activity for the Application Catalog website role.|Site system server|  
|PrestageContent.log|Records details about the use of the ExtractContent.exe tool on a remote, prestaged distribution point. This tool extracts content that has been exported to a file.|Site system server|  
|ServicePortalWebService.log|Records the activity of the Application Catalog web service.|Site system server|  
|ServicePortalWebSite.log|Records the activity of the Application Catalog website.|Site system server|  
|SMSdpmon.log|Records details about the distribution point health monitoring scheduled task that is configured on a distribution point.|Site server|  
|SoftwareCatalogUpdateEndpoint.log|Records activities for managing the URL for the Application Catalog shown in Software Center.|Client|  
|SoftwareCenterSystemTasks.log|Records activities related to Software Center prerequisite component validation.|Client|  

 The following table lists the log files that contain information related to deploying packages and programs.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site server|  
|execmgr.log|Records details about packages and task sequences that run.|Client|  

###  <a name="BKMK_AILog"></a> Asset intelligence  
 The following table lists the log files that contain information related to Asset Intelligence.  

|Log Name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Records the activities of Asset Intelligence inventory actions.|Client|  
|aikbmgr.log|Records details about the processing of XML files from the inbox for updating the Asset Intelligence catalog.|Site server|  
|AIUpdateSvc.log|Records the interaction of the Asset Intelligence sync point with System Center Online (SCO), the online web service.|Site system server|  
|AIUSMSI.log|Records details about the installation of the Asset Intelligence sync point site system role.|Site system server|  
|AIUSSetup.log|Records details about the installation of the Asset Intelligence sync point site system role.|Site system server|  
|ManagedProvider.log|Records details about discovering software with an associated software identification tag. Also records activities related to hardware inventory.|Site system server|  
|MVLSImport.log|Records details about the processing of imported licensing files.|Site system server|  

###  <a name="BKMK_BnRLog"></a> Backup and recovery  
 The following table lists log files that contain information related to backup and recovery actions, including site resets, and changes to the SMS Provider.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Records information about setup and recovery tasks when Configuration Manager recovers a site from backup.|Site server|  
|Smsbkup.log|Records details about the site backup activity.|Site server|  
|smssqlbkup.log|Records output from the site database backup process when SQL Server is installed on a server that is not the site server.|Site database server|  
|Smswriter.log|Records information about the state of the Configuration Manager VSS writer that is used by the backup process.|Site server|  

###  <a name="BKMK_CertificateEnrollment"></a> Certificate enrollment  
 The following table lists the Configuration Manager log files that contain information related to certificate enrollment. Certificate enrollment uses the certificate registration point and the Configuration Manager Policy Module on the server that is running the Network Device Enrollment Service.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|Crp.log|Records enrollment activities.|Certificate registration point|  
|Crpctrl.log|Records the operational health of the certificate registration point.|Certificate registration point|  
|Crpsetup.log|Records details about the installation and configuration of the certificate registration point.|Certificate registration point|  
|Crpmsi.log|Records details about the installation and configuration of the certificate registration point.|Certificate registration point|  
|NDESPlugin.log|Records challenge verification and certificate enrollment activities.|Configuration Manager Policy Module and the Network Device Enrollment Service|  

 In addition to the Configuration Manager log files, review the Windows Application logs in Event Viewer on the server running the Network Device Enrollment Service and the server hosting the certificate registration point. For example, look for messages from the **NetworkDeviceEnrollmentService** source. You can also use the following log files:  

-   IIS log files for Network Device Enrollment Service: **&lt;path\>\inetpub\logs\LogFiles\W3SVC1**  

-   IIS log files for the certificate registration point: **&lt;path\>\inetpub\logs\LogFiles\W3SVC1**  

-   Network Device Enrollment Policy log file: **mscep.log**  

    > [!NOTE]  
    >  This file is located in the folder for the Network Device Enrollment Service account profile, for example, in C:\Users\SCEPSvc. For more information about how to enable logging for the Network Device Enrollment Service, see the [Enable Logging](http://go.microsoft.com/fwlink/?LinkId=320576) section in the Network Device Enrollment Service (NDES) in Active Directory Certificate Services (AD CS) article on the TechNet wiki.  

###  <a name="BKMK_BGB"></a> Client notification  
 The following table lists the log files that contain information related to client notification.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Records details about site server activities related to client notification tasks and processing online and task status files.|Site server|  
|BGBServer.log|Records the activities of the notification server, such as client-server communication and pushing tasks to clients. Also records information about the generation of online and task status files to be sent to the site server.|Management point|  
|BgbSetup.log|Records the activities of the notification server installation wrapper process during installation and uninstallation.|Management point|  
|bgbisapiMSI.log|Records details about the notification server installation and uninstallation.|Management point|  
|BgbHttpProxy.log|Records the activities of the notification HTTP proxy as it relays the messages of clients using HTTP to and from the notification server.|Client|  
|CcmNotificationAgent.log|Records the activities of the notification agent, such as client-server communication and information about tasks received and dispatched to other client agents.|Client|  

### Cloud management gateway

The following table lists the log files that contain information related to the cloud management gateway.

||||
|-|-|-|
|Log name|Description|Computer with log file|
|CloudMgr.log|Records details about deploying the cloud management gateway service, ongoing service status, and use data associated with the service.<br>You can configure the logging level be editing the registry **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_CLOUD_SERVICES_MANAGER\Logging level**|The *installdir* folder on the primary site server or CAS.|
|CMGSetup.log or CMG-*RoleInstanceID*-CMGSetup.log<sup>1</sup>|Records details about the 2nd phase of the cloud management gateway deployment (local deployment in Azure)<br>You can configure the logging level using the setting **Trace level** (**Information** (Default), **Verbose**, **Error**) on the **Azure portal\Cloud services configuration** tab.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|
|CMGHttpHandler.log or CMG-*RoleInstanceID*- CMGHttpHandler.log<sup>1</sup>|Records details about the cloud management gateway http handler binding with Internet Information Services in Azure<br>You can configure the logging level using the setting **Trace level** (**Information** (Default), **Verbose**, **Error**) on the **Azure portal\Cloud services configuration** tab.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|
|CMGService.log or CMG-*RoleInstanceID*- CMGService.log<sup>1</sup>|Records details about the cloud management gateway service core component in Azure<br>You can configure the logging level using the setting **Trace level** (**Information** (Default), **Verbose**, **Error**) on the **Azure portal\Cloud services configuration** tab.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|
|SMS_Cloud_ProxyConnector.log|Records details about setting up connections between the cloud management gateway service and the cloud management gateway connection point.|Site system server|

<sup>1</sup> These are local Configuration Manager log files that cloud service manager sync from Azure storage every 5 minutes. The cloud management gateway will push logs to Azure storage every 5 minutes. so the maximum delay will be 10 minutes. Verbose switches will affect both local and remote logs.

- For troubleshooting deployments, use **CloudMgr.log** and **CMGSetup.log**
- For troubleshooting service health, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**.
- For troubleshooting client traffic, use **CMGHttpHandler.log**, **CMGService.log**, and **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a> Compliance settings and company resource access  
 The following table lists the log files that contain information related to compliance settings and company resource access.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Records details about the process of remediation and compliance for compliance settings, software updates, and application management.|Client|  
|CITaskManager.log|Records information about configuration item task scheduling.|Client|  
|DCMAgent.log|Records high-level information about the evaluation, conflict reporting, and remediation of configuration items and applications.|Client|  
|DCMReporting.log|Records information about reporting policy platform results into state messages for configuration items.|Client|  
|DcmWmiProvider.log|Records information about reading configuration item synclets from WMI.|Client|  

###  <a name="BKMK_ConsoleLog"></a> Configuration Manager console  
 The following table lists the log files that contain information related to the Configuration Manager console.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Records the installation of the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|SmsAdminUI.log|Records information about the operation of the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|Smsprov.log|Records activities performed by the SMS Provider. Configuration Manager console activities use the SMS Provider.|Site server or site system server|  

###  <a name="BKMK_ContentLog"></a> Content management  
 The following table lists the log files that contain information related to content management.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Records details for a specific cloud-based distribution point, including information about storage and content access.|Site system server|  
|CloudMgr.log|Records details about content provisioning, collecting storage and bandwidth statistics, and administrator-initiated actions to stop or start the cloud service that runs a cloud-based distribution point.|Site system server|  
|DataTransferService.log|Records all BITS communication for policy or package access. This log also is used for content management by pull-distribution points.|Computer that is configured as a pull-distribution point|  
|PullDP.log|Records details about content that the pull-distribution point transfers from source distribution points.|Computer that is configured as a pull-distribution point|  
|PrestageContent.log|Records the details about the use of the ExtractContent.exe tool on a remote, prestaged distribution point. This tool extracts content that has been exported to a file.|Site system role|  
|SMSdpmon.log|Records details about distribution point health monitoring scheduled tasks that are configured on a distribution point.|Site system role|  
|smsdpprov.log|Records details about the extraction of compressed files received from a primary site. This log is generated by the WMI provider of the remote distribution point.|Distribution point computer that is not colocated with the site server|  


###  <a name="BKMK_DiscoveryLog"></a> Discovery  
The following table lists the log files that contain information related to Discovery.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Records Active Directory Security Group Discovery actions.|Site server|  
|adsysdis.log|Records Active Directory System Discovery actions.|Site server|  
|adusrdis.log|Records Active Directory User Discovery actions.|Site server|  
|ADForestDisc.Log|Records Active Directory Forest Discovery actions.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|InventoryAgent.log|Records activities of hardware inventory, software inventory, and heartbeat discovery actions on the client.|Client|  
|netdisc.log|Records Network Discovery actions.|Site server|  

###  <a name="BKMK_EPLog"></a> Endpoint Protection  
 The following table lists the log files that contain information related to Endpoint Protection.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Records details about the installation of the Endpoint Protection client and the application of antimalware policy to that client.|Client|  
|EPCtrlMgr.log|Records details about the syncing of malware threat information from the Endpoint Protection role server with the Configuration Manager database.|Site system server|  
|EPMgr.log|Monitors the status of the Endpoint Protection site system role.|Site system server|  
|EPSetup.log|Provides information about the installation of the Endpoint Protection site system role.|Site system server|  

###  <a name="BKMK_Extensions"></a> Extensions  
 The following table lists the log files that contain information related to extensions.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Records information about the download of extensions from Microsoft, and the installation and uninstallation of all extensions.|Computer that runs the Configuration Manager console|  
|FeatureExtensionInstaller.log|Records information about the installation and removal of individual extensions when they are enabled or disabled in the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  

###  <a name="BKMK_InventoryLog"></a> Inventory  
 The following table lists the log files that contain information related to processing inventory data.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Records information about the processing of MIF files and hardware inventory in the Configuration Manager database.|Site server|  
|invproc.log|Records the forwarding of MIF files from a secondary site to its parent site.|Secondary site server|  
|sinvproc.log|Records information about the processing of software inventory data to the site database.|Site server|  

###  <a name="BKMK_MeteringLog"></a> Metering  
 The following table lists the log files that contain information related to metering.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitors all software metering processes.|Site server|  

###  <a name="BKMK_MigrationLog"></a> Migration  
 The following table lists the log files that contain information related to migration.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Records information about migration actions that involve migration jobs, shared distribution points, and distribution point upgrades.|Top-level site in the Configuration Manager hierarchy, and each child primary site.<br /><br /> In a multi-primary site hierarchy, use the log file created at the central administration site.|  

###  <a name="BKMK_MDMLog"></a> Mobile devices  
 The following sections list the log files that contain information related to managing mobile devices.  

####  <a name="BKMK_EnrollmentLog"></a> Enrollment  
 The following table lists logs that contain information related to mobile device enrollment.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Records communication between management points that are enabled for mobile devices and the management point endpoints.|Site system server|  
|dmpmsi.log|Records the Windows Installer data for the configuration of a management point that is enabled for mobile devices.|Site system server|  
|DMPSetup.log|Records the configuration of the management point when it is enabled for mobile devices.|Site system server|  
|enrollsrvMSI.log|Records the Windows Installer data for the configuration of an enrollment point.|Site system server|  
|enrollmentweb.log|Records communication between mobile devices and the enrollment proxy point.|Site system server|  
|enrollwebMSI.log|Records the Windows Installer data for the configuration of an enrollment proxy point.|Site system server|  
|enrollmentservice.log|Records communication between an enrollment proxy point and an enrollment point.|Site system server|  
|SMS_DM.log|Records communication between mobile devices, Mac computers, and the management point that is enabled for mobile devices and Mac computers.|Site system server|  

####  <a name="BKMK_ExchSrvLog"></a> Exchange Server Connector  
 The following logs contain information related to the Exchange Server Connector.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Records the activities and the status of the Exchange Server connector.|Site server|  

####  <a name="BKMK_MDLegLog"></a> Mobile device legacy  
 The following table lists logs that contain information related to the mobile device legacy client.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Records details about certificate enrollment data on mobile device legacy clients.|Client|  
|DMCertResp.htm|Records the HTML response from the certificate server when the mobile device legacy client enroller program requests a PKI certificate.|Client|  
|DmClientHealth.log|Records the GUIDs of all mobile device legacy clients that communicate with the management point that is enabled for mobile devices.|Site system server|  
|DmClientRegistration.log|Records registration requests and responses to and from mobile device legacy clients.|Site system server|  
|DmClientSetup.log|Records client setup data for mobile device legacy clients.|Client|  
|DmClientXfer.log|Records client transfer data for mobile device legacy clients and for ActiveSync deployments.|Client|  
|DmCommonInstaller.log|Records client transfer file installation for configuring mobile device legacy client transfer files.|Client|  
|DmInstaller.log|Records whether DMInstaller correctly calls DmClientSetup, and whether DmClientSetup exits with success or failure for mobile device legacy clients.|Client|  
|DmpDatastore.log|Records all the site database connections and queries made by the management point that is enabled for mobile devices.|Site system server|  
|DmpDiscovery.log|Records all the discovery data from the mobile device legacy clients on the management point that is enabled for mobile devices.|Site system server|  
|DmpHardware.log|Records hardware inventory data from mobile device legacy clients on the management point that is enabled for mobile devices.|Site system server|  
|DmpIsapi.log|Records mobile device legacy client communication with a management point that is enabled for mobile devices.|Site system server|  
|dmpmsi.log|Records the Windows Installer data for the configuration of a management point that is enabled for mobile devices.|Site system server|  
|DMPSetup.log|Records the configuration of the management point when it is enabled for mobile devices.|Site system server|  
|DmpSoftware.log|Records software distribution data from mobile device legacy clients on a management point that is enabled for mobile devices.|Site system server|  
|DmpStatus.log|Records status messages data from mobile device clients on a management point that is enabled for mobile devices.|Site system server|  
|DmSvc.log|Records client communication from mobile device legacy clients with a management point that is enabled for mobile devices.|Client|  
|FspIsapi.log|Records details about communications to the fallback status point from mobile device legacy clients and client computers.|Site system server|  

###  <a name="BKMK_OSDLog"></a> Operating system deployment  
 The following table lists the log files that contain information related to operating system deployment.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CAS.log|Records details when distribution points are found for referenced content.|Client|  
|ccmsetup.log|Records ccmsetup tasks for client setup, client upgrade, and client removal. Can be used to troubleshoot client installation problems.|Client|  
|CreateTSMedia.log|Records details for task sequence media creation.|Computer that runs the Configuration Manager console|  
|DeployToVhd.log|Records details about the Virtual Hard Disk (VHD) creation and modification process.|Computer that runs the Configuration Manager console|  
|Dism.log|Records driver installation actions or update application actions for offline servicing.|Site system server|  
|Distmgr.log|Records details about the configuration of enabling a distribution point for Preboot Execution Environment (PXE).|Site system server|  
|DriverCatalog.log|Records details about device drivers that have been imported into the driver catalog.|Site system server|  
|mcsisapi.log|Records information for multicast package transfer and client request responses.|Site system server|  
|mcsexec.log|Records health check, namespace, session creation, and certificate check actions.|Site system server|  
|mcsmgr.log|Records changes to configuration, security mode, and availability.|Site system server|  
|mcsprv.log|Records multicast provider interaction with Windows Deployment Services (WDS).|Site system server|  
|MCSSetup.log|Records details about multicast server role installation.|Site system server|  
|MCSMSI.log|Records details about multicast server role installation.|Site system server|  
|Mcsperf.log|Records details about multicast performance counter updates.|Site system server|  
|MP_ClientIDManager.log|Records management point responses to the client ID requests task sequences initiated from PXE or boot media.|Site system server|  
|MP_DriverManager.log|Records management point responses to Auto Apply Driver task sequence action requests.|Site system server|  
|OfflineServicingMgr.log|Records details of offline servicing schedules and update apply actions on operating system Windows Imaging Format (WIM) files.|Site system server|  
|Setupact.log|Records details about Windows Sysprep and setup logs.|Client|  
|Setupapi.log|Records details about Windows Sysprep and setup logs.|Client|  
|Setuperr.log|Records details about Windows Sysprep and setup logs.|Client|  
|smpisapi.log|Records details about the client state capture and restore actions, and threshold information.|Client|  
|Smpmgr.log|Records details about the results of state migration point health checks and configuration changes.|Site system server|  
|smpmsi.log|Records installation and configuration details about the state migration point.|Site system server|  
|smpperf.log|Records the state migration point performance counter updates.|Site system server|  
|smspxe.log|Records details about the responses to clients that use PXE boot, and details about the expansion of boot images and boot files.|Site system server|  
|smssmpsetup.log|Records installation and configuration details about the state migration point.|Site system server|  
|Smsts.log|Records task sequence activities.|Client|  
|TSAgent.log|Records the outcome of task sequence dependencies before starting a task sequence.|Client|  
|TaskSequenceProvider.log|Records details about task sequences when they are imported, exported, or edited.|Site system server|  
|loadstate.log|Records details about the User State Migration Tool (USMT) and restoring user state data.|Client|  
|scanstate.log|Records details about the User State Migration Tool (USMT) and capturing user state data.|Client|  

###  <a name="BKMK_PowerMgmtLog"></a> Power management  
 The following table lists the log files that contain information related to power management.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Records details about power management activities on the client computer, including monitoring and the enforcement of settings by the Power Management Client Agent.|Client|  

###  <a name="BKMK_RCLog"></a> Remote control  
 The following table lists the log files that contain information related to remote control.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Records details about the activity of the remote control viewer.|In the %temp% folder on the computer that runs the remote control viewer|  

###  <a name="BKMK_ReportLog"></a> Reporting  
 The following table lists the Configuration Manager log files that contain information related to reporting.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Records information about the activity and status of the reporting services point.|Site system server|  
|srsrpMSI.log|Records detailed results of the reporting services point installation process from the MSI output.|Site system server|  
|srsrpsetup.log|Records results of the reporting services point installation process.|Site system server|  

###  <a name="BKMK_RBALog"></a> Role-based administration  
 The following table lists the log files that contain information related to managing role-based administration.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|hman.log|Records information about site configuration changes and the publishing of site information to Active Directory Domain Services.|Site server|  
|SMSProv.log|Records WMI provider access to the site database.|Computer with the SMS Provider|  

###  <a name="BKMK_WITLog"></a> Service connection point  
 The following table lists the log files that contain information related to the service connection point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Records certificate and proxy account information.|Site server|  
|CollEval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Primary site and central administration site|  
|Cloudusersync.log|Records license enablement for users.|Computer with the  service connection point|  
|Dataldr.log|Records information about the processing of MIF files.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|Distmgr.log|Records details about content distribution requests.|Top-level site server|  
|Dmpdownloader.log|Records details about downloads from Microsoft Intune.|Computer with the service connection point|  
|Dmpuploader.log|Records details related to uploading database changes to Microsoft Intune.|Computer with the service connection point|  
|hman.log|Records information about message forwarding.|Site server|  
|objreplmgr.log|Records the processing of policy and assignment.|Primary site server|  
|PolicyPV.log|Records policy generation of all policies.|Site server|  
|outgoingcontentmanager.log|Records content uploaded to Microsoft Intune.|Computer with the  service connection point|  
|Sitecomp.log|Records details of service connection point installation.|Site server|  
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  
|Smsprov.log|Records activities performed by the SMS Provider. Configuration Manager console activities use the SMS Provider.|Computer with the SMS Provider|  
|SrvBoot.log|Records details about the service connection point installer service.|Computer with the service connection point|  
|Statesys.log|Records the processing of mobile device management messages.|Primary site and central administration site|  

###  <a name="BKMK_SU_NAPLog"></a> Software updates  
 The following table lists the log files that contain information related to software updates.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Records activities related to the maintenance and capture of data related to client performance counters.|Client|  
|PatchDownloader.log|Records details about the process of downloading software updates from the update source to the download destination on the site server.|Computer that hosts the Configuration Manager console from which downloads are initiated|  
|PolicyEvaluator.log|Records details about the evaluation of policies on client computers, including policies from software updates.|Client|  
|RebootCoordinator.log|Records details about the coordination of system restarts on client computers after software update installations.|Client|  
|ScanAgent.log|Records details about scan requests for software updates, the WSUS location, and related actions.|Client|  
|SdmAgent.log|Records details about the tracking of remediation and compliance. However, the software updates log file, Updateshandler.log, provides more informative details about installing the software updates that are required for compliance.<br /><br /> This log file is shared with compliance settings.|Client|  
|ServiceWindowManager.log|Records details about the evaluation of maintenance windows.|Client|  
|SmsWusHandler.log|Records details about the scan process for the Inventory Tool for Microsoft Updates.|Client|  
|StateMessage.log|Records details about software update state messages that are created and sent to the management point.|Client|  
|SUPSetup.log|Records details about the software update point installation. When the software update point installation completes, **Installation was successful** is written to this log file.|Site system server|  
|UpdatesDeployment.log|Records details about deployments on the client, including software update activation, evaluation, and enforcement. Verbose logging shows additional information about the interaction with the client user interface.|Client|  
|UpdatesHandler.log|Records details about software update compliance scanning and about the download and installation of software updates on the client.|Client|  
|UpdatesStore.log|Records details about compliance status for the software updates that were assessed during the compliance scan cycle.|Client|  
|WCM.log|Records details about software update point configurations and connections to the WSUS server for subscribed update categories, classifications, and languages.|Site server|  
|WSUSCtrl.log|Records details about the configuration, database connectivity, and health of the WSUS server for the site.|Site system server|  
|wsyncmgr.log|Records details about the software update sync process.|Site server|  
|WUAHandler.log|Records details about the Windows Update Agent on the client when it searches for software updates.|Client|  

###  <a name="BKMK_WOLLog"></a> Wake On LAN  
 The following table lists the log files that contain information related to using Wake On LAN.  

> [!NOTE]  
>  When you supplement Wake On LAN by using wake-up proxy, this activity is logged on the client. For example, see CcmExec.log and SleepAgent_<*domain*\>@SYSTEM_0.log in the [Client operations](#BKMK_ClientOpLogs) section of this topic.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Records details about which clients need to be sent wake-up packets, the number of wake-up packets sent, and the number of wake-up packets retried.|Site server|  
|wolmgr.log|Records details about wake-up procedures, such as when to wake up deployments that are configured for Wake On LAN.|Site server|  

###  <a name="BKMK_WindowsServicingLog"></a>Windows 10 servicing  
 The following table lists the log files that contain information related to Windows 10 servicing.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Records activities related to the maintenance and capture of data related to client performance counters.|Client|  
|CcmRepair.log|Records the repair activities of the client agent.|Client|
|PatchDownloader.log|Records details about the process of downloading software updates from the update source to the download destination on the site server.|Computer that hosts the Configuration Manager console from which downloads are initiated|  
|PolicyEvaluator.log|Records details about the evaluation of policies on client computers, including policies from software updates.|Client|  
|RebootCoordinator.log|Records details about the coordination of system restarts on client computers after software update installations.|Client|  
|ScanAgent.log|Records details about scan requests for software updates, the WSUS location, and related actions.|Client|  
|SdmAgent.log|Records details about the tracking of remediation and compliance. However, the software updates log file, UpdatesHandler.log, provides more informative details about installing the software updates that are required for compliance.<br /><br /> This log file is shared with compliance settings.|Client|  
|ServiceWindowManager.log|Records details about the evaluation of maintenance windows.|Client|  
|setupact.log|Primary log file for most errors that occur during the Windows installation process. The log file is located in the %windir%\$Windows.~BT\sources\panther folder.|Client|
|SmsWusHandler.log|Records details about the scan process for the Inventory Tool for Microsoft Updates.|Client|  
|StateMessage.log|Records details about software updates state messages that are created and sent to the management point.|Client|  
|SUPSetup.log|Records details about the software update point installation. When the software update point installation completes, **Installation was successful** is written to this log file.|Site system server|  
|UpdatesDeployment.log|Records details about deployments on the client, including software update activation, evaluation, and enforcement. Verbose logging shows additional information about the interaction with the client user interface.|Client|  
|Updateshandler.log|Records details about software update compliance scanning and about the download and installation of software updates on the client.|Client|  
|UpdatesStore.log|Records details about compliance status for the software updates that were assessed during the compliance scan cycle.|Client|  
|WCM.log|Records details about software update point configurations and connections to the WSUS server for subscribed update categories, classifications, and languages.|Site server|  
|WSUSCtrl.log|Records details about the configuration, database connectivity, and health of the WSUS server for the site.|Site system server|  
|wsyncmgr.log|Records details about the software update sync process.|Site server|  
|WUAHandler.log|Records details about the Windows Update Agent on the client when it searches for software updates.|Client|  

###  <a name="BKMK_WULog"></a> Windows Update Agent  
 The following table lists the log files that contain information related to the Windows Update Agent.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Records details about when the Windows Update Agent connects to the WSUS server and retrieves the software updates for compliance assessment, and whether there are updates to the agent components.|Client|  

###  <a name="BKMK_WSUSLog"></a> WSUS server  
 The following table lists the log files that contain information related to the WSUS server.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|Change.log|Records details about WSUS server database information that has changed.|WSUS server|  
|SoftwareDistribution.log|Records details about the software updates that are synced from the configured update source to the WSUS server database.|WSUS server|  
