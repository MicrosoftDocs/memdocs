---
title: Centrally manage Admin Tasks
description: Centrally manage admin tasks in Microsoft Intune. Use the unified Admin tasks view to organize and act on administrative tasks from Device Offboarding, Endpoint Privilege Management, and more.
author: brenduns
ms.author: brenduns
ms.date: 01/26/2026
ms.topic: article
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
---

# Centrally manage common admin tasks in Microsoft Intune

In the Microsoft Intune admin center, the **admin tasks** node provides a centralized view to discover, organize, and act on administrative tasks and user elevation requests. This unified experience helps you focus on what matters most without navigating across multiple nodes.

Admin tasks supports tasks from the following Intune capabilities:

- [Device Offboarding tasks](/intune/agents/device-offboarding-agent) - Found in the admin center at *Tenant administration > Device Offboarding Agent*.
- [Endpoint Privilege Management file elevation requests](/intune/intune-service/protect/epm-support-approved#manage-pending-elevation-requests) – Found in the admin center at *Endpoint security > Endpoint Privilege Management*.
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities#work-with-security-tasks) - Found in the admin center at *Endpoint security > Security Tasks*.
- [Multi Admin Approval requests](/intune/intune-service/fundamentals/multi-admin-approval#approve-requests) - Found in the admin center at *Tenant administration > Multi Admin Approval*.

## Role-based access control for Admin tasks

Access to tasks in the admin tasks node is based on your Intune role-based access control (RBAC) permissions.The following permission is required to access the Admin tasks pane in the Intune admin center:

- **Organization** > **Read**

When viewing Admin tasks, you can only see and manage tasks permitted by your assigned roles within the task’s original source node. For RBAC requirements and related prerequisites specific to each capability, see:

- [Device Offboarding tasks](/intune/agents/device-offboarding-agent#prerequisites)
- [Endpoint Privilege Management file elevation requests](/intune/intune-service/protect/epm-support-approved#rbac-permissions-for-elevation-requests)
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities#prerequisites)
- [Multi Admin Approval requests](/intune/intune-service/fundamentals/multi-admin-approval#prerequisites-for-access-policies-and-approvers)

## Manage admin tasks in the centralized view

**To review and manage tasks:**

1. Open the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Admin tasks**.

2. Intune displays a consolidated list of tasks that are available to you, based on your RBAC permissions. The display includes the first 50 available tasks that match the filter criteria. To view additional tasks, use the filter control to adjust the displayed tasks.

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

Tasks are removed from this view when they are removed from their source node.

## Related content

- [Use Endpoint Privilege Management with Microsoft Intune](/intune/intune-service/protect/epm-overview)
- [Microsoft Defender security tasks](/intune/intune-service/protect/atp-manage-vulnerabilities)
- [Use Multi Admin Approval in Intune](/intune/intune-service/fundamentals/multi-admin-approval)
- [Device Offboarding Agent](../../agents/device-offboarding-agent.md)