---
title: Client deployment views
titleSuffix: Configuration Manager
description: Views that contain information about the deployment state of Configuration Manager client computers and devices.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 35e57dfe-b6b5-483d-8c6f-00363b5417f5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Client deployment views in Configuration Manager

There are no primary client deployment views, but there are status views that contain information about the deployment state of Configuration Manager client computers and devices. For more information about the status views, see [Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md). The status views that contain client deployment information are described in this section.

## Client deployment views

### v_ClientDeploymentState

Lists all Configuration Manager clients, by SMSID, and the last client deployment state reported, as well as the fully qualified domain name (FQDN), NetBIOS name, assigned site code, client version, and so on.

The view can be joined to other views by using the **SMSID**, **FQDN**, **NetBiosName**, and **LastMessageStateID** columns.

- **LastMessageStateID**: The state ID for topic type 800.

- **DeploymentBeginTime**: The last message time when the message's state ID is STATE_STATEID_CLIENT_DEPLOYMENT_STARTED (100), telling the server that the deployment starts. It clears the DeploymentEndTime time.<!-- SCCMDocs#1578 -->

- **DeploymentEndTime**: The last message time when the state ID is STATE_STATEID_CLIENT_DEPLOYMENT_SUCCEEDED (400) or STATE_STATEID_CLIENT_DEPLOYMENT_SUCCEEDED_REBOOT_SUCCEEDED (401). This tells the server that the deployment ends.

- **AssignmentBeginTime**: The time when getting state ID STATE_STATEID_CLIENT_ASSIGNMENT_STARTED (500).

- **AssignmentEndTime**: The time that the assignment was done with ID STATE_STATEID_CLIENT_ASSIGNMENT_SUCCEEDED (700).

- The Configuration Manager states are listed in the **v_StateNames** view.

### v_DeviceClientDeploymentState

Lists all Configuration Manager mobile device clients that are enrolled by Configuration Manager, by device client ID, NetBIOS name, and device ID, and the last device deployment state reported, as well as the assigned site code, device client version, and so on. This status view is also listed and described in [Mobile device management views in Configuration Manager](mobile-device-management-views-configuration-manager.md).

The view can be joined to other views by using the **DeviceClientID**, **DeviceNetBiosName**, and **DeviceDeploymentState** columns. The **DeviceDeploymentState** column contains the state ID for topic type 800. The **DeviceClientID** column contains the same information as the **SMS_Unique_Identifier0** column in the **v_R_System** view. The Configuration Manager states are listed in the **v_StateNames** view.

### v_CombinedDeviceResources

Lists information about all devices in the Configuration Manager site, by machine ID. The columns in this view display information such as the client name, GUID, operating system, assigned site code, domain, the client version and whether the device is a virtual machine.
This view can be joined to other views by using the **MachineID** column.

### v_CP_Machine

Lists information about client push attempts to install the client on computers. Includes the computer name, when the last attempt to install the client occurred, the assigned site code, the number of attempts made, and the current status.
This view can be joined to other views by using the **MachineID** column.

## Client notification views

Client notification in Configuration Manager lets some client operations be performed as soon as possible, instead of during the usual client policy polling interval. For example, you can use the client management task **Download Computer Policy** to instruct computers to download policy as soon as possible. Additionally, you can start some actions for Endpoint Protection, such as a malware scan of a client.

The client notification views are described in this section.

### v_BGB_ResTask

List information about the tasks performed on devices by Configuration Manager client notification.
This view can be joined to other views by using the **ResourceID** column.
 
### v_BGB_ResTaskPush

Lists information about the tasks deployed by Configuration Manager client notification, including the task ID, deployment ID, and status.
This view can be joined to other views by using the **ResourceID** column.
 
### v_BGB_Task

Lists information about all tasks that have been deployed by client notification. This includes the task ID, when the task was created and whether it has expired.
This view can be joined to other views by using the **TaskID** column.
 
### v_BgbMP

List the server name and database IDs of the management points that send out client notifications.
This view can be joined to other views by using the **ServerName** column.
 
### v_BgbServerCurrent

Lists status information about online and offline clients for each server that sends client notification requests.
This view can be joined to other views by using the **ServerID** column.
 
### v_ClientAction

Lists information about client notification actions that were taken. This information appears in the **Client Operations** node of the Configuration Manager console.
This view can be joined to other views by using the **ID** column.
 
### v_ClientActionImportance

Lists information about the priority of client notification tasks as shown in the **Client Operations** node of the Configuration Manager console.
This view can be joined to other views by using the **ClientOperationID** column.
 
### v_ClientActionResult

Lists information about the results of client notification actions that are shown in the **Client Operations** node of the Configuration Manager console.
This view can be joined to other views by using the **MachineID** column.
 
### v_ClientOperationInProcessing

Lists the ID number of client notification operations that are currently being processed.
It is unlikely that this view will be joined to other views.
 
### v_ClientOperationLinkedObjects

Lists information about objects that are linked to client notification actions.
It is unlikely that this view will be joined to other views.
 
### v_ClientOperationTargets

Lists information about the computers on which client notification actions took place.
This view can be joined to other views by using the **MachineID** column.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
