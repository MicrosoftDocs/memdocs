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
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles)
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - Intune Administrator
> - Security Reader
>
> For initial setup:
> - Copilot Owner required for setup
>
> To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to set up, run, or view results from the agent.

:::column-end:::
:::row-end:::
 
## Configuration steps

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Set up Agent** to open the set-up pane.
1. Review the details to ensure requirements are in place, and then select **Start agent** to close the set-up pane and start the first run of the agent.

The agent runs until it finishes and then displays its results in the Device Lifecycle Agent pane of the admin center.

To learn how to use the agent after it's been configured, see [Use the device lifecycle agent](device-lifecycle-agent-use.md).

## Agent action: refresh

<!--##renew-->

[!INCLUDE [renew](includes/renew.md)]

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431