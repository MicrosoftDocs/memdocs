---
title: Configure the Device Lifecycle Agent
description: 
ms.date: 10/15/2025
ms.topic: how-to
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
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
> - [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
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

## Explore the agent pane

Once the agent is configured, you can manage it from the device lifecycle agent pane.

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
  1. By default, the agent page opens to the **Overview** tab. On this tab, admins can view the suggestions of devices to offboard, drill in for more details and remediation steps.
  1. The second available tab is **Suggestions**, which provides the full list of suggestions of devices to offboard, including the completed suggestions.  
  1. The other available tab is **Settings**, which provides limited details about the agent's configuration.

# [**Overview**](#tab/overview)

After the Device Lifecycle Agent completes a run, the Overview tab updates with the agents list of top suggestions of devices to offboard. The Overview tab only displays the "not started" and "in progress" suggestions.  

The following information is available on this tab: 

- The agent's availability and run status. 
- Agent suggestions, which are the list of devices to offboard which are "not started" or "in progress" 

# [**Suggestions**](#tab/suggestions)

Agent suggestions are a list of the top devices to offboard identified based on the data from Microsoft Intune and Microsoft Entra.  

A suggestion displays the following details: 
- Summary of the suggestions. 
- Factors that were considered by the agent to suggest offboarding these devices.  
- Details about the associated suggestions (number of devices to offboard, their ownership, and their platform) 
- Recommended actions to offboard securely.  

> [!IMPORTANT]
> Follow the recommended actions in the order they are listed to prevent orphaned devices and ensure offboarding securely.  

After an admin reviews and completes the recommended actions, they can self-attest to applying those actions by updating the Manage Suggestions to complete. Marking a suggestion as complete doesn't trigger any device changes by the agent.  

### Activity 

This section tracks the current and past run activity of the agent.  

###

# [**Settings**](#tab/settings)

Use the **Settings** tab to view the agent's current configuration. You can view details about the agent's identity and tailor the agent outputs to your needs using the optional **Instructions** field.

### Custom instructions 

With the **Instruction** field you can provide a prompt that influences how the agent runs. Common use cases include:

- Including or excluding specific object IDs
- Setting thresholds for device activity

For example, if your organization has executive devices that shouldn't be flagged for offboarding, you can use custom instructions to exclude them. Without this, the agent might detect identity mismatches on those devices and consume SCUs to suggest offboarding—even when it's not appropriate. Custom instructions help you prevent that by guiding the agent's logic based on your organizational needs.

Examples of custom instructions you can use:

```agent-prompt
Exclude from all recommendations if device has been inactive in Entra for less than [n] days 

Include in all recommendations if device has been active in Entra more than [n] days ago 

Exclude [device ID] from all recommendations 

Exclude [device ID] from recommendation if retired is true 

Include [device ID] in all recommendations 

Include only [device ID] in recommendations
```

---

## Agent actions

### Refresh

<!--##renew-->

[!INCLUDE [renew](includes/renew.md)]

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

<!-- admin center links -->

## Next steps

To learn how to use the agent after it's been configured, see [Use the device lifecycle agent](device-lifecycle-agent-use.md).

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431