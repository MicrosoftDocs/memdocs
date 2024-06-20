---
title: Status and alert views
titleSuffix: Configuration Manager
description: Information about Configuration Manager component behavior and data flow.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: 40851148-f8ff-4959-b884-164fec0563e7
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Status and alert views in Configuration Manager

Configuration�Manager status messages report information about Configuration Manager component behavior and data flow and are categorized by severity and type. State messages are sent by Configuration Manager clients to site systems based on important changes of state, providing a snapshot of the state of a process at a specific time. Status summarizers produce summaries of the status and state messages and provide a snapshot of the status and health of site systems, components, software updates compliance, and so on.

Status message instances consist of properties that are stored in the database, which are represented primarily by the **v_StatusMessage** view, and message strings stored in dynamic-link library (DLL) files. When you view a message by using the Configuration Manager console, **Status Message Viewer**, and the **Status Message Details** page in **Report Viewer**, Configuration Manager creates the instance of status messages by combining the various parts.

The following sections provide detailed information about status message views, state message views, and status summarizer views.

## Status message views

The status views are described in this section.

### v_AdvertisementStatusInformation

Lists all deployment status message IDs, the message state, and the message name, such as succeeded, expired, failed, and retrying. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other advertisement status views by using the **MessageID** column.

### v_ClientAdvertisementStatus

Lists all package and program deployments with the associated status for system resources that have been targeted. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AdvertisementID**, **ResourceID**, and **LastStatusMessageID** columns.

### v_ClientMessageStatistics

Lists all Configuration Manager clients, by resource ID, the last time the client sent and processed a status message, and the last time a resynchronization was issued and completed on the client.
This view can be joined to other views by using the **ResourceID** column.

### v_DCMClientStatusInformation

Lists all possible compliance settings client states. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
It is unlikely that this view will be joined to other views.

### v_PackageStatus

Lists the status for all deployments, as well as the package server location, last update time, and so on. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **PackageID** column.

### v_PeerDPStatusInfo

Lists the peer distribution point states and associated state names.
It is unlikely that this view will be joined to other views.

### v_ServerMessageStatistics

Lists the site system servers, the associated site code, when the last heartbeat occurred, and how long the heartbeat took to process. The view is also listed and described in the [Site Administration Views in Configuration Manager](site-admin-views-configuration-manager.md) topic.
The view can be joined to other views by using the **ServerName** column.

### v_StatMsgAttributes

Lists the attributes for all status messages (for example, package ID, collection ID, user name, object GUID, and so on).
The view can be joined to the **v_StatusMessage** and **v_StatMsgInsStrings** views by using the **RecordID** column.

### v_StatMsgInsStrings

Lists the status insertion strings for all status messages.
The view can be joined to the **v_StatusMessage** and **v_StatMsgAttributes** views by using the **RecordID** column.

### v_StatMsgModuleNames

Lists the status message module names with associated module DLL name. By default, Configuration Manager has the SMS Client, SMS Provider, and SMS Server module names.
It is unlikely that this view will be joined to other views.

### v_StatusMessage

Lists information about all status messages, including status message ID, time of status message, severity, site code, and so on.
The view can be joined to the **v_StatMsgAttributes** and **v_StatMsgInsStrings** views by using the **RecordID** column, and to other views by using the **MachineName** column.

### v_TaskExecutionStatus

