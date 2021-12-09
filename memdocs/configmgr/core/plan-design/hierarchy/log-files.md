---
title: Log file reference
titleSuffix: Configuration Manager
description: A reference of all log files for Configuration Manager client, server, and dependent components.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Log file reference

*Applies to: Configuration Manager (current branch)*

In Configuration Manager, client and site server components record process information in individual log files. You can use the information in these log files to help you troubleshoot issues that might occur. By default, Configuration Manager enables logging for client and server components.

For more general information about log files in Configuration Manager, see [About log files](about-log-files.md). That article includes information on the tools to use, how to configure the logs, and where to find them.

The following sections provide details about the different log files available to you. Monitor Configuration Manager client and server logs for operation details, and view error information to troubleshoot problems.  

- [Client log files](#BKMK_ClientLogs)  

  - [Client operations](#BKMK_ClientOpLogs)  

  - [Client installation](#BKMK_ClientInstallLog)  

  - [Client for Mac computers](#BKMK_LogfilesforMac)  

- [Server log files](#BKMK_ServerLogs)  

  - [Site server and site systems](#BKMK_SiteSiteServerLog)  

  - [Site server installation](#BKMK_SiteInstallLog)

  - [Data warehouse service point](#BKMK_DataWarehouse)

  - [Fallback status point](#BKMK_FSPLog)  

  - [Management point](#BKMK_MPLog)  

  - [Service connection point](#BKMK_WITLog)  

  - [Software update point](#BKMK_SUPLog)  

- [Log files by functionality](#BKMK_FunctionLogs)  

  - [Application management](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Backup and recovery](#BKMK_BnRLog)  

  - [Certificate enrollment](#BKMK_CertificateEnrollment)

  - [Client notification](#BKMK_BGB)

  - [Cloud management gateway](#cloud-management-gateway)

  - [Compliance settings and company resource access](#BKMK_CompSettingsLog)  

  - [Configuration Manager console](#BKMK_ConsoleLog)  

  - [Content management](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Discovery](#BKMK_DiscoveryLog)  

  - [Endpoint analytics](#bkmk_analytics)
  
  - [Endpoint Protection](#BKMK_EPLog)  

  - [Extensions](#BKMK_Extensions)  

  - [Inventory](#BKMK_InventoryLog)  

  - [Migration](#BKMK_MigrationLog)  

  - [Mobile devices](#BKMK_MDMLog)  

  - [OS deployment](#BKMK_OSDLog)  

  - [Power management](#BKMK_PowerMgmtLog)  

  - [Remote control](#BKMK_RCLog)  

  - [Reporting](#BKMK_ReportLog)  

  - [Role-based administration](#BKMK_RBALog)  

  - [Software metering](#BKMK_MeteringLog)  

  - [Software updates](#BKMK_SU_NAPLog)  

  - [Wake On LAN](#BKMK_WOLLog)  

  - [Windows servicing](#BKMK_WindowsServicingLog)

  - [Windows Update Agent](#BKMK_WULog)  

  - [WSUS server](#BKMK_WSUSLog)  

## <a name="BKMK_ClientLogs"></a> Client log files

The following sections list the log files related to client operations and client installation.  

### <a name="BKMK_ClientOpLogs"></a> Client operations

The following table lists the log files located on the Configuration Manager client.  

|Log name|Description|  
|--------------|-----------------|  
|ADALOperationProvider.log|Information about client authentication token requests with Azure Active Directory (Azure AD) Authentication Library (ADAL).|
|BitLockerManagementHandler.log|Records information about BitLocker management policies.|
|CAS.log|The Content Access service. Maintains the local package cache on the client.|  
|Ccm32BitLauncher.log|Records actions for starting applications on the client marked *run as 32 bit*.|  
|CcmEval.log|Records Configuration Manager client status evaluation activities and details for components that are required by the Configuration Manager client.|  
|CcmEvalTask.log|Records the Configuration Manager client status evaluation activities that are initiated by the evaluation scheduled task.|  
|CcmExec.log|Records activities of the client and the SMS Agent Host service. This log file also includes information about enabling and disabling wake-up proxy.|  
|CcmMessaging.log|Records activities related to communication between the client and management points.|  
|CCMNotificationAgent.log|Records activities related to client notification operations.|  
|Ccmperf.log|Records activities related to the maintenance and capture of data related to client performance counters.|  
|CcmRestart.log|Records client service restart activity.|  
|CCMSDKProvider.log|Records activities for the client SDK interfaces.|  
|ccmsqlce.log|Records activities for the SQL Server Compact Edition (CE) that the client uses. This log is typically only used when you enable debug logging, or there's a problem with the component. The client health task (ccmeval) usually self-corrects problems with this component.|
|CcmUsrCse.log|Records details during user sign on for folder redirection policies.|
|CCMVDIProvider.log|Records information for clients in a virtual desktop infrastructure (VDI).|
|CertEnrollAgent.log|Records information for Windows Hello for Business. Specifically communication with the Network Device Enrollment Service (NDES) for certificate requests using the Simple Certificate Enrollment Protocol (SCEP).|
|CertificateMaintenance.log|Maintains certificates for Active Directory Domain Services and management points.|  
|CIAgent.log|Records details about the process of remediation and compliance for compliance settings, software updates, and application management.|
|CIDownloader.log|Records details about configuration item definition downloads.|
|CIStateStore.log|Records changes in state for configuration items, such as compliance settings, software updates, and applications.|
|CIStore.log|Records information about configuration items, such as compliance settings, software updates, and applications.|
|CITaskMgr.log|Records tasks for each application and deployment type, such as content download and install or uninstall actions.|  
|ClientAuth.log|Records signing and authentication activity for the client.|  
|ClientIDManagerStartup.log|Creates and maintains the client GUID and identifies tasks during client registration and assignment.|  
|ClientLocation.log|Records tasks that are related to client site assignment.|
|ClientServicing.log|Records information for client deployment state messages during auto-upgrade and client piloting.|
|CMBITSManager.log|Records information for Background Intelligent Transfer Service (BITS) jobs on the device.|
|CMHttpsReadiness.log|Records the results of running the Configuration Manager HTTPS Readiness Assessment Tool. This tool checks whether computers have a public key infrastructure (PKI) client authentication certificate that can be used with Configuration Manager.|  
|CmRcService.log|Records information for the remote control service.|  
|CoManagementHandler.log|Use to troubleshoot co-management on the client.|
|ComplRelayAgent.log|Records information for the co-management workload for compliance policies.|
|ContentTransferManager.log|Schedules the Background Intelligent Transfer Service (BITS) or Server Message Block (SMB) to download or access packages.|  
|DataTransferService.log|Records all BITS communication for policy or package access.|  
|DCMAgent.log|Records high-level information about the evaluation, conflict reporting, and remediation of configuration items and applications.|
|DCMReporting.log|Records information about reporting policy platform results into state messages for configuration items.|
|DcmWmiProvider.log|Records information about reading configuration item synclets from WMI.|
|DeltaDownload.log|Records information about the download of express updates and updates downloaded using Delivery Optimization.|  
|Diagnostics.log|Records the status of client diagnostic actions.|
|EndpointProtectionAgent|Records information about the installation of the System Center Endpoint Protection client and the application of antimalware policy to that client.|  
|execmgr.log|Records details about packages and task sequences that run on the client.|  
|ExpressionSolver.log|Records details about enhanced detection methods that are used when verbose or debug logging is turned on.|  
|ExternalEventAgent.log|Records the history of Endpoint Protection malware detection and events related to client status.|  
|FileBITS.log|Records all SMB package access tasks.|  
|FileSystemFile.log|Records the activity of the Windows Management Instrumentation (WMI) provider for software inventory and file collection.|  
|FSPStateMessage.log|Records the activity for state messages that are sent to the fallback status point by the client.|  
|InternetProxy.log|Records the network proxy configuration and use activity for the client.|  
|InventoryAgent.log|Records activities of hardware inventory, software inventory, and heartbeat discovery actions on the client.| 
|InventoryProvider.log|More details about hardware inventory, software inventory, and heartbeat discovery actions on the client.|
|LocationCache.log|Records the activity for location cache use and maintenance for the client.|  
|LocationServices.log|Records the client activity for locating management points, software update points, and distribution points.|  
|M365AHandler.log|Information about the Desktop Analytics settings policy|
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
|Scripts.log|Records the activity of when Configuration Manager scripts run on the client.|
|SensorWmiProvider.log|Records the activity of the WMI provider for the endpoint analytics sensor.|
|SensorEndpoint.log|Records the execution of endpoint analytics policy and upload of client data to the site server.|
|SensorManagedProvider.log|Records the gathering and processing of events and information for endpoint analytics.|
|setuppolicyevaluator.log|Records configuration and inventory policy creation in WMI.|  
|SleepAgent_&lt;*domain*\>@SYSTEM_0.log|The main log file for wake-up proxy.|  
|SmsClientMethodProvider.log|Records activity for sending client schedules. For example, with the Send Schedule tool or other programmatic methods.|
|smscliui.log|Records use of the Configuration Manager client in Control Panel.|  
|SrcUpdateMgr.log|Records activity for installed Windows Installer applications that are updated with current distribution point source locations.|  
|StateMessageProvider.log|Records information for the component that sends state messages from the client to the site.|
|StatusAgent.log|Records status messages that are created by the client components.|  
|SWMTRReportGen.log|Generates a use data report that is collected by the metering agent. This data is logged in Mtrmgr.log.|  
|UserAffinity.log|Records details about user device affinity.|
|UserAffinityProvider.log|Technical details from the component that tracks user device affinity.|
|VirtualApp.log|Records information specific to the evaluation of Application Virtualization (App-V) deployment types.|  
|Wedmtrace.log|Records operations related to write filters on Windows Embedded clients.|  
|wakeprxy-install.log|Records installation information when clients receive the client setting option to turn on wake-up proxy.|  
|wakeprxy-uninstall.log|Records information about uninstalling wake-up proxy when clients receive the client setting option to turn off wake-up proxy, if wake-up proxy was previously turned on.|  

### <a name="BKMK_ClientInstallLog"></a> Client installation

The following table lists the log files that contain information related to the installation of the Configuration Manager client.  

|Log name|Description|  
|--------------|-----------------|  
|ccmsetup.log|Records ccmsetup.exe tasks for client setup, client upgrade, and client removal. Can be used to troubleshoot client installation problems.|  
|ccmsetup-ccmeval.log|Records ccmsetup.exe tasks for client status and remediation.|  
|CcmRepair.log|Records the repair activities of the client agent.|  
|client.msi.log|Records setup tasks done by client.msi. Can be used to troubleshoot client installation or removal problems.|  
|ClientServicing.log|Records information for client deployment state messages during auto-upgrade and client piloting.|

### <a name="BKMK_LogfilesforMac"></a> Client for Mac computers

The Configuration Manager client for Mac computers records information in the following log files on the Mac computer:  

|Log name|Details|Location|
|--------------|-------------|-------------|
|CCMClient-&lt;*date_time*>.log|Records activities that are related to the Mac client operations, including application management, inventory, and error logging.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*date_time*>.log|Records information that is related to client operations, including user sign in and sign out operations, and Mac computer activity.| `~/Library/Logs`|  
|CCMNotifications-&lt;*date_time*>.log|Records activities that are related to Configuration Manager notifications displayed on the Mac computer.| `~/Library/Logs`|  
|CCMPrefPane-&lt;*date_time*>.log|Records activities related to the Configuration Manager preferences dialog box on the Mac computer, which includes general status and error logging.| `~/Library/Logs`|  

The log file **SMS_DM.log** on the site system server also records communication between Mac computers and the management point that is set up for mobile devices and Mac computers.  

## <a name="BKMK_ServerLogs"></a> Server log files

The following sections list log files that are on the site server or that are related to specific site system roles.  

### <a name="BKMK_SiteSiteServerLog"></a> Site server and site systems

The following table lists the log files that are on the Configuration Manager site server and site system servers.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Records enrollment processing activity.|Site server|  
|ADForestDisc.log|Records Active Directory Forest Discovery actions.|Site server|  
|adminservice.log|Records actions for the SMS Provider administration service REST API|Computer with the SMS Provider|
|ADService.log|Records account creation and security group details in Active Directory.|Site server|  
|adsgdis.log|Records Active Directory Group Discovery actions.|Site server|  
|adsysdis.log|Records Active Directory System Discovery actions.|Site server|  
|adusrdis.log|Records Active Directory User Discovery actions.|Site server|  
|BusinessAppProcessWorker.log|Records processing for Microsoft Store for Business apps.|Site server|
|ccm.log|Records activities for client push installation.|Site server|  
|CertMgr.log|Records certificate activities for intrasite communication.|Site system server|  
|chmgr.log|Records activities of the client health manager.|Site server|  
|Cidm.log|Records changes to the client settings by the Client Install Data Manager (CIDM).|Site server|  
|CollectionAADGroupSyncWorker.log | Log file for synchronization of collection membership results to Azure Active Directory. | Site server|
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site server|  
|compmon.log|Records the status of component threads monitored for the site server.|Site system server|  
|compsumm.log|Records Component Status Summarizer tasks.|Site server|  
|ComRegSetup.log|Records the initial installation of COM registration results for a site server.|Site system server|  
|dataldr.log|Records information about the processing of MIF files and hardware inventory in the Configuration Manager database.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|despool.log|Records incoming site-to-site communication transfers.|Site server|  
|distmgr.log|Records details about package creation, compression, delta replication, and information updates. It can also include other activities from the distribution manager component. For example, installing a distribution point, connection attempts, and installing components. For more information on other functionality that uses this log, see [Service connection point](#BKMK_WITLog) and [OS deployment](#BKMK_OSDLog).|Site server|  
|EPCtrlMgr.log|Records information about the syncing of malware threat information from the Endpoint Protection site system role server with the Configuration Manager database.|Site server|  
|EPMgr.log|Records the status of the Endpoint Protection site system role.|Site system server|  
|EPSetup.log|Provides information about the installation of the Endpoint Protection site system role.|Site system server|  
|EnrollSrv.log|Records activities of the enrollment service process.|Site system server|  
|EnrollWeb.log|Records activities of the enrollment website process.|Site system server|  
|ExternalNotificationsWorker.log|Records the queue and activities for notifications to external systems like Azure Logic Apps.|Site server|
|fspmgr.log|Records activities of the fallback status point site system role.|Site system server|  
|hman.log|Records information about site configuration changes, and about the publishing of site information in Active Directory Domain Services.|Site server|  
|Inboxast.log|Records the files that are moved from the management point to the corresponding INBOXES folder on the site server.|Site server|  
|inboxmgr.log|Records file transfer activities between inbox folders.|Site server|  
|inboxmon.log|Records the processing of inbox files and performance counter updates.|Site server|  
|invproc.log|Records the forwarding of MIF files from a secondary site to its parent site.|Site server|  
|migmctrl.log|Records information for Migration actions that involve migration jobs, shared distribution points, and distribution point upgrades.|Top-level site in the Configuration Manager hierarchy, and each child primary site. In a multi-primary site hierarchy, use the log file that is created at the central administration site.|  
|mpcontrol.log|Records the registration of the management point. Records the availability of the management point every 10 minutes.|Site system server|  
|mpfdm.log|Records the actions of the management point component that moves client files to the corresponding INBOXES folder on the site server.|Site system server|  
|mpMSI.log|Records details about the management point installation.|Site server|  
|MPSetup.log|Records the management point installation wrapper process.|Site server|  
|netdisc.log|Records Network Discovery actions.|Site server|  
|NotiCtrl.log|Application request notifications.|Site server|  
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
|RESTPROVIDERSetup.log|Installation of the SMS Provider administration service REST API|Computer with the SMS Provider|
|ruleengine.log|Records details about automatic deployment rules for the identification, content download, and software update group and deployment creation.|Site server|  
|schedule.log|Records details about site-to-site job and file replication.|Site server|  
|sender.log|Records the files that transfer by file-based replication between sites.|Site server|  
|sinvproc.log|Records information about the processing of software inventory data to the site database.|Site server|  
|sitecomp.log|Records details about the maintenance of the installed site components on all site system servers in the site.|Site server|  
|sitectrl.log|Records site setting changes made to site control objects in the database.|Site server|  
|sitestat.log|Records the availability and disk space monitoring process of all site systems.|Site server|
|SMS_AZUREAD_DISCOVERY_AGENT.log| Log file for Azure Active Directory (Azure AD) user and user group discovery. | Site server|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Log file for component that synchronizes apps from the Microsoft Store for Business.|Site server|
|SMS_DataEngine.log|Log file for management insights.|Site server|
|SMS_ISVUPDATES_SYNCAGENT.log| Log file for synchronization of third-party software updates.| Top-level software update point in the Configuration Manager hierarchy.|
|SMS_MESSAGE_PROCESSING_ENGINE.log| Log file for the message processing engine, which the site uses to process results for client actions. For example, run scripts and CMPivot.| Site server|
|SMS_OrchestrationGroup.log| Log file for orchestration groups|Site server|
|SMS_PhasedDeployment.log| Log file for phased deployments|Top-level site in the Configuration Manager hierarchy|
|SMS_REST_PROVIDER.log|Service health state for the SMS Provider administration service REST API, including certificate information|Computer with the SMS Provider|
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  
|smsbkup.log|Records output from the site backup process.|Site server|  
|smsdbmon.log|Records database changes.|Site server|  
|SMSENROLLSRVSetup.log|Records the installation activities of the enrollment web service.|Site system server|  
|SMSENROLLWEBSetup.log|Records the installation activities of the enrollment website.|Site system server|  
|smsexec.log|Records the processing of all site server component threads.|Site server or site system server|  
|SMSFSPSetup.log|Records messages generated by the installation of a fallback status point.|Site system server|  
|SMSProv.log|Records WMI provider access to the site database.|Computer with the SMS Provider|  
|srsrpMSI.log|Records detailed results of the reporting point installation process from the MSI output.|Site system server|  
|srsrpsetup.log|Records results of the reporting point installation process.|Site system server|  
|statesys.log|Records the processing of state system messages.|Site server|  
|statmgr.log|Records the writing of all status messages to the database.|Site server|  
|swmproc.log|Records the processing of metering files and settings.|Site server|
|UXAnalyticsUploadWorker.log|Records data upload to the service for endpoint analytics.|Site server|

### <a name="BKMK_SiteInstallLog"></a> Site server installation

The following table lists the log files that contain information related to site installation.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Records prerequisite component evaluation and installation activities.|Site server|  
|ConfigMgrSetup.log|Records detailed output from the site server setup.|Site Server|  
|ConfigMgrSetupWizard.log|Records information related to activity in the Setup Wizard.|Site Server|  
|SMS_BOOTSTRAP.log|Records information about the progress of launching the secondary site installation process. Details of the actual setup process are contained in ConfigMgrSetup.log.|Site Server|  
|smstsvc.log|Records information about the installation, use, and removal of a Windows service. Windows uses this service to test network connectivity and permissions between servers. It uses the computer account of the server that creates the connection.|Site server and site system server|  

### <a name="BKMK_DataWarehouse"></a> Data warehouse service point

The following table lists the log files that contain information related to the data warehouse service point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Records messages generated by the installation of a data warehouse service point.|Site system server|  
|DWSSSetup.log|Records messages generated by the installation of a data warehouse service point.|Site system server|  
|Microsoft.ConfigMgrDataWarehouse.log|Records information about data synchronization between the site database and the data warehouse database.|Site system server|  

### <a name="BKMK_FSPLog"></a> Fallback status point

The following table lists the log files that contain information related to the fallback status point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Records details about communications to the fallback status point from mobile device legacy clients and client computers.|Site system server|  
|fspMSI.log|Records messages generated by the installation of a fallback status point.|Site system server|  
|fspmgr.log|Records activities of the fallback status point site system role.|Site system server|  

### <a name="BKMK_MPLog"></a> Management point

The following table lists the log files that contain information related to the management point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Records client messaging activity on the endpoint.|Site system server|
|CCM_STS.log|Records activities for authentication tokens, either from Azure Active Directory or site-issued client tokens.|Site system server|
|ClientAuth.log|Records signing and authentication activity.|Site system server|
|MP_CliReg.log|Records the client registration activity processed by the management point.|Site system server|  
|MP_Ddr.log|Records the conversion of XML.ddr records from clients, and then copies them to the site server.|Site system server|  
|MP_Framework.log|Records the activities of the core management point and client framework components.|Site system server|  
|MP_GetAuth.log|Records client authorization activity.|Site system server|  
|MP_GetPolicy.log|Records policy request activity from client computers.|Site system server|  
|MP_Hinv.log|Records details about the conversion of XML hardware inventory records from clients and the copy of those files to the site server.|Site system server|  
|MP_Location.log|Records location request and reply activity from clients.|Site system server|  
|MP_OOBMgr.log|Records the management point activities related to receiving an OTP from a client.|Site system server|  
|MP_Policy.log|Records policy communication.|Site system server|  
|MP_RegistrationManager.log|Records activities related to client registration, such as validating certificates, CRL, and tokens.|Site system server|
|MP_Relay.log|Records the transfer of files that are collected from the client.|Site system server|  
|MP_RelayMsgMgr.log|Records how the management point handles incoming client messages, such as for scripts or CMPivot.|Site system server|
|MP_Retry.log|Records hardware inventory retry processes.|Site system server|  
|MP_Sinv.log|Records details about the conversion of XML software inventory records from clients and the copy of those files to the site server.|Site system server|  
|MP_SinvCollFile.log|Records details about file collection.|Site system server|  
|MP_Status.log|Records details about the conversion of XML.svf status message files from clients and the copy of those files to the site server.|Site system server|
|mpcontrol.log|Records the registration of the management point. Records the availability of the management point every 10 minutes.|Site server|  
|mpfdm.log|Records the actions of the management point component that moves client files to the corresponding INBOXES folder on the site server.|Site system server|  
|mpMSI.log|Records details about the management point installation.|Site server|  
|MPSetup.log|Records the management point installation wrapper process.|Site server|  
|UserService.log|Records user requests from Software Center, retrieving/installing user-available applications from the server.|Site system server|

### <a name="BKMK_WITLog"></a> Service connection point

The following table lists the log files that contain information related to the service connection point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Records certificate and proxy account information.|Site server|  
|CollEval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Primary site and central administration site|  
|Cloudusersync.log|Records license enablement for users.|Computer with the  service connection point|  
|Dataldr.log|Records information about the processing of MIF files.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|Distmgr.log|Records details about content distribution requests.|Top-level site server|  
|Dmpdownloader.log|Records details about downloads from Microsoft, such as site updates.|Computer with the service connection point|  
|Dmpuploader.log|Records detail related to uploading database changes to Microsoft.|Computer with the service connection point|  
|EndpointConnectivityCheckWorker.log|Starting in version 2010, records detail related to checks for important internet endpoints.|Computer with the service connection point|
|hman.log|Records information about message forwarding.|Site server|  
|WsfbSyncWorker.log|Records information about the communication with the Microsoft Store for Business.|Computer with the service connection point|
|objreplmgr.log|Records the processing of policy and assignment.|Primary site server|  
|PolicyPV.log|Records policy generation of all policies.|Site server|  
|outgoingcontentmanager.log|Records content uploaded to Microsoft.|Computer with the service connection point|  
|ServiceConnectionTool.log|Records details about use of the [service connection tool](../../servers/manage/use-the-service-connection-tool.md) based on the parameter you use. Each time you run the tool, it replaces any existing log file.|Same location as the tool|
|Sitecomp.log|Records details of service connection point installation.|Site server|  
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  
|SMS_CLOUDCONNECTION.log|Records information about cloud services.|Computer with the service connection point|
|Smsprov.log|Records activities of the SMS Provider. Configuration Manager console activities use the SMS Provider.|Computer with the SMS Provider|  
|SrvBoot.log|Records details about the service connection point installer service.|Computer with the service connection point|  
|Statesys.log|Records the processing of mobile device management messages.|Primary site and central administration site|  

### <a name="BKMK_SUPLog"></a> Software update point

The following table lists the log files that contain information related to the software update point.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Records details about the replication of software updates notification files from a parent site to child sites.|Site server|  
|PatchDownloader.log|Records details about the process of downloading software updates from the update source to the download destination on the site server.|When you manually download updates, this file is in your `%temp%` directory on the computer where you use the console. For automatic deployment rules, if the Configuration Manager client is installed on the site server, this file is on the site server in `%windir%\CCM\Logs`.|  
|ruleengine.log|Records details about automatic deployment rules for the identification, content download, and software update group and deployment creation.|Site server|
|SMS_ISVUPDATES_SYNCAGENT.log| Log file for synchronization of third-party software updates.| Top-level software update point in the Configuration Manager hierarchy.|
|SUPSetup.log|Records details about the software update point installation. When the software update point installation completes, **Installation was successful** is written to this log file.|Site system server|  
|WCM.log|Records details about the software update point configuration and connections to the WSUS server for subscribed update categories, classifications, and languages.|Site server that connects to the WSUS server|  
|WSUSCtrl.log|Records details about the configuration, database connectivity, and health of the WSUS server for the site.|Site system server|  
|wsyncmgr.log|Records details about the software updates sync process.|Site system server|  
|WUSSyncXML.log|Records details about the Inventory Tool for the Microsoft Updates sync process.|Client computer configured as the sync host for the Inventory Tool for Microsoft Updates|  


## <a name="BKMK_FunctionLogs"></a> Log files by functionality

The following sections list log files related to Configuration Manager functions.  

### <a name="BKMK_AppManageLog"></a> Application management

The following table lists the log files that contain information related to application management.  

| Log name | Description | Computer with log file |
|----------|-------------|------------------------|
|AppIntentEval.log|Records details about the current and intended state of applications, their applicability, whether requirements were met, deployment types, and dependencies.|Client|
|AppDiscovery.log|Records details about the discovery or detection of applications on client computers.|Client|
|AppEnforce.log|Records details about enforcement actions (install and uninstall) taken for applications on the client.|Client|
|AppGroupHandler.log|Records detection and enforcement information for application groups|Client|
|BusinessAppProcessWorker.log|Records processing for Microsoft Store for Business apps.|Site server|
|Ccmsdkprovider.log|Records the activities of the application management SDK.|Client|
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site system server|
|WsfbSyncWorker.log|Records information about the communication with the Microsoft Store for Business.|Computer with the service connection point|
|NotiCtrl.log|Application request notifications.|Site server|
|PrestageContent.log|Records details about the use of the ExtractContent.exe tool on a remote, prestaged distribution point. This tool extracts content that has been exported to a file.|Site system server|
|SettingsAgent.log|Enforcement of specific applications, records orchestration of application group evaluation, and details of co-management policies.|Client|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Log file for component that synchronizes apps from the Microsoft Store for Business.|Site server|
|SMS_CLOUDCONNECTION.log|Records information about cloud services.|Computer with the service connection point|
|SMS_ImplicitUninstall.log|Records events from the implicit uninstall background worker process.<!--3607457-->|Site server|
|SMSdpmon.log|Records details about the distribution point health monitoring scheduled task that is configured on a distribution point.|Site server|
|SoftwareCenterSystemTasks.log|Records activities related to Software Center prerequisite component validation.|Client|
|TSDTHandler.log|For the task sequence deployment type. It logs the process from app enforcement (install or uninstall) to the launch of the task sequence. Use it with AppEnforce.log and smsts.log.<!-- MEMDocs#336 -->|Client|

#### Packages and programs

The following table lists the log files that contain information related to deploying packages and programs.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|colleval.log|Records details about when collections are created, changed, and deleted by the Collection Evaluator.|Site server|  
|execmgr.log|Records details about packages and task sequences that run.|Client|  

### <a name="BKMK_AILog"></a> Asset Intelligence

The following table lists the log files that contain information related to Asset Intelligence.  

|Log Name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Records the activities of Asset Intelligence inventory actions.|Client|  
|aikbmgr.log|Records details about the processing of XML files from the inbox for updating the Asset Intelligence catalog.|Site server|  
|AIUpdateSvc.log|Records the interaction of the Asset Intelligence sync point with the cloud service.|Site system server|  
|AIUSMSI.log|Records details about the installation of the Asset Intelligence sync point site system role.|Site system server|  
|AIUSSetup.log|Records details about the installation of the Asset Intelligence sync point site system role.|Site system server|  
|ManagedProvider.log|Records details about discovering software with an associated software identification tag. Also records activities related to hardware inventory.|Site system server|  
|MVLSImport.log|Records details about the processing of imported licensing files.|Site system server|  

### <a name="BKMK_BnRLog"></a> Backup and recovery

The following table lists log files that contain information related to backup and recovery actions, including site resets, and changes to the SMS Provider.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Records information about setup and recovery tasks when Configuration Manager recovers a site from backup.|Site server|  
|Smsbkup.log|Records details about the site backup activity.|Site server|  
|smssqlbkup.log|Records output from the site database backup process when SQL Server is installed on a server that isn't the site server.|Site database server|  
|Smswriter.log|Records information about the state of the Configuration Manager VSS writer that is used by the backup process.|Site server|  

### <a name="BKMK_CertificateEnrollment"></a> Certificate enrollment

The following table lists the Configuration Manager log files that contain information related to certificate enrollment. Certificate enrollment uses the certificate registration point and the Configuration Manager Policy Module on the server that's running the Network Device Enrollment Service (NDES).  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CertEnrollAgent.log|Records client communication with NDES for certificate requests using the Simple Certificate Enrollment Protocol (SCEP).|Windows Hello for Business client|
|Crp.log|Records enrollment activities.|Certificate registration point|  
|Crpctrl.log|Records the operational health of the certificate registration point.|Certificate registration point|  
|Crpsetup.log|Records details about the installation and configuration of the certificate registration point.|Certificate registration point|  
|Crpmsi.log|Records details about the installation and configuration of the certificate registration point.|Certificate registration point|  
|NDESPlugin.log|Records challenge verification and certificate enrollment activities.|Configuration Manager Policy Module and the Network Device Enrollment Service|  

Along with the Configuration Manager log files, review the Windows Application logs in Event Viewer on the server running the Network Device Enrollment Service and the server hosting the certificate registration point. For example, look for messages from the **NetworkDeviceEnrollmentService** source.

You can also use the following log files:  

- IIS log files for Network Device Enrollment Service: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- IIS log files for the certificate registration point: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- Network Device Enrollment Policy log file: **mscep.log**  

    > [!NOTE]  
    > This file is located in the folder for the NDES account profile, for example, in C:\Users\SCEPSvc. For more information about how to enable NDES logging, see the [Enable Logging](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) section of the NDES wiki.  

### <a name="BKMK_BGB"></a> Client notification

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

[!INCLUDE [Logs for cloud management gateway](includes/logs-cmg.md)]

### <a name="BKMK_CompSettingsLog"></a> Compliance settings and company resource access

The following table lists the log files that contain information related to compliance settings and company resource access.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Records details about the process of remediation and compliance for compliance settings, software updates, and application management.|Client|  
|CITaskManager.log|Records information about configuration item task scheduling.|Client|  
|DCMAgent.log|Records high-level information about the evaluation, conflict reporting, and remediation of configuration items and applications.|Client|  
|DCMReporting.log|Records information about reporting policy platform results into state messages for configuration items.|Client|  
|DcmWmiProvider.log|Records information about reading configuration item synclets from WMI.|Client|  

### <a name="BKMK_ConsoleLog"></a> Configuration Manager console

The following table lists the log files that contain information related to the Configuration Manager console.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Records the installation of the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|SmsAdminUI.log|Records information about the operation of the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|Smsprov.log|Records activities of the SMS Provider. Configuration Manager console activities use the SMS Provider.|Site server or site system server|  

### <a name="BKMK_ContentLog"></a> Content management

The following table lists the log files that contain information related to content management.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Records details for a specific cloud-based content source, including information about storage and content access.|Site system server|  
|CloudMgr.log|Records details about content provisioning, collecting storage and bandwidth statistics, and administrator-initiated actions to stop or start the cloud service that runs a content-enabled cloud management gateway (CMG).|Site system server|  
|DataTransferService.log|Records all BITS communication for policy or package access. This log also is used for content management by pull-distribution points.|Computer that is configured as a pull-distribution point|  
|PullDP.log|Records details about content that the pull-distribution point transfers from source distribution points.|Computer that is configured as a pull-distribution point|  
|PrestageContent.log|Records the details about the use of the ExtractContent.exe tool on a remote, prestaged distribution point. This tool extracts content that has been exported to a file.|Site system role|  
|PkgXferMgr.log|Records the actions of the SMS_Executive component that is responsible for sending content from a primary site to a remote distribution point.|Site server|
|SMSdpmon.log|Records details about distribution point health monitoring scheduled tasks that are configured on a distribution point.|Site system role|  
|smsdpprov.log|Records details about the extraction of compressed files received from a primary site. This log is generated by the WMI provider of the remote distribution point.|Distribution point computer that isn't colocated with the site server|  
|smsdpusage.log|Records details about the smsdpusage.exe that runs and gathers data for the distribution point usage summary report.|Site system role|  

### Desktop Analytics

Use the following log files to help troubleshoot issues with Desktop Analytics integrated with Configuration Manager.

The log files on the service connection point are in the following directory: `%ProgramFiles%\Configuration Manager\Logs\M365A`.
The log files on the Configuration Manager client are in the following directory: `%WinDir%\CCM\logs`.

| Log | Description |Computer with log file|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Information about deployment plan sync from Desktop Analytics cloud service to on-premises Configuration Manager |Service connection point|
| M365ADeviceHealthWorker.log | Information about device health upload from Configuration Manager to Microsoft cloud |Service connection point|
| M365AHandler.log | Information about the Desktop Analytics settings policy |Client|
| M365AUploadWorker.log | Information about collection and device upload from Configuration Manager to Microsoft cloud |Service connection point|
| SmsAdminUI.log | Information about Configuration Manager console activity, like configuring the Azure cloud services  |Service connection point|

### <a name="BKMK_DiscoveryLog"></a> Discovery

The following table lists the log files that contain information related to discovery.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Records Active Directory Security Group Discovery actions.|Site server|  
|adsysdis.log|Records Active Directory System Discovery actions.|Site server|  
|adusrdis.log|Records Active Directory User Discovery actions.|Site server|  
|ADForestDisc.Log|Records Active Directory Forest Discovery actions.|Site server|  
|ddm.log|Records activities of the discovery data manager.|Site server|  
|InventoryAgent.log|Records activities of hardware inventory, software inventory, and heartbeat discovery actions on the client.|Client|  
|netdisc.log|Records Network Discovery actions.|Site server|  

### <a name="bkmk_analytics"></a> Endpoint analytics

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|UXAnalyticsUploadWorker.log|Records data upload to the service for endpoint analytics.|Site server|  
|SensorWmiProvider.log|Records the activity of the WMI provider for the endpoint analytics sensor.|Client|  
|SensorEndpoint.log|Records the execution of endpoint analytics policy and upload of client data to the site server.|Client|
|SensorManagedProvider.log|Records the gathering and processing of events and information for endpoint analytics.|Client|

### <a name="BKMK_EPLog"></a> Endpoint Protection

The following table lists the log files that contain information related to Endpoint Protection.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Records details about the installation of the Endpoint Protection client and the application of antimalware policy to that client.|Client|  
|EPCtrlMgr.log|Records details about the syncing of malware threat information from the Endpoint Protection role server with the Configuration Manager database.|Site system server|  
|EPMgr.log|Monitors the status of the Endpoint Protection site system role.|Site system server|  
|EPSetup.log|Provides information about the installation of the Endpoint Protection site system role.|Site system server|  

### <a name="BKMK_Extensions"></a> Extensions

The following table lists the log files that contain information related to extensions.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Records information about the download of extensions from Microsoft, and the installation and uninstallation of all extensions.|Computer that runs the Configuration Manager console|  
|FeatureExtensionInstaller.log|Records information about the installation and removal of individual extensions when they're enabled or disabled in the Configuration Manager console.|Computer that runs the Configuration Manager console|  
|SmsAdminUI.log|Records Configuration Manager console activity.|Computer that runs the Configuration Manager console|  

### <a name="BKMK_InventoryLog"></a> Inventory

The following table lists the log files that contain information related to processing inventory data.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Records information about the processing of MIF files and hardware inventory in the Configuration Manager database.|Site server|  
|invproc.log|Records the forwarding of MIF files from a secondary site to its parent site.|Secondary site server|  
|sinvproc.log|Records information about the processing of software inventory data to the site database.|Site server|  

### <a name="BKMK_MeteringLog"></a> Metering

The following table lists the log files that contain information related to metering.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitors all software metering processes.|Client|  
|SWMTRReportGen.log|Generates a use data report that is collected by the metering agent. This data is logged in Mtrmgr.log.|Client|
|swmproc.log|Records the processing of metering files and settings.|Site server|

### <a name="BKMK_MigrationLog"></a> Migration

The following table lists the log files that contain information related to migration.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Records information about migration actions that involve migration jobs, shared distribution points, and distribution point upgrades.|Top-level site in the Configuration Manager hierarchy, and each child primary site. In a multi-primary site hierarchy, use the log file created at the central administration site.|  

### <a name="BKMK_MDMLog"></a> Mobile devices

The following sections list the log files that contain information related to managing mobile devices.  

#### <a name="BKMK_EnrollmentLog"></a> Enrollment

The following table lists logs that contain information related to mobile device enrollment.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Records communication between management points that are enabled for mobile devices and the management point endpoints.|Site system server|  
|dmpmsi.log|Records the Windows Installer data for the configuration of a management point that is enabled for mobile devices.|Site system server|  
|DMPSetup.log|Records the configuration of the management point when it's enabled for mobile devices.|Site system server|  
|enrollsrvMSI.log|Records the Windows Installer data for the configuration of an enrollment point.|Site system server|  
|enrollmentweb.log|Records communication between mobile devices and the enrollment proxy point.|Site system server|  
|enrollwebMSI.log|Records the Windows Installer data for the configuration of an enrollment proxy point.|Site system server|  
|enrollmentservice.log|Records communication between an enrollment proxy point and an enrollment point.|Site system server|  
|SMS_DM.log|Records communication between mobile devices, Mac computers, and the management point that is enabled for mobile devices and Mac computers.|Site system server|  

#### <a name="BKMK_ExchSrvLog"></a> Exchange Server connector

The following logs contain information related to the Exchange Server connector.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Records the activities and the status of the Exchange Server connector.|Site server|  

#### <a name="BKMK_MDLegLog"></a> Mobile device legacy

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
|DMPSetup.log|Records the configuration of the management point when it's enabled for mobile devices.|Site system server|  
|DmpSoftware.log|Records software distribution data from mobile device legacy clients on a management point that is enabled for mobile devices.|Site system server|  
|DmpStatus.log|Records status messages data from mobile device clients on a management point that is enabled for mobile devices.|Site system server|  
|DmSvc.log|Records client communication from mobile device legacy clients with a management point that is enabled for mobile devices.|Client|  
|FspIsapi.log|Records details about communications to the fallback status point from mobile device legacy clients and client computers.|Site system server|  

### <a name="BKMK_OSDLog"></a> OS deployment

The following table lists the log files that contain information related to OS deployment.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CAS.log|Records details when distribution points are found for referenced content.|Client|  
|ccmsetup.log|Records ccmsetup tasks for client setup, client upgrade, and client removal. Can be used to troubleshoot client installation problems.|Client|  
|CreateTSMedia.log|Records details for task sequence media creation.|Computer that runs the Configuration Manager console|  
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
|MP_ClientIDManager.log|Records management point responses to client ID requests that task sequences start from PXE or boot media.|Site system server|  
|MP_DriverManager.log|Records management point responses to Auto Apply Driver task sequence action requests.|Site system server|  
|OfflineServicingMgr.log|Records details of offline servicing schedules and update apply actions on operating system Windows Imaging Format (WIM) files.|Site system server|  
|Setupact.log|Records details about Windows Sysprep and setup logs. For more information, see [Log Files](/windows/deployment/upgrade/log-files).|Client|  
|Setupapi.log|Records details about Windows Sysprep and setup logs.|Client|  
|Setuperr.log|Records details about Windows Sysprep and setup logs.|Client|  
|smpisapi.log|Records details about the client state capture and restore actions, and threshold information.|Client|  
|Smpmgr.log|Records details about the results of state migration point health checks and configuration changes.|Site system server|  
|smpmsi.log|Records installation and configuration details about the state migration point.|Site system server|  
|smpperf.log|Records the state migration point performance counter updates.|Site system server|  
|smspxe.log|Records details about the responses to clients that use PXE boot, and details about the expansion of boot images and boot files.|Site system server|  
|smssmpsetup.log|Records installation and configuration details about the state migration point.|Site system server|
| SMS_PhasedDeployment.log| Log file for phased deployments|Top-level site in the Configuration Manager hierarchy|
|Smsts.log|Records task sequence activities.|Client|  
|TSAgent.log|Records the outcome of task sequence dependencies before starting a task sequence.|Client|  
|TaskSequenceProvider.log|Records details about task sequences when they're imported, exported, or edited.|Site system server|  
|loadstate.log|Records details about the User State Migration Tool (USMT) and restoring user state data.|Client|  
|scanstate.log|Records details about the User State Migration Tool (USMT) and capturing user state data.|Client|  

### <a name="BKMK_PowerMgmtLog"></a> Power management

The following table lists the log files that contain information related to power management.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Records details about power management activities on the client computer, including monitoring and the enforcement of settings by the Power Management Client Agent.|Client|  

### <a name="BKMK_RCLog"></a> Remote control

The following table lists the log files that contain information related to remote control.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Records details about the activity of the remote control viewer.|On the computer that runs the remote control viewer, in the %temp% folder.|  

### <a name="BKMK_ReportLog"></a> Reporting

The following table lists the Configuration Manager log files that contain information related to reporting.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Records information about the activity and status of the reporting services point.|Site system server|  
|srsrpMSI.log|Records detailed results of the reporting services point installation process from the MSI output.|Site system server|  
|srsrpsetup.log|Records results of the reporting services point installation process.|Site system server|  

### <a name="BKMK_RBALog"></a> Role-based administration

The following table lists the log files that contain information related to managing role-based administration.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|hman.log|Records information about site configuration changes and the publishing of site information to Active Directory Domain Services.|Site server|  
|SMSProv.log|Records WMI provider access to the site database.|Computer with the SMS Provider|  

### <a name="BKMK_MeteringLog"></a> Software metering

The following table lists the log files that contain information related to software metering.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitors all software metering processes.|Site server|  

### <a name="BKMK_SU_NAPLog"></a> Software updates

The following table lists the log files that contain information related to software updates.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Records details when the client calls the Office click-to-run COM interface to download and install Microsoft 365 Apps for enterprise client updates. It's similar to use of WuaHandler when it calls the Windows Update Agent API to download and install Windows updates.<!-- SCCMDocs#888 -->|Client|
|ccmperf.log|Records activities related to the maintenance and capture of data related to client performance counters.|Client|
|DeltaDownload.log|Records information about the download of express updates and updates downloaded using Delivery Optimization.|Client|  
|PatchDownloader.log|Records details about the process of downloading software updates from the update source to the download destination on the site server.|When downloading updates manually, this log file is located in the %temp% directory of the user running the console on the machine you're running the console. For Automatic Deployment Rules, this log file is located on the site server in %windir%\CCM\Logs, if the ConfigMgr client is installed on the site server.|  
|PolicyEvaluator.log|Records details about the evaluation of policies on client computers, including policies from software updates.|Client|  
|RebootCoordinator.log|Records details about the coordination of system restarts on client computers after software update installations.|Client|  
|ScanAgent.log|Records details about scan requests for software updates, the WSUS location, and related actions.|Client|  
|SdmAgent.log|Records details about the tracking of remediation and compliance. However, the software updates log file, Updateshandler.log, provides more informative details about installing the software updates that are required for compliance. This log file is shared with compliance settings.|Client|  
|ServiceWindowManager.log|Records details about the evaluation of maintenance windows.|Client|
|SMS_ISVUPDATES_SYNCAGENT.log| Log file for synchronization of third-party software updates.| Top-level software update point in the Configuration Manager hierarchy.|
|SMS_OrchestrationGroup.log| Log file for orchestration groups|Site server|
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

### <a name="BKMK_WOLLog"></a> Wake On LAN

The following table lists the log files that contain information related to using Wake On LAN.  

> [!NOTE]  
> When you supplement Wake On LAN by using wake-up proxy, this activity is logged on the client. For example, see CcmExec.log and SleepAgent_<*domain*\>@SYSTEM_0.log in the [Client operations](#BKMK_ClientOpLogs) section of this article.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Records details about which clients need to be sent wake-up packets, the number of wake-up packets sent, and the number of wake-up packets retried.|Site server|  
|wolmgr.log|Records details about wake-up procedures, such as when to wake up deployments that are configured for Wake On LAN.|Site server|  

### <a name="BKMK_WindowsServicingLog"></a> Windows servicing

The following table lists the log files that contain information related to Windows servicing.  
Servicing uses the same infrastructure and process as software updates. For other logs applicable to the servicing scenario, see [Software updates](#BKMK_SU_NAPLog).

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|CBS.log|Records servicing failures related to changes for Windows Updates or roles and features.|Client|
|DISM.log|Records all actions using DISM. If necessary, DISM.log will point to CBS.log for more details.|Client|
|setupact.log|Primary log file for most errors that occur during the Windows installation process. The log file is located in the %windir%\$Windows.~BT\sources\panther folder.|Client|

For more information, see [Online Servicing-Related Log Files](/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="BKMK_WULog"></a> Windows Update Agent

The following table lists the log files that contain information related to the Windows Update Agent.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Records details about when the Windows Update Agent connects to the WSUS server and retrieves the software updates for compliance assessment, and whether there are updates to the agent components.|Client|  

For more information, see [Windows Update log files](/windows/deployment/update/windows-update-logs).

### <a name="BKMK_WSUSLog"></a> WSUS server

The following table lists the log files that contain information related to the WSUS server.  

|Log name|Description|Computer with log file|  
|--------------|-----------------|----------------------------|  
|Change.log|Records details about WSUS server database information that has changed.|WSUS server|  
|SoftwareDistribution.log|Records details about the software updates that are synced from the configured update source to the WSUS server database.|WSUS server|  

These log files are located in the `%ProgramFiles%\Update Services\LogFiles` folder.

## See also

- [About log files](about-log-files.md)

- [Support Center OneTrace](../../support/support-center-onetrace.md)

- [Support Center log file viewer](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
