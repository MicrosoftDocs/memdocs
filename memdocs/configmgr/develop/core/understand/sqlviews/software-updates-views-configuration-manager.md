---
title: Software updates views
titleSuffix: Configuration Manager
description: Information about the software updates metadata, software update groups, and software update bundles.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 1e6741d2-7737-4446-b65f-e6e330c09458
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Software updates views in Configuration Manager

The Configuration Manager software updates views contain information about the software updates metadata, software update groups, software update bundles, and so on. Many of the status and status summarizer views provide information about software updates compliance, software update deployment evaluation and enforcement state, scan states, compliance status summarization, deployment status summarization, and so on. The compliance state for clients using an inventory scan tool, such as the Inventory Tool for Microsoft Updates, are picked up during the hardware inventory cycle and stored in the inventory views.

The following sections provide detailed information about software updates views, software updates status views, software updates status summarizer views, and software updates hardware inventory views.

## Software updates views

The software updates views contain information about software updates. When creating software updates reports for individual software updates or update bundles, the **v_UpdateCIs** or **v_UpdateInfo** views will most often be used in combination with other views. The software update views are described in this section.

### v_AuthListInfo

Lists the software update groups, by CI_ID, for the Configuration Manager hierarchy, including when the software update group was created, when it was last modified, who last modified the software update group, source site, title, description, and so on. This view contains a subset of information from the **v_ConfigurationItems** view, joins the **v_LocalizedCIProperties** view to retrieve software update group title and description information, and filters the information by **CIType**=9, which indicates an software update group configuration item.
The view can be joined to other views by using the **CI_ID**, **CI_UniqueID**, and **SDMPackage_ID** columns.

### v_EULAContent

Lists the license terms, by **EULAContentID** and **EULAContentUniqueID**, associated with software updates. The license terms text is in binary format.
The view can be joined to the **v_CIEULA_LocalizedContent** view, which associates the software update (configuration item) to the license terms, by using the **EULAContentUniqueID** column.

### v_ScannedUpdates

Lists all software updates, by **CI_ID**, that have been scanned for software updates compliance on Configuration Manager clients, including Resource ID, scan time, and last local change time.
The view can be joined to other views by using the **CI_ID** and **ResourceID** columns.

### v_SoftwareUpdateSource

Lists all sources for the software updates metadata, by **UpdateSource_ID**, for the site. Configuration Manager sites should use **WSUS Enterprise Server** as the update source and **WUA** as the scan method.
The view can be joined to the **v_UpdateScanStatus** view by using the **UpdateSource_ID** column.

### v_UpdateCIs

Lists all of the software updates configuration items, by **CI_ID** and **CI_UniqueID**. The information in this view is a subset of information from the **v_ConfigurationItems** view, retrieving all records where the configuration type is **Software Updates** or **Software Updates Bundle** (**CIType**=1 or 8), including article ID, bulletin ID, severity, date created, whether the update is deployed, and so on.
The view can be joined to other views by using the **CI_ID**, **CI_UniqueID**, and **SDMPackage_ID** columns.

### v_UpdateContents

Lists the software updates configuration items that have associated content, by CI_ID, the configuration item ID for the software update in which the content is associated, the content ID, whether the content has been provisioned, the locale for the content, and so on. The configuration item ID for a software updates bundle is listed multiple times in the **CI_ID** column, and the configuration item IDs for the software updates that are part of the bundle are listed in the **ContentCI_ID** column. For example, a software update that is not a bundle would have the same configuration item ID in the **CI_ID** and **ContentCI_ID** columns. A software updates bundle would have one listing with the configuration item ID in the **CI_ID** column and the same configuration item ID in the **ContentCI_ID** columns, and then would have new listings containing the configuration item ID for the bundle in the **CI_ID** column and the configuration item ID for the bundled software updates in the **ContentCI_ID** column. The **ContentLevel** column represents how many times a configuration item ID is listed in the **ContentCI_ID** column.
The view can be joined to other views by using the **CI_ID** and **Content_ID** columns and to the **v_CIContents_All** view by using the **ContentCI_ID** column.

### v_UpdateInfo

Lists stand-alone software updates (CIType_ID = 1) or software update groups (CIType_ID = 9), by **CI_ID**, and information about the update or bundle, such as configuration item type, configuration item version, data created, date last modified, whether the update or bundle has been deployed, associated bulletin ID, article ID, severity, and so on. Unlike the Configuration Manager console when it displays software updates, this view does not list the updates that are part of an update bundle.
The view can be joined to other views by using the **CI_ID**, **CI_UniqueID**, and **SDMPackage_ID** columns.

## Software updates status views

The software updates status views provide information about software updates compliance, deployment evaluation, deployment enforcement, scan state, and so on. These views can generally be joined to other software updates and desired configuration management views by using the **CI_ID** column. For more information about the status views, see [Status and Alert Views in Configuration Manager](status-alert-views-configuration-manager.md). The status views that contain software updates information are described in this section.

### v_AssignmentState_Combined

Lists the last state message received from Configuration Manager client computers for assigned software update deployments, including the assignment ID (deployment ID), resource ID, state type, and so on.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **StateType**, or **StateID** columns.

### v_AssignmentStatePerTopic

Lists the last state message for each state type received from Configuration Manager client computers for assigned software update deployments, including assignment ID (deployment ID), resource ID, state type, and so on.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **TopicType**, and **StateID** columns.

