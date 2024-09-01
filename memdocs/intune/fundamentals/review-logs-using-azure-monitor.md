---
# required metadata

title: Route logs to Azure Monitor using Microsoft Intune
description: Use Diagnostics Settings to send audit logs and operational logs in Microsoft Intune to Azure Storage account, Event Hubs, or Log Analytics. Choose how long you want to keep the data, and see some estimated costs for different size tenants.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/30/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 95191d64-9895-4f2e-8c5b-f0e85be086d8

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chnatar, daviales
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Send Intune log data to Azure Storage, Event Hubs, or Log Analytics

Microsoft Intune includes built-in logs that provide information about your environment:

- **Audit Logs** shows a record of activities that generate a change in Intune, including create, update (edit), delete, assign, and remote actions.
- **Operational Logs** show details on users and devices that successfully (or failed) to enroll, and details on noncompliant devices.
- **Device Compliance Organizational Logs** show an organizational report for device compliance in Intune, and details on noncompliant devices.
- **IntuneDevices** show device inventory and status information for Intune enrolled and managed devices.

These logs can also be sent to Azure Monitor services, including storage accounts, Event Hubs, and Log Analytics. Specifically, you can:

- Archive Intune logs to an Azure Storage account to keep the data, or archive for a set time.
- Stream Intune logs to an Azure Event Hubs for analytics using popular Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.
- Integrate Intune logs with your own custom log solutions by streaming them to Event Hubs.
- Send Intune logs to Log Analytics to enable rich visualizations, monitoring, and alerting on the connected data.

These features are part of the **Diagnostics Settings** in Intune.

This article shows you how to use **Diagnostics Settings** to send log data to different services, gives examples & cost estimates, and answers some common questions. Once you enable this feature, your logs are routed to the Azure Monitor service you choose.

> [!NOTE]
> These logs use schemas that can change. To provide feedback, including information in the logs, go to [Feedback for Intune](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472).<!-- 10948264 -->

## Prerequisites

To use this feature, you need:

- An Azure subscription that you can sign in to. If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).
- A Microsoft Intune environment (tenant)
- A user who has the **Intune Service Administrator** Microsoft Entra role for the Intune tenant. For information on this role, go to [Microsoft Entra built-in roles - Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).
- To configure the log collection from Azure Storage, you need the **Log Analytics Contributor** role in the Log Analytics Workspace. For more information on the different roles, and what they can do, go to [Manage access to log data and workspaces in Azure Monitor](/azure/azure-monitor/logs/manage-access).

Depending on where you want to route the audit log data, you need one of the following services:

- An [Azure storage account](/azure/storage/common/storage-account-overview) with the **ListKeys** permissions. We recommend that you use a general storage account, and not a blob storage account. For storage pricing information, go to the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage). 
- An [Azure Event Hubs namespace](/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) to integrate with third-party partner solutions.
- An [Azure Log Analytics workspace](/azure/azure-monitor/learn/quick-create-workspace) to send logs to Log Analytics.

## Send logs to Azure monitor

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Reports** > **Diagnostics settings**. The first time you open it, turn it on. Otherwise, add a setting.

    :::image type="content" source="./media/review-logs-using-azure-monitor/diagnostics-settings-turn-on.png" alt-text="Screenshot that shows how to turn on Diagnostics settings in Microsoft Intune to send logs to Azure Monitor.":::

    If your Azure subscription isn't shown, go to the top right corner, select the signed in account > **Switch directory**. You might have to enter the Azure subscription account.