Lists the status for operating system deployment task sequence steps, as well as the advertisement ID, resource ID, action name, and so on. The view is also listed and described in the [Operating System Deployment Views in Configuration Manager](operating-system-deployment-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AdvertisementID** and **ResourceID** columns.

### v_WOLCommicationErrorStatus

Lists the Wake on LAN error status messages, as well as the time of the error, batch ID, object type, ID, and error code. The view is also listed and described in the [Wake On LAN Views in Configuration Manager](wake-lan-views-configuration-manager.md) topic.
It is unlikely that this view will be joined to other views.

### v_StatusMessagesAlerts

Lists, by record ID, recently generated alerts. This includes the severity of the alert, the alert text and more.
This view can be joined to other views by using the **AlertSeverity**, **Name**, **TypeInstanceID** or **MachineName** columns.

## State views

The state views list the state messages sent by Configuration Manager clients to site systems and can generally be joined to system data, other state message views, deployment views, and more. The Configuration Manager states are listed in the **v_StateNames** view. When creating reports by using state views, you will likely want to join the **v_StateNames** view with another state view by using the **StateType** and **StateID** columns to retrieve the friendly names for the state and to use the **v_StateNames** view to determine the criteria to filter the SQL statement. Each state message type has multiple state IDs, which start at 1 for each message type. When joining to a view that contains information for more than one state type, you will need to either join to the other view by using both the **StateType** and **StateID** columns or join to the other view by using the **StateID** column and filter the query with for the specific **StateType**. For example, if you join to another view by using the **StateID** column, you could filter the results by **StateType**=300.

### v_AssignmentState_Combined

Lists the last state message received from Configuration Manager client computers for assigned software update deployments, including the assignment ID (deployment ID), resource ID, state type, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **StateType**, and **StateID** columns.

### v_AssignmentStatePerTopic

Lists the last state message for each state type received from Configuration Manager client computers for assigned software update deployments, including assignment ID (deployment ID), resource ID, state type, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **TopicType**, and **StateID** columns.

### v_CIAssignmentStatus

Lists the enforcement and evaluation state messages received from Configuration Manager client computers for all assigned configuration items, including assigned software update deployments and assigned configuration baselines. The assignment ID, resource ID, the last enforcement state message ID, the last evaluation state message ID, and so on are provided. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **LastEnforcementMessageID**, and **LastEvaluationMessageID** columns. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 402. The **LastEvaluationMessageID** column provides the state ID for state messages with a topic type of 400.

### v_CIComplianceHistory

Lists the configuration items, by **CI_UniqueID** and **CI_ID**, that are configuration baselines or configuration items within a configuration baseline, that have been assigned to a Configuration Manager client, listed by **ResourceID**, and compliance information for the configuration item. The information includes the compliance start and end dates, whether the configuration item is applicable to the client, whether the client is compliant for the configuration item, and so on. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_UniqueID**, **CI_ID**, and **ResourceID** columns.

### v_CIComplianceStatusDetail

Lists the configuration items, by **CI_ID** and **CI_UniqueID**, that are in a configuration baseline, have been assigned to a Configuration Manager client, listed by **ResourceID**, and have a state value of **Non-Compliant**. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **CI_UniqueID**, **ResourceID**, and **ModelName** columns.

### v_CICurrentComplianceStatus

Lists the compliance and enforcement states for configuration items, by configuration item ID, as well as the resource ID, whether the configuration item is applicable to the resource, and information related to the compliance and evaluation of the configuration item. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **CI_UniqueID**, **ModelName**, **ComplianceState**, and **LastEnforcementMessageID** columns. The **ComplianceState** column provides the state ID for state messages with a topic type of 401. The **LastEnforcementMessageID** column provides the state ID for state messages with a state message topic type of 402.

### v_ClientDeploymentState

Lists all Configuration Manager clients, by SMSID, and the last client deployment state reported, as well as the fully qualified domain name (FQDN), NetBIOS name, assigned site code, client version, and so on. The view is also listed and described in the [Client Deployment Views in Configuration Manager](client-deployment-views-configuration-manager.md) topic.
The view can be joined to other views by using the **SMSID**, **FQDN**, **NetBiosName**, and **LastMessageStateID** columns. The **LastMessageStateID** column contains the state ID for topic type 800. The Configuration Manager states are listed in the **v_StateNames** view.

### v_ClientHealthState

Lists all Configuration Manager clients, by SMSID, the last client health state reported for each state type, the fully qualified domain name (FQDN), NetBIOS name, assigned site code, health type, health state, health state name, and so on. The view is also listed and described in the [Client Status Views in Configuration Manager](client-status-views-configuration-manager.md) topic.
The view can be joined to other views by using the **SMSID**, **FQDN**, **NetBiosName**, **HealthType**, and **HealthState** columns. The **HealthType** column contains the topic type and the **HealthState** column contains the state ID. Client health state messages have a state type from 1000 to 1004. The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientDeploymentState

Lists all Configuration Manager mobile device clients, by device client ID, NetBIOS name, and device ID, and the last device deployment state reported, as well as the assigned site code, device client version, and so on. The view is also listed and described in the [Mobile Device Management Views in Configuration Manager](mobile-device-management-views-configuration-manager.md) and [Client Deployment Views in Configuration Manager](client-deployment-views-configuration-manager.md) topics.
The view can be joined to other views by using the **DeviceClientID**, which contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view, **DeviceNetBiosName**, and DeviceDeploymentState columns. The **DeviceDeploymentState** column contains the state ID for topic type 800. The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientHealthState

Lists all Configuration Manager mobile device clients, by device client ID, NetBIOS name, and device ID, and the health state of the device, as well as the assigned site code, owner name, and so on. The view is also listed and described in the [Mobile Device Management Views in Configuration Manager](mobile-device-management-views-configuration-manager.md) and [Client Status Views in Configuration Manager](client-status-views-configuration-manager.md) topics.
The view can be joined to other views by using the **DeviceClientID**, which contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view, **DeviceNetBiosName**, **DeviceID**, **HealthType**, and **HealthState** columns. The **HealthType** column contains the topic type and the **HealthState** column contains the state ID. Client health state messages have a state type from 1000 to 1004. The Configuration Manager states are listed in the **v_StateNames** view.

### v_StateNames

Lists all states that can be reported by Configuration Manager clients by topic type, state ID, state name, and state description. Each state topic type defines a specific function, and each topic type contains multiple state IDs.
The view can be joined to other views by using the **TopicType** and **StateID** columns.

### v_Update_ComplianceStatusAll

Lists the detection state for all software updates that have been scanned for compliance on Configuration Manager clients, as well as the resource ID of the client, last enforcement state ID, enforcement source, last status check time, and so on. The **v_Update_ComplianceStatusAll** view combines information from the **v_Update_ComplianceStatusReported** and **v_UpdateComplianceStatus_Unknown** views. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **Status**, and **LastEnforcementMessageID** columns. The Status column provides the state ID for state messages with a topic type of 500. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 402.

### v_Update_ComplianceStatusReported

Lists the detection state for all software updates that have been scanned for compliance on Configuration Manager clients, as well as the resource ID of the client, last enforcement state ID, enforcement source, last status check time, and so on. The **v_Update_ComplianceStatusReported** view combines information from the **v_UpdateComplianceStatus** and **v_UpdateComplianceStatus_NotApplicable** views. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **Status**, and **LastEnforcementMessageID** columns. The **Status** column provides the state ID for state messages with a topic type of 500. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 402.

### v_UpdateAssignmentStatus

Lists the software update deployment assignments, the system resources that have been targeted, the last compliance state for the deployment, the last enforcement state for the deployments, the last evaluation state for the deployment, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID**, ResourceID, **LastComplianceMessageID**, **LastEnforcementMessageID**, and **LastEvaluationMessageID** columns. The **LastComplianceMessageID** column provides the state ID for state messages with a topic type of 300. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 301. The **LastEvaluationMessageID** provides the state ID for state messages with a topic type of 302.

### v_UpdateAssignmentStatus_Live

Lists the software update deployment assignments, the system resources that have been targeted, the last compliance state for the deployment, the last enforcement state for the deployments, the last evaluation state for the deployment, and so on. The **v_UpdateAssignmentStatus_Live** view contains a subset of information from the **v_UpdateAssignmentStatus** view. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **LastComplianceMessageID**, **LastEnforcementMessageID**, and **LastEvaluationMessageID** columns. The **LastComplianceMessageID** column provides the state ID for state messages with a topic type of 300. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 301. The **LastEvaluationMessageID** provides the state ID for state messages with a topic type of 302.

### v_UpdateComplianceStatus

Lists the detection state for all software updates that have been scanned for compliance on Configuration Manager clients, as well as the resource ID of the client, last enforcement state ID, enforcement source, last status check time, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **Status**, and **LastEnforcementMessageID** columns. The **Status** column provides the state ID for state messages with a topic type of 500. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 402.

### v_UpdateScanStatus

Lists the Configuration Manager client computers, by resource ID, that have scanned for software updates compliance and the last scan state, as well as the last scan time, last error code, last Windows Update Agent version, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **ResourceID**, **UpdateSource_ID**, and **LastScanState** columns.

> [!NOTE]
> The **LastScanState** column provides the state ID for state messages with a topic type of 501.

### v_UpdateState_Combined

Lists the detection state for software updates that are not required on Configuration Manager client computers and the enforcement state for software updates that are required on Configuration Manager client computers, as well as the state ID, state time, enforcement source, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **StateType**, and **StateID** columns.

> [!NOTE]
> A value of 402 in the **StateType** column is for enforcement state, and a value of 500 is for software update detection state.

## Status summarizer views

Status summarizers produce summaries from status messages, state messages, and other data in the Configuration Manager site database. Status summaries are produced in real time as the summarizers receive status and state messages from Configuration Manager components and clients. You can use status summarizers to view a snapshot of the status and health of the site systems, components, deployments, software updates compliance, client health, and so on.

Data in a status summary is classified as either a count or a state. A count is a tally of events that occurs over a specific period of time, such as the number of error status messages reported by a component since the beginning of the week. A state is the last known condition of something, such as the number of free bytes that is available for the Configuration Manager site database.

Each of the status summaries contains some state data. Only the component status and advertisement status summaries contain count data. The status summarizer views contain data such as the number of information, warning, and error messages for a site within a specified interval and the state of all components in a site at a specified interval.

Each of the status message summarizer views are listed and described in this section.

### v_AssignmentEnforcementSummaryPerUpdateAndState

Lists the software update deployments, by assignment ID, the software updates in the deployment, by **CI_ID**, the enforcement state name, the count of Configuration Manager client computers that are in the enforcement state, and the total count of client computers that have been targeted for the deployment. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID** and **CI_ID** columns.

> [!NOTE]
> The enforcement states listed in this view have a state type of 402.

### v_AssignmentSummaryPerTopic

Lists the assignments, by assignment ID, the type of assignment state message, the state ID for the type, the count of Configuration Manager client computers that are in the assignment state, and the total count of client computers that have been targeted for the assignment. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **AssignmentID** column.

> [!NOTE]
> There are three deployment assignment states. State type of 300 is assignment compliance, type 301 is assignment enforcement, and type 302 is assignment evaluation. You can find a list of the state IDs by looking in the **v_StateNames** view.

### v_CH_ClientSummary

Lists summarized client status information for all Configuration Manager client computers, such as last heartbeat discovery, last hardware and software inventory scan, last policy request, whether there are possible certificate issues, and so on. The view is also listed and described in the [Client Status Views in Configuration Manager](client-status-views-configuration-manager.md) topic.
The view can be joined to other views by using the **MachineID**, **NetBiosName**, and **SiteCode** columns.

### v_CH_ClientSummaryHistory

Lists a summarization of the client status information for all Configuration Manager client computers, such as total number of clients, total number of clients that are active based on the last heartbeat discovery, hardware and software inventory scans, and so on. The view is also listed and described in the [Client Status Views in Configuration Manager](client-status-views-configuration-manager.md) topic.
It is unlikely that this view will be joined to other views.

### v_CIComplianceSummary

Lists the compliance settings configuration baselines, by **CI_ID**, and the count of Configuration Manager client computers that have been targeted, how many clients are compliant, how many have failed the compliance evaluation, the count of client computers that are noncompliant, and so on. The view is also listed and described in the [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID** and **CI_UniqueID** columns.

### v_ClientOfferSummary

Lists the standard package and program deployments, by **OfferID**, the count of Configuration Manager client computers that have been targeted, and the count of computers reporting not started, waiting, running, retrying, failed, and succeeded status for the deployment. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **OfferID** and **PkgID** columns.

### v_ComponentSummarizer

Lists summary status information for all Configuration Manager components for different intervals. The view also provides the site code, server name, component name, the count of information, warning, and error messages, and so on. The information in this view contains the same information that is displayed in the **Component Status** node of the Configuration Manager console, but the view contains information for all display intervals. The view is also listed and described in the [Site Administration Views in Configuration Manager](site-admin-views-configuration-manager.md) topic.

> [!NOTE]
> The value in the **Status** column provides the current status for the component. A value of 0 indicates that the component is OK, a value of 1 indicates a warning state for the component, and a value of 2 indicates a critical state for the component.

The view can be joined to other views by using the **SiteCode**, **MachineName**, and **ComponentName** columns.

### v_FileUsageSummary

Lists software metering summary status information for file usage by site. The view is also listed and described in the [Software Metering Views in Configuration Manager](software-metering-views-configuration-manager.md) topic.
The view can be linked by using the **FileID** column.

### v_FileUsageSummaryIntervals

Lists software metering summary interval information for file usage. The view is also listed and described in the [Software Metering Views in Configuration Manager](software-metering-views-configuration-manager.md) topic.
It is unlikely that this view will be joined to other views.

### v_INSTALLED_SOFTWARE_DATA_Summary

Lists the count of the installed software applications on Configuration Manager clients found through Asset Intelligence. This view contains the same source information as the **v_GS_INSTALLED_SOFTWARE** view, but provides summary information instead of listing the individual system resources. The view is also listed and described in the [Asset Intelligence Views in Configuration Manager](asset-intelligence-views-configuration-manager.md) topic.
It is unlikely that this view will be joined to other views.

### v_MonthlyUsageSummary

Lists the Configuration Manager client computers, by **ResourceID**, and the usage summary for metered files, as well as the logged-on user name, usage time, and time of last usage. The view is also listed and described in the [Software Metering Views in Configuration Manager](software-metering-views-configuration-manager.md) topic.
The view can be joined to other views by using the **ResourceID**, **FileID**, and **MeteredUserID** columns.

### v_PackageStatusDetailSumm

Lists all applications, task sequences, and packages and programs, by **PackageID**, the originating site code, package name, site name, source version, the date for the summary information, the targeted count for each package, and the count for installed, retrying, and failed status. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **PackageID** column.

### v_PackageStatusDistPointSumm

Lists all content packages, by **PackageID**, and the installation status for the package source files on all associated distribution points. The view also provides information such as the site code, path to the distribution point, path to source location, time of last copy, and so on. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **PackageID** and **ServerNALPath** columns.

### v_PackageStatusRootSummarizer

Lists all applications, task sequences, and packages and programs, by **PackageID**, the package name, source version, source date, the source site, size of the source files, the targeted count for each package, and the count for installed, retrying, and failed status. The view is also listed and described in the [Application Management Views in Configuration Manager](application-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **PackageID** column.

### v_SiteDetailSummarizer

Lists status summary information for all Configuration Manager sites, by **SiteCode**, for different intervals. The view also provides the site name, site version, interval, the count of information, warning, and error messages, and so on. The information in this view contains the same information that is displayed in the **Site Status** node of the Configuration Manager console, but the view contains information for all display intervals. The view is also listed and described in the [Site Administration Views in Configuration Manager](site-admin-views-configuration-manager.md) topic.
The view can be joined to other views by using the **SiteCode** column.

> [!NOTE]
> The value in the **Status** column provides the current status for the site. A value of 0 indicates that the site is OK, a value of 1 indicates a warning state for the site, and a value of 2 indicates a critical state for the site.

### v_SiteSystemSummarizer

Lists status summary information for all Configuration Manager sites systems for different intervals. The view also provides the object location, the site role for the site system, total disk space, free disk space, and percentage of free disk space for the site system, the time of the last status reported, and whether the site system is available. The information in this view contains the same information that is displayed in the Site System Status node of the Configuration Manager console. The view is also listed and described in the [Site Administration Views in Configuration Manager](site-admin-views-configuration-manager.md) topic.
The view can be joined to other views by using the **SiteCode** column.

### v_SummarizationInterval

Lists the status summarization interval.
It is unlikely that this view will be joined to other views.

### v_SummarizerRootStatus

Lists the root summary status, which is the same status displayed on the **System Status** node of the Configuration Manager console.
It is unlikely that this view will be joined to other views.

### v_SummarizerSiteStatus

Lists the site summary status, which is the same status displayed for the &lt;<em>site code</em>&gt; - &lt;<em>site name</em>&gt; node of the Configuration Manager console. The view is also listed and described in the [Site Administration Views in Configuration Manager](site-admin-views-configuration-manager.md) topic.
The view can be joined to other views by using the **SiteCode** column.

### v_SummaryTasks

Lists the tasks, by name and command, used to summarize Configuration Manager information, as well as the run interval, last run duration, when the task last completed successfully, next start time, and so on.
It is unlikely that this view will be joined to other views.

### v_Update_ComplianceSummary

Lists all software updates, by **CI_ID**, the last time summarization was run, the total count of client computers, the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID** column.

### v_Update_ComplianceSummary_Live

Lists all software updates, by CI_ID, the last time summarization was run, the total count of client computers, the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states, and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID** column.

### v_Update_DeploymentSummary_Live

Lists all software updates, by **CI_ID**, in active software update deployments, listed by AssignmentID, and summarized state reported by targeted clients. The view includes the target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states; the number of clients that have installed the software update and failed to install the update; and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **AssignmentID**, and **CollectionID** columns.

### v_UpdateDeploymentSummary

Lists all software updates, by **CI_ID**, in software update deployments, listed by **AssignmentID**, and summarized state reported by targeted clients. The view includes the target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states; the number of clients that have installed the software update and failed to install the update; and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID**, **AssignmentID**, and **CollectionID** columns.

> [!NOTE]
> This view has been deprecated, no longer generates summary data, and may be removed in the future.

### v_UpdateEnforcementSummaryPerCollection

Lists the summary state for all software updates that have been deployed. The view provides the software update, by **CI_ID**, target collection, collection name, and summarized enforcement state reported by clients in the collection. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID** column.

### v_UpdateSummaryPerCollection

Lists the summary state for all software updates and the compliance state per collection. The view includes the software update, by **CI_ID**; target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting not applicable, missing (required), present (already installed), and unknown states; and so on. The view is also listed and described in the [Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md) topic.
The view can be joined to other views by using the **CI_ID** and **CollectionID** columns.

## Alert views

The alerts views are listed in this section.

### v_Alert

Lists information about the events than can be generated by Configuration Manager. This includes the severity of the alert, when it was created, and who created it.
This view can be joined to other views by using the **Name** and **Severity** columns.

### v_AlertEvents

Lists information about the events that have been triggered on the Configuration Manager site.
This view can be joined to other views by using the **AlertID** and EventMachineID columns.

### v_AlertValidFeatureArea

Lists information about each product component, by feature area ID, that might generate alerts.
It is unlikely that this view will be joined to other views.

### v_AlertVariable_G

Lists system information about variables that are assigned to alerts.
It is unlikely that this view will be joined to other views.

### v_SMS_Alert

Lists information about the built-in, and user created alerts that might be displayed in the Configuration Manager console.
It is unlikely that this view will be joined to other views.

### v_Report_StatusMessageDetail

Lists detailed information about status messages returned by each Configuration Manager component. This includes the record ID, the time of the status message, the component that generated the message, and more.
This view can be joined to other views by using the **RecordID** column.

### v_StateMessageStatistics

Lists information about the number of state messages returned for each topic type.
It is unlikely that this view will be joined to other views.

### v_StatMsgWithInsStrings

Lists detailed information about status messages returned by each Configuration Manager component. This includes the record ID, the time of the status message, the component that generated the message, and more.
This view can be joined to other views by using the **RecordID** column.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
