---
title: "Device lifecycle agent: configuration"
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Device lifecycle agent: configuration

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune admin roles:
> - Intune Administrator
> - Read Only Operator
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra admin roles:
> - Security Reader
>
> For initial setup:
> - Copilot Owner required for setup
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


## Agent action: refresh

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431