3. Enter the following properties:

    - **Name**: Enter a name for the diagnostic settings. This setting includes all the properties you enter. For example, enter `Route audit logs to storage account`.
    - **Archive to a storage account**: Saves the log data to an Azure Storage account. If you want to save or archive the data, then choose this option.

        1. Select this option > **Configure**.
        2. Choose an existing storage account from the list > **OK**.

    - **Stream to an event hub**: Streams the logs to Azure Event Hubs. If you want analytics on your log data using SIEM tools, such as Splunk and QRadar, then choose this option.

        1. Select this option > **Configure**.
        2. Choose an existing Event Hubs namespace and policy from the list > **OK**.

    - **Send to Log Analytics**: Sends the data to Azure Log Analytics. If you want to use visualizations, monitoring and alerting for your logs, then choose this option.

        1. Select this option > **Configure**.
        2. Create a new workspace, and enter the workspace details. Or, choose an existing workspace from the list > **OK**.

            [Azure Log Analytics workspace](/azure/azure-monitor/learn/quick-create-workspace) provides more details on these settings.

    - **LOG** > **AuditLogs**: Choose this option to send the [Intune audit logs](monitor-audit-logs.md) to your storage account, Event Hubs, or Log Analytics. The audit logs show the history of every task that generates a change in Intune, including who did it and when. For more reference information, go to [IntuneAuditLogs](/azure/azure-monitor/reference/tables/IntuneAuditLogs).

      If you choose to use a storage account, then also enter how many days you want to keep the data (retention). To keep data forever, set **Retention (days)** to `0` (zero).

    - **LOG** > **OperationalLogs**: Operational logs show the success or failure of users and devices that enroll in Intune, and details on noncompliant devices. Choose this option to send the enrollment logs to your storage account, Event Hubs, or Log Analytics. For more reference information, go to [IntuneOperationalLogs](/azure/azure-monitor/reference/tables/IntuneOperationalLogs).

      If you choose to use a storage account, then also enter how many days you want to keep the data (retention). To keep data forever, set **Retention (days)** to `0` (zero).

    - **LOG** > **DeviceComplianceOrg**: Device compliance organizational logs show the organizational report for Device Compliance in Intune, and details of noncompliant devices. Choose this option to send the compliance logs to your storage account, Event Hubs, or Log Analytics. For more reference information, go to [IntuneDeviceComplianceOrg](/azure/azure-monitor/reference/tables/IntuneDeviceComplianceOrg).

      If you choose to use a storage account, then also enter how many days you want to keep the data (retention). To keep data forever, set **Retention (days)** to `0` (zero).

    - **LOG** > **IntuneDevices**: The Intune Device log shows device inventory and status information for Intune enrolled and managed devices. Choose this option to send the IntuneDevices logs to your storage account, Event Hubs, or Log Analytics. For more reference information, go to [IntuneDevices](/azure/azure-monitor/reference/tables/IntuneDevices).

      If you choose to use a storage account, then also enter how many days you want to keep the data (retention). To keep data forever, set **Retention (days)** to `0` (zero).

    When finished, your settings look similar to the following settings:

    :::image type="content" source="./media/review-logs-using-azure-monitor/diagnostics-settings-example.png" alt-text="Screenshot that shows how to send Microsoft Intune audit logs to an Azure Storage account.":::

4. **Save** your changes. Your setting is shown in the list. Once the settings are created, you can change the settings by selecting **Edit setting** > **Save**.

## Use audit logs throughout Intune

You can also export the audit logs used in other parts of Intune, including enrollment, compliance, configuration, devices, client apps, and more.

