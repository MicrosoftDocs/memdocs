---
title: Set up the device lifecycle agent
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Set up the device lifecycle agent


Set up the agent to automate and optimize device offboarding in Intune. Security Copilot agents use AI to complete routine tasks and surface insights with some level of autonomy so you can focus on high-value work. 

> [!NOTE]
> This agent is in preview and currently doesn't take action on your devices.

Your organization will be able to monitor and manage the agent. You should check its output to make sure it's correct and give feedback to help the agent learn and improve. Like all AI, an agent might be wrong sometimes.  

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> Endpoint analytics includes tasks that require different levels of permissions.
>
> For a detailed breakdown of the required permissions for each task:
>
> - Read Intune audit logs
> - Read Entra devices
> 
> If you want to take action from within the agent, such as to disable devices in Entra, you must have the Disable devices in Entra permission. You don't need this permission to set up, run, or view results from the agent.

> Agent identity:
> The agent will run using the identity of the user who first set up the agent. Agent authentication will expire after 90 days and need to be renewed. Learn more about agent authentication.

> Users
> Anyone with the required permissions, which can include a custom role or a Security Reader role.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

:::column-end:::
:::row-end:::



Identity 

Plugins
Provides the agent access needed for this agent to run. Learn more about plugins 
Microsoft Intune
Microsoft Entra

Workspace: This agent will run in the same preferred workspace you selected for Security Copilot.
Once started, the agent will immediately run in your tenant. You will not be able to cancel an agent mid-run. When the run finishes, you can choose to remove the agent.

Select **Start agent** to begin the setup process.

## Configure the agent

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > [**Device Lifecycle Agent**].

## Remove the agent

By removing this agent, all associated data generated including suggestions and activities will be deleted. Previously applied suggestions will remain unchanged. This action is permanent and cannot be undone.


Select **Remove agent**.

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

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431