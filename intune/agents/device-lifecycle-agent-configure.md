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

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Set up Agent** to open the set-up pane.
1. Review the details to ensure requirements are in place, and then select **Start agent** to close the set-up pane and start the first run of the agent.

The agent runs until it finishes and then displays its results in the Device Lifecycle Agent pane of the admin center.

### Manage devices and the agent 

After the agent completes its initial run, admins can review and manage the Device Lifecycle Agent suggestions in the Intune admin center.

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
  1. By default, the agent page opens to the **Overview** tab. On this tab, admins can view the suggestions of devices to offboard, drill in for more details and remediation steps.
  1. The second available tab is **Suggestions**, which provides the full list of suggestions of devices to offboard, including the completed suggestions.  
  1. The other available tab is **Settings**, which provides limited details about the agent's configuration. 

## Agent action: refresh

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431