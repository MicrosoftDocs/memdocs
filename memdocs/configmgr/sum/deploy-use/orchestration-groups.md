---
title: Orchestration groups
titleSuffix: Configuration Manager
description: About orchestration groups and their prerequisites and limitations.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# About orchestration groups in Configuration Manager
<!--3098816-->
*Applies to: Configuration Manager (current branch)*

Create an orchestration group to better control the deployment of software updates to devices. Many server administrators need to carefully manage updates for specific workloads, and automate behaviors in between.

:::image type="content" source="./media/9957939-orchestration-group-scripts-tab.png" alt-text="Screenshot of the Scripts tab in the Orchestration Group node." lightbox="./media/9957939-orchestration-group-scripts-tab.png":::

An orchestration group gives you the flexibility to update devices based on a percentage, a specific number, or an explicit order. You can also run a PowerShell script before and after the devices run the update deployment.

Members of an orchestration group can be any Configuration Manager client, not just servers. The orchestration group rules apply to the devices for all software update deployments to any collection that contains an orchestration group member. Other deployment behaviors still apply. For example, maintenance windows and deployment schedules.

> [!NOTE]
> Starting in Configuration Manager version 2111, Orchestration groups is no longer a pre-release feature. For more information, see [Pre-release features](../../core/servers/manage/pre-release-features.md).  
>
> The **Orchestration Groups** feature is the evolution of the [Server Groups](service-a-server-group.md) feature. An orchestration group is an object in Configuration Manager.

## Orchestration group usage example

- As the software updates administrator, you manage all updates for your organization.
- You have one large collection for all servers and one large collection for all clients. You deploy all updates to these collections.
- The SQL Server administrators want to control all the software installed on the SQL Servers. They want to patch five servers in a specific order. Their current process is to manually stop specific services before installing updates, and then restart the services afterwards.
- You create an orchestration group and add all five SQL Servers. You also add pre- and post-scripts, using the PowerShell scripts provided by the SQL Server administrators.
- During the next update cycle, you create and deploy the software updates as normal to the large collection of servers. The SQL Server administrators run the deployment, and the orchestration group automates the order and services.

## Prerequisites

### Site server and permission prerequisites

- To see all of the orchestration groups and updates for those groups, your account needs to be a **Full Administrator**.
   - Role-based administration for orchestration groups currently isn't available.
- Enable the **Orchestration Groups** feature. For more information, see [Enable optional features](../../core/servers/manage/optional-features.md).
   - When you enable **Orchestration Groups**, the site disables the **Server Groups** feature. This behavior avoids any conflicts between the two features.

### Client prerequisites

- Upgrade the target devices to the latest version of the Configuration Manager client.
- Members of an orchestration group should be assigned to the same site.
- Devices can't be in more than one orchestration group.
   - Devices already in an orchestration group won't be available to select when adding new members.

### Permissions for approving scripts
<!--9957939-->
*(Introduced in version 2111)*

Approving scripts for orchestration groups requires one of the following security roles:

- Full Administrator
- Operations Administrator

## Limitations

- You can have up to 1000 orchestration group members.
- Orchestration groups don't work in interoperability mode. For more information, see [Interoperability between different versions of Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#limitations-in-a-mixed-version-hierarchy). <!--6389000-->
- If updates are initiated by users from Software Center, orchestration will be bypassed. <!--6362887-->
- Starting in Configuration Manager version 2103, updates in the **Definition** [classification](../get-started/configure-classifications-and-products.md) don't require orchestration and will always bypass orchestration group rules. <!--7706596-->
- Scripts that have parameters aren't supported <!--9893550-->

## Server groups are automatically updated to orchestration groups

The **Orchestration Groups** feature is the evolution of the [Server Groups](service-a-server-group.md) feature. When you install Configuration Manager version 2002 or later and you have Server Groups enabled, your server groups are automatically moved to orchestration groups.

## Next steps

- [Create orchestration groups](create-orchestration-groups.md)
- [Monitor orchestration groups](monitor-orchestration-groups.md)