For more information, go to [Use audit logs to track and monitor events](monitor-audit-logs.md). You can choose where to send the audit logs, as described in [send logs to Azure monitor](#send-logs-to-azure-monitor) (in this article).

## Audit log properties

In the audit log, you can find the following properties and their specific values:

| Property | Property description | Values |
|---|---|---|
| ActivityType  | The action that the admin takes. | Create, Delete, Patch, Action, SetReference, RemoveReference, Get, Search |
| ActorType  | Person taking the action. | Unknown = 0, ItPro, IW, System, Partner, Application, GuestUser |
| Category  | The pane where the action took place. | Other = 0, Enrollment = 1, Compliance = 2, DeviceConfiguration = 3, Device = 4, Application = 5, EBookManagement = 6, ConditionalAccess= 7, OnPremiseAccess= 8, Role = 9, SoftwareUpdates =10, DeviceSetupConfiguration = 11, DeviceIntent = 12, DeviceIntentSetting = 13, DeviceSecurity = 14, GroupPolicyAnalytics = 15, AssignmentFilter = 16, RemoteHelp = 17, OrganizationalMessage = 18, EndpointPrivilegeMgmt = 19, DeviceInventory = 20|
| ActivityResult | Whether the action is successful or not | Success = 1 |

## Cost considerations

If you already have a Microsoft Intune license, then you need an Azure subscription to set up the storage account and Event Hubs. The Azure subscription is typically free. But, you do pay to use Azure resources, including the storage account for archival and Event Hubs for streaming. The amount of data and the costs vary depending on the tenant size.

### Storage size for activity logs

Every audit log event uses about 2 KB of data storage. For a tenant with 100,000 users, you can have about 1.5 million events per day. You might need about 3 GB of data storage per day. Since writes typically happen in five-minute batches, you can expect approximately 9,000 write operations per month.

The following tables show a cost estimate depending on the size of the tenant. It also includes a general purpose v2 storage account in West US for at least one year of data retention. To get an estimate for the data volume that you expect for your logs, use the [Azure storage pricing calculator](https://azure.microsoft.com/pricing/details/storage/blobs/).

**Audit log with 100,000 users**:

| Category | Value |
| -------- | ----- |
|Events per day| 1.5 million|
|Estimated volume of data per month| 90 GB|
|Estimated cost per month (USD)| $1.93|
|Estimated cost per year (USD)| $23.12|

**Audit log with 1,000 users**:

| Category | Value |
| -------- | ----- |
|Events per day| 15,000|
|Estimated volume of data per month| 900 MB|
|Estimated cost per month (USD)| $0.02|
|Estimated cost per year (USD)| $0.24|

### Event Hubs messages for activity logs

Events are typically batched in five-minute intervals, and sent as a single message with all the events within that timeframe. A message in Event Hubs has a maximum size of 256 KB. If the total size of all the messages within the timeframe exceed that volume, then multiple messages are sent.

For example, about 18 events per second typically happen for a large tenant of more than 100,000 users. This value equates to 5,400 events every five minutes (300 seconds x 18 events). Audit logs are about 2 KB per event. This value equates to 10.8 MB of data. So, 43 messages are sent to Event Hubs in that five-minute interval.

The following table contains estimated costs per month for a basic Event Hubs in West US, depending on the volume of event data. To get an estimate of the data volume that you expect for your logs, use the [Event Hubs pricing calculator](https://azure.microsoft.com/pricing/details/event-hubs/).

**Audit log with 100,000 users**:

| Category | Value |
| -------- | ----- |
|Events per second| 18|
|Events per five-minute interval| 5,400|
|Volume per interval| 10.8 MB|
|Messages per interval| 43|
|Messages per month| 371,520|
|Estimated cost per month (USD)| $10.83|

**Audit log with 1,000 users**:

| Category | Value |
| -------- | ----- |
|Events per second|0.1 |
|Events per five-minute interval| 52|
|Volume per interval|104 KB |
|Messages per interval|1 |
|Messages per month|8,640 |
|Estimated cost per month (USD)|$10.80 |

### Log Analytics cost considerations

To review costs related to managing the Log Analytics workspace, go to [Manage cost by controlling data volume and retention in Log Analytics](/azure/log-analytics/log-analytics-manage-cost-storage).

## Frequently asked questions (FAQ)

Get answers to frequently asked questions, including latency times, how costs are affected, supported SIEM tools, and more.

### Which logs are included?

The Intune **Audit logs** and **Operational logs** are available for routing using this feature.

### After an action, when do the logs show up in the Azure Monitor services?

After the action:

- The Intune **Audit Logs** and **Operational Logs** are sent immediately from Intune to Azure Monitor services.
- The Intune **Device Compliance Organizational Logs** and **IntuneDevices** report data is sent from Intune to Azure Monitor services once every 24 hours. So, it can take up to 24 hours to get the logs in the Azure Monitor services.

Once the data is sent from Intune, then it typically shows in the Azure Monitor service within 30 minutes.

### What happens if an administrator changes the retention period of a diagnostic setting?

The new retention policy is applied to logs collected after the change. Logs collected before the policy change are unaffected.

### How much does it cost to store my data?

The storage costs depend on the size of your logs and the retention period you choose. For a list of the estimated costs for tenants, which depend on the log volume generated, go to [Storage size for activity logs](#storage-size-for-activity-logs) (in this article).

### How much does it cost to stream my data to Azure Event Hubs?

The streaming costs depend on the number of messages you receive per minute. For details on how costs are calculated and cost estimates based on the number of messages, go to [Event Hubs messages for activity logs](#event-hubs-messages-for-activity-logs) (in this article).

### How do I integrate Intune audit logs with my SIEM system?

Use Azure Monitor with Event Hubs to stream logs to your SIEM system:

1. [Stream the logs to Event Hubs](/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub).
2. [Set up your SIEM tool](/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub#access-data-from-your-event-hub) with the configured Event Hubs.

### What SIEM tools are currently supported?

Currently, [Splunk](/azure/active-directory/reports-monitoring/tutorial-integrate-activity-logs-with-splunk), QRadar, and [Sumo Logic](https://help.sumologic.com/docs/integrations/microsoft-azure/active-directory-azure/) (opens a new website) support Azure Monitor. For more information about how the connectors work, go to [Stream Azure monitoring data to Event Hubs for consumption by an external tool](/azure/azure-monitor/platform/stream-monitoring-data-event-hubs).

### Can I access the data from Azure Event Hubs without using an external SIEM tool?

Yes. To access the logs from your custom application, you can use the [Event Hubs API](/azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph).

### What data is stored?

Intune doesn't store any data sent through the pipeline. Intune routes data to the Azure Monitor pipeline, at the authority of the tenant. For more information, go to [Azure Monitor overview](/azure/azure-monitor/overview).

## Related content

- [Archive activity logs to a storage account](/azure/active-directory/reports-monitoring/quickstart-azure-monitor-route-logs-to-storage-account)
- [Route activity logs to Azure Event Hubs](/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub)
- [Integrate activity logs with Log Analytics](/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)
