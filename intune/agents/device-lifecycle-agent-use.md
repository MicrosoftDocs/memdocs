---
title: "Device lifecycle agent: use"
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Use the device lifecycle agent

This article describes how to use the Device Lifecycle Agent in Microsoft Intune to identify and manage devices that were removed from Intune but might still exist in Microsoft Entra.

Different prompts can be used to get different results from the agent. The article includes sample prompts and responses to illustrate how the agent can assist in offboarding devices.

## Prerequisites

Before you get started, ensure you meet the requirementts listed in the overview article: [Device lifecycle agent overview](device-lifecycle-agent.md). The following additional prerequisite are required to use the agent.

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - Read Only Operator
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - Intune Administrator
> - Security Reader
>
> For results:
> - Copilot Contributor 
>
> To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to set up, run, or view results from the agent.

:::column-end:::
:::row-end:::

## Manage devices and the agent 

To review and manage the device lifecycle agent suggestions:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
  1. By default, the agent page opens to the **Overview** tab. On this tab, admins can view the suggestions of devices to offboard, drill in for more details and remediation steps.
  1. The second available tab is **Suggestions**, which provides the full list of suggestions of devices to offboard, including the completed suggestions.  
  1. The other available tab is **Settings**, which provides limited details about the agent's configuration. 

## Agent action: run

To manually run the Device Lifecycle Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Run**.  

When an agent run starts, the agent runs until it completes its evaluation. It can't be stopped or paused. 

> [!NOTE]
> Each time the agent runs, it runs under the identity and permissions of the Intune administrator that its been configured to use. 

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

## Device Lifecycle Agent logs 

All agent management, create, delete, run, and any permission failures are available in Security Copilot logs. Logging of which devices were offboarded or when a recommended actions were complete aren't available. Instead, use the options to mark a suggestion as complete.  

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431