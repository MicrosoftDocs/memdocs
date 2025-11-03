---
title: Use the Device Offboarding Agent
description: Learn how to use the Device Offboarding Agent in Microsoft Intune to identify and offboard devices that are no longer in use.
ms.date: 10/15/2025
ms.topic: how-to
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Use the Device Offboarding Agent

This article describes how to use the Device Offboarding Agent in Microsoft Intune to identify and manage devices that were removed from Intune but might still exist in Microsoft Entra.

Different prompts can be used to get different results from the agent. The article includes sample prompts and responses to illustrate how the agent can assist in offboarding devices.

## Prerequisites

Before you get started, ensure you meet the requirementts listed in the overview article: [Device Offboarding Agent overview](device-offboarding-agent.md).

<!--The following additional prerequisite are required to use the agent.

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) or [custom role](/intune/intune-service/fundamentals/role-based-access-control#custom-roles) with equivalent permissions.
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> 
>   To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to run or view results from the agent.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot contributor](/copilot/security/authentication#security-copilot-roles) 

:::column-end:::
:::row-end:::
-->

## Run the agent

Running the agent will reset your current suggestions, status, and assignments for this view. You can use the Tasks page to track progress of suggestions you've added.

To manually run the Device Offboarding Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select **Run**.  

When an agent run starts, the agent runs until it completes its evaluation. It can't be stopped or paused. 

> [!NOTE]
> Each time the agent runs, it runs under the identity and permissions of the Intune administrator that its been configured to use. 

## Refresh

Executing the **Refresh** action updates the agent's current view with the latest data from its most recent run. This action doesn't trigger a new evaluation; it simply refreshes the displayed information to reflect any changes or updates since the last run.

## Review suggestions and take action

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select the **Suggestions** tab to view the list of recommndations.
1. Select a suggestion to view more details, including the rationale behind the recommendation and steps for offboarding the device.
  1. You can change the status of a suggestion by selecting **Manage suggestion** and selecting whether the offboarding action is in progress or completed.
  1. You can select the option **Add to tasks list** to assign the offboarding action to an individual or team for tracking and management.

:::image type="content" source="images/device-offboarding-agent/suggestion.png" alt-text="Screenshot of a suggestion of the Device Offboarding Agent showind the details and options." border="false" lightbox="images/device-offboarding-agent/suggestion.png":::

<!--
## Use the agent

```agent-prompt
Find all devices that were removed from Intune but might still exist in Microsoft Entra. Provide steps to properly remove them from Entra.
```

```agent-response
Summary
There are 23 devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Users accessing corporate apps without MDM enrollment.
- Cannot enforce compliance policies or data protection.
- Personal devices may have corporate data without proper controls.
- Conditional access limited to user-based policies only.
```
--->



## Device Offboarding Agent logs 

All agent management, create, delete, run, and any permission failures are available in Security Copilot logs. Logging of which devices were offboarded or when a recommended actions were complete aren't available. Instead, use the options to mark a suggestion as complete.  

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431