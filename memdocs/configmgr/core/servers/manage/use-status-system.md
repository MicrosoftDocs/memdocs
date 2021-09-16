---
title: The status system
titleSuffix: Configuration Manager
description: Use the status system to understand the state of your Configuration Manager environment.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the status system in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the built-in status message system to understand the state of your Configuration Manager environment.

All major site components generate status messages that provide feedback on site and hierarchy operations. This information can keep you informed about the health of different site processes. You can tune the alert system to ignore noise for known problems, and increase early visibility for other issues that might need your attention.

You generally don't need to configure the Configuration Manager status system. By default, it uses suitable settings for most environments. You can configure the following components:

- **Status summarizers**: Control the frequency of status messages that indicate a change for the following four summarizers:

  - Application deployment summarizer

  - Application statistics summarizer

  - Component status summarizer

  - Site system status summarizer

- **Status filter rules**: Create new status filter rules, modify the priority of rules, disable or enable rules, and delete unused rules at each site.

    > [!NOTE]
    > Status filter rules don't support environment variables to run external commands.

- **Status reporting**: Configure both server and client component reporting, and specify where they're sent.

    > [!WARNING]
    > Because the default reporting settings are appropriate for most environments, change them with caution. When you increase the level of status reporting by choosing to report all status details, you can increase the amount of status messages for the site to process. This change increases the processing load on the Configuration Manager site. If you decrease the level of status reporting, you might limit the usefulness of the status summarizers.

Because the status system maintains separate configurations for each site, edit each site individually.

## Configure status summarizers

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select a site. Then on the **Home** tab of the ribbon, in the **Settings** group, select **Status Summarizers**.

1. In the **Status Summarizers** window, select the status summarizer that you want to configure, and select **Edit**.

### Application deployment or application statistics summarizers

On the **General** tab of the summarizer properties page, configure the summarization intervals.

For the application deployment summarizer, these time periods specify how frequently the site updates the deployment status for applications, task sequences, and packages. It's calculated based on the deployment start time. The following values show the defaults:

- Modified in the last 30 days: 60 minutes
- Modified in the last 31 to 90 days: 24 hours
- Modified over 90 days ago: 7 days

For the application statistics summarizer, these time periods specify how often the site updates application statistics. They're based on the date you last modified the application. The following values show the defaults:

- Modified in the last 30 days: 240 minutes
- Modified in the last 31 to 90 days: 24 hours
- Modified over 90 days ago: 7 days

### Component status summarizer

1. On the **General** tab of the summarizer properties page, configure the replication and threshold period values:

    - **Enable status summarization**
    - **Replicate to parent site** and select the **Replication priority** (by default, **Normal**)
    - **Threshold period** (by default, **Since 00:00:00**). In other words, by default component status is reset at midnight.

1. On the **Thresholds** tab, select the **Message type**: Informational, Warning, or Error.

1. Select a component and then select the properties icon. You can also double-click the component, or right-click and select **Property**.

1. Specify the threshold for the number of status messages on the component before the site changes the status.

The following table shows the default values:

| Message type | Warning threshold | Critical threshold |
|---------|---------|---------|
| Informational | 2000 | 5000 |
| Warning | 10 | 50 |
| Error | 1 | 5 |

For example, if a component generates 2000 informational status messages in the threshold period (by default, since midnight), the site sets that component's state to warning.

### Site system status summarizer

1. On the **General** tab of the summarizer properties page, configure the replication and schedule values:

    - **Enable status summarization**
    - **Replicate to parent site** and select the **Replication priority** (by default, **Medium**)
    - **Status summarization schedule** (by default, every hour on the hour)

1. On the **Thresholds** tab, specify values for the **Default thresholds** for free space on any site system. The following values are the defaults:

    - **Warning (KB)**: `10485760` (10 GB)
    - **Critical (KB)**: `5242880` (5 GB)

    For example, if a site system reports less than 10 GB of free space on a drive, that site system's status changes to warning.

1. The site can also monitor specific thresholds for specific **Storage objects**. By default, it includes thresholds for the SQL Server database and transaction log for the site database. The default values for these default objects are the same as the default thresholds.

    To modify these thresholds, select the object in the list, and then select the properties icon. (You can also double-click the object, or right-click to access these actions.)

1. To create a new storage object to monitor, select the gold asterisk "new" icon. Select a storage object from the list, and specify the free space thresholds.

1. To delete a storage object, select the object, and then select the delete icon.

## Manage status filter rules

With status filter rules, the site can take action when specific status message criteria occurs. There are several default status filter rules, and you can create custom rules.

> [!TIP]
> Starting in version 2107, you can enable the site to send notifications to an external system or application.<!--9504414--> This capability simplifies the process by using a web service-based method. You configure subscriptions to send these notifications. These notifications are in response to specific, defined events as they occur. For example, status message filter rules. For more information, see [External notifications](external-notifications.md).

### Modify a status filter rule

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select a site, and then on the **Home** tab of the ribbon, in the **Settings** group, select **Status Filter Rules**.

1. In the **Status Filter Rules** window, select the rule that you want to modify.

    - To change the processing order of the status filter rule, select **Increase Priority** or **Decrease Priority**.

    - To change the status of the rule, select **Disable** or **Enable**.

    - To delete the status filter rule from the site, select **Delete**

    - To change the criteria for the status message rule, select **Edit**.

