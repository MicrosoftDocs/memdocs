---
title: Monitor clients
titleSuffix: Configuration Manager
description: Learn how to monitor the health and activity of clients in Configuration Manager.
ms.date: 11/15/2021
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to monitor clients in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Once you install the Configuration Manager client on the Windows devices in your site, monitor their health and activity in the Configuration Manager console.

## About client status

Configuration Manager provides the following types of information as client status:

- **Client online status**: The site considers a device as **online** if it's connected to its assigned management point. To indicate that the client is online, it sends ping-like messages to the management point. If the management point doesn't receive a message in five minutes, the site considers the client as **offline**.

    > [!TIP]
    > These messages use the client notification channel. For more information, see [Ports used in Configuration Manager](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP).<!-- MEMDocs#1666 -->

- **Client activity**: The site considers the client as **active** if it has communicated with Configuration Manager in the past seven days. The site considers the client **inactive** if it hasn't done the following actions in seven days:

  - Requested policy update
  - Sent a heartbeat message
  - Sent hardware inventory

- **Client check**: The state of the periodic evaluation that the Configuration Manager client runs on the device. The evaluation checks the device and can remediate some of the problems it finds. For more information, see [Client health checks](client-health-checks.md).

  Client check runs automatically during the Windows maintenance window.

  You can configure remediation not to run on specific devices, for example, a business-critical server. For more information, see [How to configure client status](../deploy/configure-client-status.md#automatic-remediation-exclusion).

  If there are more items that you want to evaluate, use Configuration Manager compliance settings to monitor other configurations. For more information about compliance settings, see [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).

- **Decommissioned**: The site has marked the device record for deletion. This behavior can happen when a new registration for same device assigns to the same or a different primary site in a hierarchy. The site deletes these devices the next time it runs the site maintenance task **Delete Aged Discovery Data**.<!-- SCCMDocs issue #1418 -->

- **Obsolete**: The site has discovered a new device record with the same hardware ID, so it marks the old record as obsolete. Reports don't count obsolete records of the same device multiple times. You can still target policies to obsolete devices. If the site doesn't get a heartbeat for an obsolete record after 90 days of inactivity, it removes the obsolete device when it runs the site maintenance task **Delete Obsolete Client Discovery Data**.

> [!TIP]
> The [Power BI sample reports](../../servers/manage/powerbi-sample-reports.md) for Configuration Manager includes a report called **Client Status**. This report can also help with monitoring clients. <!--5679791, 10123832, 10131458, 10488910-->

## Monitor individual clients

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select either the **Devices** node or choose a collection under **Device Collections**.

    The icons at the beginning of each row indicate the online status of the device:

    | Icon | Description |
    | ---- | ----------- |
    |![Online status icon for clients.](../../../core/clients/manage/media/online-status-icon.png)|Device is online.|
    |![Offline status icon for clients.](../../../core/clients/manage/media/offline-status-icon.png)|Device is offline.|
    |![Unknown status icon for clients.](../../../core/clients/manage/media/unknown-status-icon.png)|Online status is unknown.|
    |![Client not installed icon.](../../../core/clients/manage/media/client-not-installed.png)|Client isn't installed on the device.|

2. For more detailed online status, add the client online status information to the device view. Right-click the column header and select the online status fields you want to add:

    - **Device Online Status**: Indicates whether the client is currently online or offline. (This status is the same information given by the icons.)

    - **Last Online Time**: Indicates when the client online status changed to online.

    - **Last Offline Time** indicates when the status changed to offline.

3. Select an individual client in the list pane to see more status in the detail pane. This information includes client activity and client check status.

## Monitor the status of all clients

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Client Status** node. Review the overall statistics for client activity and client checks across the site. Change the scope of the information by choosing a different collection.

2. To drill down into detail about the reported statistics, choose the name of the reported information. For example, **Active clients that have passed client check or no results**. Then review the information about the individual clients.

3. Select **Client Activity** to see charts showing the client activity in your Configuration Manager site.

4. Select **Client Check** to see charts showing the status of client checks in your Configuration Manager site.

    Configure alerts to notify you when client check results or client activity drops below a specified percentage. The site can also alert you when remediation fails on a specified percentage of clients. For more information, see [How to configure client status](../deploy/configure-client-status.md).

For more information on the client's regular checks to keep healthy, see [Client health checks](client-health-checks.md).

## Next steps

<a name="bkmk_health"></a> <!-- keep old section anchor to help redirect -->

Use the **client health dashboard** to view your client health, scenario health, and common errors. Filter the view by several attributes to see any potential issues by OS and client versions. For more information, see [Client health dashboard](client-health-dashboard.md).

For more information about the log files used by client deployment and management operations, see [Log files](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
