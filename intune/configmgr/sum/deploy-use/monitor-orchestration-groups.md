---
title: Monitor orchestration groups
titleSuffix: Configuration Manager
description: Monitor and reset orchestration groups.
ms.date: 07/11/2022
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: article
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Monitor orchestration groups in Configuration Manager
<!--3098816-->
*Applies to: Configuration Manager (current branch)*

After you create, edit, or start an orchestration group, you may need to monitor the group or its members. Using monitoring information along with the log files, can help you troubleshoot orchestration groups and group members.  

## Monitor orchestration groups

From the **Assets and Compliance** workspace, select the **Orchestration Group** node. Add any of the following columns to get information about the groups:

- **Orchestration Name**: The name of your orchestration group.
- **Site Code**: Site code for the group.
- **Orchestration Type**: is one of the following types:
   - Number
   - Percentage
   - Sequence

- **Orchestration Value**: How many members or the percentage of members that can get a lock simultaneously. **Orchestration Value** is only populated when **Orchestration Type** is either *Number* or *Percentage*.  
- **Orchestration State**: In progress during orchestration. Idle when not in progress.
- **Orchestration Start Time**: Date and time that the orchestration started.
- **Current Sequence Number**: Indicates for which member of the group orchestration is active. This number corresponds with the **Sequence Number** for the member.  
- **Orchestration Timeout (in minutes)**: Value of **The Orchestration Group timeout (in minutes)** set on the **General** page when creating the group, or the **General** tab when editing the group.
- **Orchestration Group Member Timeout (in minutes)**: Value of **Orchestration Group member timeout (in minutes)** set on the **General** page when creating the group, or the **General** tab when editing the group.
- **Orchestration Group ID**: ID of the group, The ID is used in logs and the database.
- **Orchestration Group Unique ID**: Unique ID of the group, The Unique ID is used in logs and the database.
- **Last Modified Time**: The time the orchestration group was last modified (starting in version 2203). <!--12500680, 12976470-->
- **Last Modified By**: The user that last modified the orchestration group (starting in version 2203). <!--12500680, 12976470-->

## Orchestration groups details tabs

*(Introduced in version 2107*)

Starting in Configuration Manager version 2107, the following two tabs were added to the details pane for **Orchestration Groups** to assist you with monitoring the [script approval](create-orchestration-groups.md#approvals-for-orchestration-group-scripts): <!--9957939-->

- **Summary**: Contains information about the selected orchestration group, including the **Approval State** of scripts.
- **Scripts**: Lists information about pre and post-scripts, including the timeout, approver, and approval state for each script.

## Monitor orchestration group members

In the **Orchestration Group** node, select an orchestration group. In the ribbon, select **Show Members**. You can see the members of the group, and their orchestration status. Add any of the following columns to get information about the members:

- **Name**: Device name of the orchestration group member
- **Current State**: Gives you the state of the member device.
   - **In progress** during orchestration.
   - **Waiting**: Indicates the client is waiting on the lock for its turn to install updates.
   - **Idle** when orchestration is complete or not running.
- **State Code**: You can right-click on the Orchestration Group member and select **Reset Orchestration Group Member**. This reset allows you to rerun orchestration. States include: 
   - Idle
   - Waiting, the device is waiting its turn
   - In progress, installing an update
   - Failed
   - Reboot pending
- **Lock Acquired Time**: Locks are requested by the client based on its policy. Once the client acquires a lock, orchestration is triggered on it.  
-**Last State Reported Time**: Time the member last reported a state.
- **Sequence Number**: The client's location in the queue for installing updates.
- **Site Code**: The site code for the member.
- **Client Activity**: Tells you if the client is active or inactive.
- **Primary User(s)**: Which users are primary for the device.
- **Client Type**: What type of device the client is.
- **Currently Logged on User**: Which user is currently logged on to the device.
- **OG ID**: ID of the orchestration group the member belongs to.
- **OG Unique ID**: Unique ID of the orchestration group the member belongs to.
- **Resource ID**: Resource ID of the device.

## <a name="bkmk_alerts"></a> Alerts for orchestration groups
*(Introduced in version 2203)*

Starting in version 2203, if an orchestration group fails, an alert is generated. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Alerts**, and then select **Active Alerts** or **All Alerts**. For more information about alerts, see [Configure alerts](../../core/servers/manage/configure-alerts.md).

## Log files

Use the following log files on the site server to help monitor and troubleshoot:

### Site server

- **Policypv.log**: shows that the site targets the orchestration group to the clients.
- **SMS_OrchestrationGroup.log**: shows the behaviors of the orchestration group.

### Client

- **MaintenanceCoordinator.log**: Shows the lock acquisition, update installation, pre and post-scripts, and lock release process.
- **UpdateDeployment.log**: Shows the update installation process.
- **PolicyAgent.log**: Checks if the client is in an orchestration group.

## Next steps

- [Orchestration groups prerequisites](orchestration-groups.md)
- [Create, edit, and use orchestration groups](create-orchestration-groups.md)
