---
# required metadata

title: Audit changes and events in Microsoft Intune
description: Learn how to review audit logs that record Microsoft Intune activities.
keywords: 
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 08/14/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Use audit logs to track and monitor events in Microsoft Intune

In Microsoft Intune, there are audit logs that include a record of activities that generate a change. For example, the create, update (edit), delete, assign, and remote actions all create audit events.

Administrators can review the audit logs to track and monitor events for most Intune workloads. Auditing is enabled for all customers. It can't be disabled.

## Who can access the data?

Users with the following permissions can review audit logs:

- [Intune Administrator Microsoft Entra role](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
- Administrators assigned to an Intune role with **Audit data** - **Read** permissions. For a list of built-in Intune roles that have this permission, go to [Built-in role permissions for Microsoft Intune](role-based-access-control-reference.md).

## View the audit logs

You can review audit logs in the monitoring group for each Intune workload, like compliance or Conditional Access.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Audit logs**.
3. A list of the logs is shown. Select a log from the list to see the activity details.
4. If there are many logs, you can:

    1. Select **Date** and enter a start and end date. This date range can show logs for the previous month, week, or day.

        :::image type="content" source="./media/monitor-audit-logs/audit-logs-date-range.png" alt-text="Filter audit logs by date in Microsoft Intune and Intune admin center.":::

    1. Select **Add filters** > **Category**. Select a category from the list, like **Compliance**, **Device**, or **Role**. Then, select **Apply**.
    1. Select **Add filters** > **Activity**. The available options depend on the **Category** you select. Then, select **Apply**.

        For example, if you select the **Compliance** category, your **Activity** filter options look similar to the following image:

        :::image type="content" source="./media/monitor-audit-logs/audit-logs-compliance-category-activity-options.png" alt-text="Filter audit logs by compliance category and select an activity in Microsoft Intune and Intune admin center.":::

For related information about audit logs, go to:

- [Data storage and processing in Intune](../protect/privacy-data-store-process.md)
- [Use audit logs throughout Intune](../fundamentals/review-logs-using-azure-monitor.md#use-audit-logs-throughout-intune)
- [Audit, export, or delete personal data in Intune](../protect/privacy-data-audit-export-delete.md)

## Route logs to Azure Monitor

Audit logs and operational logs can also be routed to [Azure Monitor](/azure/azure-monitor/overview). In the Intune admin center, select **Tenant administration** > **Audit logs** > **Export**:

:::image type="content" source="./media/monitor-audit-logs/audit-logs-export-data-settings.png" alt-text="Export log data to Azure monitor by selecting Export data settings in Microsoft Intune and Intune admin center.":::

When you export, a `.csv` file is created and saved locally, possibly in `C:\Users\UserName\AppData\Local\Temp\MicrosoftEdgeDownloads\GUID`.

When looking at the `.csv` file:

- **Initiated by (actor)** includes information on who ran the task, and where it was run.

  For example, if you run the activity in Intune in the Azure portal, then **Application** always lists **Microsoft Intune portal extension**, and the **Application ID** always uses the same GUID.

- The **Target(s)** section lists multiple targets and the properties that were changed.  

For more information about this feature, including the prerequisites, go to [send log data to storage, event hubs, or log analytics](review-logs-using-azure-monitor.md).

## Use Graph API to retrieve audit events

You can also use Graph API to get one year of audit events. For more information, go to [List auditEvents](/graph/api/intune-auditing-auditevent-list).

## Related articles

- [Send log data to storage, event hubs, or log analytics](review-logs-using-azure-monitor.md)
- [Review client app protection logs](../apps/app-protection-policy-settings-log.md)
