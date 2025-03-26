---
title: Client status views
titleSuffix: Configuration Manager
description: Information about the client status components on Configuration Manager client computers.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 9f7f8cc5-8173-4a3d-be97-02c1686a3751
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Client status views in Configuration Manager

Client status views contain information about the client status components on Configuration Manager client computers and the results of client checks. There are also status views that contain information about the health of Configuration Manager client computers, such as when the client last scanned for hardware and software inventory, the last policy request, and so on. Client status views will most often be joined to other views by using the **MachineID**, **ResourceID**, **NetbiosName**, **HealthStatus**, and **HealthType** columns.

The following sections provide detailed information about client status views.

## Client status views

The client status views contain status and status summary information about the health of Configuration Manager client computers. For more information about the status views, see [Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md). The status views that contain client status information are described in this section.

### v_CH_PolicyRequestHistory

Lists all Configuration Manager client computers and the time of the last policy request, which can be used to determine how many unique clients have requested policy within a given number of days.
The view can be joined to other views by using the **ResourceID** column.

### v_CH_ClientSummary

Lists client status information for all Configuration Manager client computers, such as the last time it was reported as being online, the last management point it contacted, the last time it reported hardware and software inventory, the last time a client health evaluation was performed, whether a remediation occurred and more.
The view can be joined to other views by using the **ResourceID** column.

### v_CH_ClientSummaryHistory

Lists a summarization of the client status information for all Configuration Manager client computers, such as total number of clients, total number of clients that are active based on the last heartbeat discovery, hardware and software inventory scans, and so on.
It is unlikely that this view will be joined to other views.

### v_ClientHealthState

Lists all Configuration Manager clients, by SMSID, and the last client health state reported for each state type, as well as the NetBIOS name, fully qualified domain name (FQDN), assigned site code, health type, health state, health state name, and so on.
The view can be joined to other views by using the **SMSID**, **NetBiosName**, **HealthType**, and **HealthState** columns. The **SMSID** column contains the same information as the **SMS_UniqueIdentifier0** column in the **v_R_System** view. The **HealthType** column in this view contains the same information as the **TopicType** column in the **v_StateNames** view and the **HealthState** column in this view contains the same information as the **StateID** column in the **v_StateNames** status view. Client health state messages have a state type from 1000 to 1004. The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientHealthState

Lists all Configuration Manager mobile device clients, by device client ID, NetBIOS name, and device ID, and the health state of the device, as well as the assigned site code, owner name, and so on. This status view is also listed and described in the [Mobile device management views in Configuration Manager](mobile-device-management-views-configuration-manager.md) topic.
The view can be joined to other views by using the **DeviceClientID**, **DeviceNetBiosName**, **HealthType**, and **HealthState** columns. The **DeviceClientID** column in this view contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view. The **HealthType** column in this view contains the same information as the **TopicType** column in the **v_StateNames** view and the **HealthState** column in this view contains the same information as the **StateID** column in the **v_StateNames** status view. Client health state messages have a state type from 1000 to 1004. The Configuration Manager states are listed in the **v_StateNames** view.

### v_CH_ClientSummaryCurrent

For each collection, lists, by collection ID, information about the status of client in that collection. The view contains information about the number of clients in the collection and which are active, the number of clients that have requested policy, the number of clients that have been remediated and more.
This view can be joined to other views by using the **CollectionID** column.

### v_CH_EvalResults

Lists the results, by resource ID of client status checks performed on each client in the site. This includes the NetBIOS name of each client, the last evaluation time, the results of the evaluation and more.
This view can be joined to other views by using the **ResourceID** column.

### v_CH_HealthCheckInfo

Lists information about each check that client check can perform on client computers, sorted by the ID number.
It is unlikely that this view will be joined to other views.

### v_CH_HealthCheckSummary

Lists information about the current client checks being performed by Configuration Manager, sorted by collection. The view shows the collection, the ID of the health check being performed (see **v_CH_HealthCheckInfo** to map this ID to the name of the client check), the number of computers in the collection that have performed the client check and the number of computers that still have to perform the client check.
This view can be joined to other views by using the **CollectionID** column.

### v_CH_PendingPolicyRequests

Lists information about pending policy requests including the GUID of the request, the time of the request and the management point that will process the request.
It is unlikely that this view will be joined to other views.

### v_CH_Settings

Lists information about the thresholds for client status reporting.
It is unlikely that this view will be joined to other views.

### v_ActiveClients

Lists information, by **MachineResourceID** about all active client computers in the site. This includes whether the client is on the Internet, the client version, information about certificates and more.
This view can be joined to other views by using the **MachineResourceID** column.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
