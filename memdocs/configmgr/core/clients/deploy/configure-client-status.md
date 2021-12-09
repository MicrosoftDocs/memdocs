---
title: Configure client status
titleSuffix: Configuration Manager
description: Select client status settings in Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# How to configure client status in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you can monitor Configuration Manager clients and remediate problems, configure the site's client status settings. These settings specify the parameters that the site uses to mark clients as inactive. Also configure options to alert you if client activity falls below a specified threshold.

## Configure client status

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Client Status** node. On the **Home** tab of the ribbon, in the **Client Status** group, select **Client Status Settings**.

1. Configure the following settings:

    > [!NOTE]
    > If a client doesn't meet any of the settings, the site marks it as inactive.

    - **Client policy requests during the following days:** Specify the number of days since the client requested policy from the site. The default value is `7` days.

      Compare this value to the **Client policy polling interval** setting in the **Client Policy** group of client settings. Its default is 60 minutes. In other words, a client should poll the site for policy every hour. If it doesn't request policy after one week, the site marks it as inactive.

    - **Heartbeat discovery during the following days:** Specify the number of days since the client sent a heartbeat discovery record to the site. The default value is `7` days.

      Compare this value to the schedule for the [Heartbeat discovery method](../../servers/deploy/configure/about-discovery-methods.md). By default, the site runs heartbeat discovery once a week.

    - **Hardware inventory during the following days:** Specify the number of days since the client sent a hardware inventory record to the site. The default value is `7` days.

      Compare this value to the **Hardware inventory schedule** setting in the **Hardware Inventory** group of client settings. Its default is seven days.

    - **Software inventory during the following days:** Specify the number of days since the client sent a software inventory record to the site. The default value is `7` days.

      Compare this value to the **Schedule software inventory and file collection** setting in the **Software Inventory** group of client settings. Its default is seven days.

    - **Status messages during the following days:** Specify the number of days since the client sent any status messages to the site. The default value is `7` days. The client can send status messages for different kinds of activities, such as running a task sequence. The site deletes old status messages as part of the maintenance task, **Delete Aged Status Messages**.

1. Specify the following value to determine how long the site keeps client status history data:

    - **Retain client status history for the following number of days:** By default, the site keeps client status information for `31` days. This setting doesn't have any impact on client or site behavior. It's similar to a maintenance task for client status history.

## Configure the schedule

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Client Status** node. On the **Home** tab of the ribbon, in the **Client Status** group, select **Schedule Client Status Update**.

1. Configure the interval at which you want client status to update.

    > [!NOTE]
    > When you change the schedule for client status updates, it doesn't take effect until the next scheduled client status update on the previous schedule.

## Configure alerts

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.

1. Select the collection for which you want to configure alerts. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

    > [!NOTE]
    > You can't configure alerts for user collections.

1. Switch to the **Alerts** tab, and select **Add**.

   > [!TIP]
   > You can only view the **Alerts** tab if your security role has permissions for alerts.

    Choose the alerts that you want the site to generate for client status thresholds, and select **OK**.

1. In the **Conditions** list of the **Alerts** tab, select each client status alert, and then specify the following information:

    - **Alert Name**: Accept the default name or enter a new name for the alert.

    - **Alert Severity**: Choose the alert level that the Configuration Manager console displays.

    - **Raise alert**: Specify the threshold percentage for the alert.

## Automatic remediation exclusion

1. On the client computer where you want to disable automatic remediation, open the registry editor.

    > [!WARNING]
    > If you use the registry editor incorrectly, you can cause serious problems that could require you to reinstall Windows. Microsoft can't guarantee that you can solve problems that result from using the registry editor incorrectly. Use it at your own risk.

1. Navigate to the registry key **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval**.

1. Change the value for the **NotifyOnly** entry:

    - `TRUE`: The client won't automatically remediate any problems that it finds. The site still notifies you in the **Monitoring** workspace about any problems with this client.

    - `FALSE`: This setting is the default. The client automatically remediates problems when it finds them, and the site notifies you in the **Monitoring** workspace.

When you install clients, you can exclude them from automatic remediation with the **NotifyOnly** installation property. For more information, see [About client installation properties](about-client-installation-properties.md).

## Next steps

[Monitor clients](../manage/monitor-clients.md)
