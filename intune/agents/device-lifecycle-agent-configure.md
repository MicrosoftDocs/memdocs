---
title: "Device lifecycle agent: configuration and use"
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Device lifecycle agent: configuration and use

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune admin roles:
> - Intune Administrator
> - Read Only Operator
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra admin roles:
> - Security Reader
>
> For initial setup:
> - Copilot Owner required for setup
>
> For results:
> - Copilot Contributor 
>
> To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to set up, run, or view results from the agent.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
> - Microsoft Intune subscription (Plan 1 or equivalent). 
> - Microsoft Security Copilot access with sufficient security compute units (SCUs). 
> - Microsoft Entra ID integrated with Intune (Free or P1). 
> - Optional: Microsoft Defender for Endpoint (Plan 2) for Defender offboarding steps. 

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.

:::column-end:::
:::row-end:::
 
## Configure the agent

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent**.

## Agent action: run

To manually run the Device Lifecycle Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Run**.  

When an agent run starts, the agent runs until it completes its evaluation. It can't be stopped or paused. 

> [!NOTE]
> Each time the agent runs, it runs under the identity and permissions of the Intune administrator that its been configured to use. 

## Agent action: refresh

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

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

<!--##renew-->

[!INCLUDE [renew](includes/renew.md)]

## Device Lifecycle Agent logs 

All agent management, create, delete, run, and any permission failures are available in Security Copilot logs. Logging of which devices were offboarded or when a recommended actions were complete aren't available. Instead, use the options to mark a suggestion as complete.  

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431