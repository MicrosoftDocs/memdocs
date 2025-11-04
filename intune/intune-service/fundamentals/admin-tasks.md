---
title: Manage Admin Tasks
description: Use the centralized Admin tasks view in Microsoft Intune to manage tasks across capabilities.
author: brenduns
ms.author: brenduns
ms.date: 11/18/2025
ms.topic: article
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
---

# Manage admin tasks in Microsoft Intune

In the Microsoft Intune admin center, the **admin tasks** node provides a centralized view where you can discover, organize, and act on recommendations, administrative tasks, and user requests. This consolidated experience helps you focus on what matters most without navigating across multiple nodes.

Admin tasks include items from the following Intune capabilities:

- [Endpoint Privilege Management file elevation requests](/intune/intune-service/protect/epm-support-approved#manage-pending-elevation-requests) – Found in the admin center at *Endpoint security > Endpoint Privilege Management*.
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities) - Found in the admin center at *Endpoint security > Security Tasks*.
- [Multi Admin Approval requests](/intune/intune-service/fundamentals/multi-admin-approval) - Found in the admin center at *Tenant administration > Multi Admin Approval*.

## Role-based access control for admin tasks

Access to tasks in the admin tasks node is based on your role-based access control (RBAC) permissions. You can only view and manage tasks that your assigned roles allow in the original source nodes.

For RBAC and related prerequisite details specific to each capability, see:
- [Endpoint Privilege Management file elevation requests](/intune/intune-service/protect/epm-support-approved#rbac-permissions-for-elevation-requests)
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities#prerequisites)
- [Multi Admin Approval requests](/intune/intune-service/fundamentals/multi-admin-approval#prerequisites-for-access-policies-and-approvers) 

## Manage tasks in the admin tasks node

**To review and manage tasks:**

1. Open the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Admin tasks**.
2. Intune displays a consolidated list of tasks available to you, based on your RBAC permissions. To manage the list view you can search, use filters and select a column header to sort the view.
3. Select a task from the **Task** column to open its management pane. The pane that opens is the *same interface and workflow* you'd use if managing the task from its original location in the admin center. This ensures a consistent experience whether you're working from the admin tasks node or directly within the source capability.

For task-specific workflows, refer to the documentation for that task type.

**Task list columns:**

The list of available tasks includes the following columns of information:

- **Task** – The name of the task. Select it to open a flyout pane with task details and management options.
- **Source** – Identifies the task type, like a Defender security task, Endpoint Privilege Management elevation request, or Multi Admin Approval request.
- **Status** – Indicates the current state of the task. Values include: 
  - **Active** – The task hasn't been managed yet.
  - **Pending** – The task has been accepted but not resolved. For example, a Defender task might require remediation before being marked as complete
  - **Completed** – The task is complete and no further action is needed.
  - **Rejected** – The task was declined.
  - **Expired** – The task expired. Expired tasks are automatically removed after 30 days.  
  - **Needs approval** – Indicates a change awaiting approval.
- **Due in** – Shows how much time remains before the task expires (if applicable).
- **Last updated** – The date the task was last modified.
- **Created** – The date the task was created.

## Related articles

- [Use Endpoint Privilege Management with Microsoft Intune](/intune/intune-service/protect/epm-overview)
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities)
- [Use Multi Admin Approval in Intune](/intune/intune-service/fundamentals/multi-admin-approval)