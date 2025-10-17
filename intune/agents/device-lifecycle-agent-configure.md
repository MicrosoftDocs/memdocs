---
title: Configure the device lifecycle agent
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Configure the device lifecycle agent

This article describes how to configure the device lifecycle agent in Microsoft Intune.

## Prerequisites

Before you get started, ensure you meet the requirementts listed in the overview article: [Device lifecycle agent overview](device-lifecycle-agent.md). The following additional prerequisite are required to configure the agent.

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - Intune Administrator
> - Security Reader
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot owner](/copilot/security/authentication#security-copilot-roles) 
>
> To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to set up, run, or view results from the agent.

:::column-end:::
:::row-end:::
 
## Enable the agent

To enable the device lifecycle agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Set up Agent** to open the set-up pane.
1. Review the details to ensure requirements are in place, and then select **Start agent**.

The agent runs until it finishes and then displays its results in the device lifecycle agent pane.

:::image type="content" source="images/device-lifecycle-agent-overview.png" alt-text="Screenshot of the overview pane of the device lifecycle agent." border="false":::

## Manage the agent

Once the agent is configured, you can manage it from the device lifecycle agent pane.

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
  1. By default, the agent page opens to the **Overview** tab. On this tab, admins can view the suggestions of devices to offboard, drill in for more details and remediation steps.
  1. The second available tab is **Suggestions**, which provides the full list of suggestions of devices to offboard, including the completed suggestions.  
  1. The other available tab is **Settings**, which provides limited details about the agent's configuration.

To learn how to use the agent after it's been configured, see [Use the device lifecycle agent](device-lifecycle-agent-use.md).

## Agent action: refresh

<!--##renew-->

[!INCLUDE [renew](includes/renew.md)]

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431