### v_UpdateAssignmentStatus

Lists the software update deployment assignments, the system resources that have been targeted, the last compliance state for the deployment, the last enforcement state for the deployments, the last evaluation state for the deployment, and so on.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **LastComplianceMessageID**, **LastEnforcementMessageID**, and **LastEvaluationMessageID** columns. The **LastComplianceMessageID** column provides the state ID for state messages with a topic type of 300. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 301. The **LastEvaluationMessageID** provides the state ID for state messages with a topic type of 302.

### v_UpdateAssignmentStatus_Live

Lists the software update deployments, the system resources that have been targeted, the last compliance state for the deployment, the last enforcement state for the deployments, the last evaluation state for the deployment, and so on. The **v_UpdateAssignmentStatus_Live** view contains a subset of information from the **v_UpdateAssignmentStatus** view.
The view can be joined to other views by using the **AssignmentID**, **ResourceID**, **LastComplianceMessageID**, **LastEnforcementMessageID**, and **LastEvaluationMessageID** columns. The **LastComplianceMessageID** column provides the state ID for state messages with a topic type of 300. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 301. The **LastEvaluationMessageID** provides the state ID for state messages with a topic type of 302.

### v_Update_ComplianceStatus

Lists the detection state for all software updates that have been scanned for compliance on Configuration Manager clients, as well as the resource ID of the client, last enforcement state ID, enforcement source, last status check time, and so on.
The view can be joined to other views by using the **CI_ID**, **ResourceID**, **Status**, and **LastEnforcementMessageID** columns. The Status column provides the state ID for state messages with a topic type of 500. The **LastEnforcementMessageID** column provides the state ID for state messages with a topic type of 402.

### v_UpdateScanStatus

Lists the Configuration Manager client computers, by resource ID, that have scanned for software updates compliance and the last scan state, as well as the last scan time, last error code, last Windows Update Agent version, and so on.
The view can be joined to other views by using the **ResourceID**, **UpdateSource_ID**, and **LastScanState** columns.

> [!NOTE]
> The **LastScanState** column provides the state ID for state messages with a topic type of 501.

### v_UpdateState_Combined

Lists the detection state for software updates that are not required on Configuration Manager client computers or the enforcement state for software updates that are required on Configuration Manager client computers, as well as the state ID, state time, enforcement source, and so on.
The view can be joined to other views by using the **CI_ID** and **ResourceID** columns.

> [!NOTE]
> A value of 402 in the **StateType** column is for enforcement state, and a value of 500 is for compliance state.

## Software updates status summarizer views

The software updates status summarizers produce summaries from software updates state messages in the Configuration Manager site database. Status summaries are produced in real time as the summarizers receive state messages from Configuration Manager clients. The software updates status summarizer views provide summary information about software updates compliance, deployment evaluation, deployment enforcement, and scan state. For more information about the status summarizer views, see [Status and Alert Views in Configuration Manager](status-alert-views-configuration-manager.md). The software update status views are described in this section.

### v_AssignmentEnforcementSummaryPerUpdateAndState

Lists the software update deployments, by assignment ID, the software updates in the deployment, by **CI_ID**, the enforcement state name, the count of Configuration Manager client computers that are in the enforcement state, and the total count of client computers that have been targeted for the deployment.
The view can be joined to other views by using the **AssignmentID** and **CI_ID** columns.

> [!NOTE]
> The enforcement states listed in this view have a state type of 402.

### v_Update_ComplianceSummary

Lists all software updates, by **CI_ID**, the last time summarization was run, the total count of client computers, the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states, and so on.
The view can be joined to other views by using the **CI_ID** column.

### v_Update_ComplianceSummary_Live

Lists all software updates, by **CI_ID**, the last time summarization was run, the total count of client computers, the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states, and so on.
The view can be joined to other views by using the **CI_ID** column.

### v_Update_DeploymentSummary_Live

Lists all software updates, by **CI_ID**, in active software update deployments, listed by AssignmentID, and summarized state reported by targeted clients. The view includes the target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states; the number of clients that have installed the software update or failed to install the update; and so on.
The view can be joined to other views by using the **CI_ID**, **AssignmentID**, and **CollectionID** columns.

### v_UpdateDeploymentSummary

Lists all software updates, by **CI_ID**, in software update deployments, listed by assignment ID, and summarized state reported by targeted clients. The view includes the target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting unknown, not applicable, missing (required), and present (already installed) states; the number of clients that have installed the software update or failed to install the update; and so on.
The view can be joined to other views by using the **CI_ID**, **AssignmentID**, and **CollectionID** columns.

> [!NOTE]
> This view has been deprecated, no longer generates summary data, and may be removed in the future.

### v_UpdateEnforcementSummaryPerCollection

Lists the summary state for all software updates that have been deployed. The view provides the software update, by **CI_ID**, target collection, collection name, and summarized enforcement state reported by clients in the collection.
The view can be joined to other views by using the **CI_ID** column.

### v_UpdateSummaryPerCollection

Lists the summary state for all software updates and the compliance state per collection. The view includes the software update, by **CI_ID**; target collection ID and name; the time of the last summarization; the total number of client computers targeted; the count of client computers reporting not applicable, missing (required), present (already installed), and unknown states; and so on.
The view can be joined to other views by using the **CI_ID** and **CollectionID** columns.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