### Create a status filter rule

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select a site, and then on the **Home** tab of the ribbon, in the **Settings** group, select **Status Filter Rules**.

1. Select **Create**.

1. On the **General** page of the **Create Status Filter Rule Wizard**, specify a **Name** for the new status filter rule. Select message-matching criteria for the rule, and specify values to match. The following criteria are available:

    - Source: Client, SMS Provider, Site Server
    - Site code
    - System
    - Component
    - Message type: Milestone, Detail, Audit
    - Severity: Informational, Warning, Error
    - Message ID
    - Property
    - Property value

1. On the **Actions** page, specify the actions when a status message matches the specified criteria. The following actions are available:

    - Write to the Configuration Manager database
        - Allow the user to delete messages after how many days
    - Report to the event log
    - Replicate to the parent site
        - Replication priority
    - Run a program
        - Specify a command line to run on the site server
    - Do not forward to status summarizers
    - Do not process lower-priority status filter rules

1. Complete the wizard.

> [!NOTE]
> Configuration Manager only requires that a new status filter rule has a name. If you create a rule, but you don't specify any criteria to process status messages, the status filter rule has no effect. This behavior allows you to create and organize rules before you configure the criteria for each rule.

## Configure status reporting  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select a site, and then on the **Home** tab of the ribbon, in the **Settings** group, select **Configure Site Components**, and then select **Status Reporting**.

1. In the **Status Reporting Component Properties** window, specify the server and client component status messages that you want to report or log:

    - **Report**: Send status messages to the Configuration Manager status message system. By default, this option is enabled for **All Milestones** for both server and client components. The option to **Report details on failure** is also enabled by default.

    - **Log**: Write the type and severity of status messages to the Windows event log. By default, this option isn't enabled for either server or client components.

## Monitor the status system

System status in Configuration Manager provides an overview of the general operations of sites and site server operations of your hierarchy. It can reveal operational problems for site system servers or components. You can use the system status to review specific details for different Configuration Manager operations. You monitor system status from the **System Status** node of the **Monitoring** workspace in the Configuration Manager console.  

Most Configuration Manager site system roles and components generate status messages. Status message details are logged in each component's operational log, but are also submitted to the site database. The site then summarizes and presents them in a general health rollup for each component or site system. These status message rollups provide information details for regular operations, and details of warnings and errors. You can configure the thresholds at which the site triggers warnings or errors. Tune the system in your environment to make sure rollup information ignores known issues that aren't relevant to you. Also configure it to call attention to actual problems that you need to investigate.

System status is replicated to other sites in a hierarchy as site data, not global data. This behavior means you can only see the status for the site to which your Configuration Manager console connects, and any child sites below that site. When you view system status, use the Configuration Manager console with the top-level site of your hierarchy. For more information on site data versus global data, see [Database replication: Types of data](../../plan-design/hierarchy/database-replication.md#types-of-data).

There are different system status views in the Configuration Manager console:

- **Site Status**: View a rollup of the status of each site system to review the health of each server. The site determines site system health by thresholds that you configure for each site in the [Site System Status Summarizer](#site-system-status-summarizer). In this node:

  - View status messages for each site system
  - Set thresholds for status messages
  - Manage the operation of the components on site systems by using the **Configuration Manager Service Manager**

- **Component Status**: View a rollup of the status of each Configuration Manager component to review its operational health. The site determines component health by thresholds that you configure for each site in the [Component Status Summarizer](#component-status-summarizer). In this node:

  - View status messages for each component
  - Set thresholds for status messages
  - Manage the operation of components by using the **Configuration Manager Service Manager**

- **Conflicting Records**: View status messages about clients that might have conflicting records. Configuration Manager uses the hardware ID to attempt to identify clients that might be duplicates and alert you to the conflicting records. For example, if you have to reinstall a computer, the hardware ID would be the same, but the GUID that Configuration Manager uses might change.

- **Status Message Queries**: Query status messages for specific events and related details. Use status message queries to find the status messages related to specific events. You can identify when a specific component, operation, or Configuration Manager object was modified, and the account that was used to make the modification. For example, run the built-in **Collections Created, Modified, or Deleted** query to identify when a specific collection was created, and the user account used to create it.

## View status messages

1. To view status messages in the Configuration Manager console, select a specific site system server or component.

1. In the ribbon, select **Show Messages**, then choose the type of messages to show: All, Error, Warning, Information.

1. Select the viewing period. Either on or after a specific date and time, or from a specific time period. By default, the viewing period is **1 day ago**.

    :::image type="content" source="media/status-messages-set-viewing-period.png" alt-text="Screenshot of Status Messages: Set Viewing Period window":::

1. The Status Message Viewer has many controls to customize the view. For example, to filter the results based on the status messages details, go to the **View** menu, and select **Filter**.

Starting in version 2010, there's an easier way to view status messages for the following objects:<!--8232705-->

- Devices
- Users
- Content
- Deployments
  - Monitoring workspace
    - Phased deployments (select **Show Deployments** from the Phased Deployments node)
  - Deployments tab in the details pane for:
    - Packages
    - Task sequences

Select one of these objects in the Configuration Manager console, and then select **Show Status Messages** from the ribbon.

## Next steps

[Configure alerts](configure-alerts.md)

[Configuration Manager Service Manager](../deploy/configure/site-components.md#configuration-manager-service-manager)
