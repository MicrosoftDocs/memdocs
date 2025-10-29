---
title: Configure the Device Offboarding Agent
description: Learn how to configure the Device Offboarding Agent in Microsoft Intune to identify and offboard devices that are no longer in use.
ms.date: 10/15/2025
ms.topic: how-to
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Configure the Device Offboarding Agent

This article describes how to configure the Device Offboarding Agent in Microsoft Intune.

## Prerequisites

Before you get started, ensure you meet the requirements listed in the overview article: [Device Offboarding Agent overview](device-offboarding-agent.md). The following additional prerequisite are required to configure the agent.

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

:::column-end:::
:::row-end:::
 
## Enable the agent

To enable the Device Offboarding Agent, follow these steps:

:::row:::
:::column span="3":::
1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select **Set up Agent** to open the set-up pane.
1. Review the details to ensure requirements are in place, then select **Start agent**.
:::column-end:::
:::column span="1":::
:::image type="icon" source="icons/add-agent.svg" border="false":::
:::column-end:::
:::row-end:::

The agent runs until it finishes and then displays its results in the Device Offboarding Agent pane.

:::image type="content" source="images/device-offboarding-agent-overview.png" alt-text="Screenshot of the overview pane of the Device Offboarding Agent." border="false":::

## Explore the agent pane

After you configure the agent, you can manage it from the Device Offboarding Agent pane.

In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**:
- On the **Overview** tab, view the suggestions of devices to offboard, and get more details and remediation steps.
- On the **Suggestions** tab, view the full list of suggestions of devices to offboard, including the completed suggestions.  
- On the **Settings** tab, review details about the agent's configuration.

To learn more about each tab, select the following tabs:

# [**Overview**](#tab/overview)

After the Device Offboarding Agent completes a run, the Overview tab updates with the agent's list of top suggestions for devices to offboard. The Overview tab only displays the suggestions that are *not started* or *in progress*.  

The following information is available on this tab: 

- The agent's availability and run status. 
- Agent suggestions, which are the list of devices to offboard that are *not started* or *in progress*. 

# [**Suggestions**](#tab/suggestions)

Agent suggestions are a list of the top devices to offboard, identified based on data from Microsoft Intune and Microsoft Entra.  

A suggestion displays the following details: 
- Summary of the suggestions. 
- Factors that the agent considered when suggesting offboarding these devices.  
- Details about the associated suggestions, including the number of devices to offboard, their ownership, and their platform. 
- Recommended actions to offboard securely.  

> [!IMPORTANT]
> Follow the recommended actions in the order they're listed to prevent orphaned devices and ensure secure offboarding.  

After an admin reviews and completes the recommended actions, they can self-attest to applying those actions by updating the **Manage Suggestions** to complete. Marking a suggestion as complete doesn't trigger any device changes by the agent.  

### Activity 

This section tracks the current and past run activity of the agent.

# [**Settings**](#tab/settings)

Use the **Settings** tab to view the agent's current configuration. You can view details about the agent's identity and tailor the agent outputs to your needs by using the optional **Instructions** field.

### Custom instructions 

With the **Instruction** field, you can provide a prompt that influences how the agent runs. Common use cases include:

- Including or excluding specific object IDs
- Setting thresholds for device activity

For example, if your organization has executive devices that you don't want to flag for offboarding, you can use custom instructions to exclude them. Without this exclusion, the agent might detect identity mismatches on those devices and consume SCUs to suggest offboarding—even when it's not appropriate. Custom instructions help you prevent that issue by guiding the agent's logic based on your organizational needs.

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

To learn how to use the agent after you configure it, see [Use the Device Offboarding Agent](device-offboarding-agent-use.md).

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431