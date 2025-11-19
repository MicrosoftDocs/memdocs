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

The* Device Offboarding Agent* identifies stale or misaligned devices across Intune and Entra ID, providing actionable insights and requiring admin approval before offboarding any devices. The Device Offboarding Agent complements existing Intune automation by surfacing insights and handling ambiguous cases where automated cleanup may not suffice.

This article provides sample responses to show how the agent helps with device offboarding.

## Before you begin

- This feature is in [public preview](../intune-service/fundamentals/public-preview.md).
- Make sure you meet the requirements detailed in the [Get Started with the Device Offboarding Agent](device-offboarding-agent.md) article.

## Explore the agent options

After configuration, manage the agent from the Device Offboarding Agent pane.

In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**:
- On the **Overview** tab, view the suggestions of devices to offboard, and get more details and remediation steps.
- On the **Suggestions** tab, view the full list of suggestions of devices to offboard, including the completed suggestions.  
- On the **Settings** tab, review details about the agent's configuration.

Select a tab to learn more about its purpose and available options.

# [**Overview**](#tab/overview)

After the Device Offboarding Agent completes a run, the **Overview** tab updates with the agent's list of top suggestions for devices to offboard. The **Overview** tab only displays the suggestions that are *not started* or *in progress*.

The following information is available on this tab: 

- The agent's availability and run status. 
- Agent suggestions, which are the list of devices to offboard that are *not started* or *in progress*.
- Activity section that tracks the current and past run activity of the agent.

:::image type="content" source="images/device-offboarding-agent/overview.png" alt-text="Screenshot of the overview pane of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/overview.png":::

# [**Suggestions**](#tab/suggestions)

Agent suggestions are a list of the top devices to offboard. Suggestions are generated after each agent run based on the latest data. In this tab, you can use search and filters to find specific suggestions.

A suggestion displays the following details: 
- Summary of the suggestions. 
- Factors that the agent considered when suggesting offboarding these devices.  
- Details about the associated suggestions, including the number of devices to offboard, their ownership, and their platform. 
- Recommended actions to offboard securely.

:::image type="content" source="images/device-offboarding-agent/suggestions.png" alt-text="Screenshot of the suggestions tab of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/suggestions.png":::

> [!IMPORTANT]
> Follow the recommended actions in the order they're listed to prevent orphaned devices and ensure secure offboarding.  

After an admin reviews and completes the recommended actions, they can self-attest to applying those actions by updating the **Manage Suggestions** to complete. Marking a suggestion as complete doesn't trigger any device changes by the agent.  

# [**Settings**](#tab/settings)

Use the **Settings** tab to view the agent's current configuration. You can view details about the agent's identity and tailor the agent outputs to your needs by using the optional **Instructions** field.

:::image type="content" source="images/device-offboarding-agent/settings.png" alt-text="Screenshot of the settings tab of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/settings.png":::

---

## Run the agent

To start using the Device Offboarding Agent, first run an evaluation of your device inventory. This action resets the agent's suggestions and status. The agent doesn't persist suggestions across runs; re-running clears previous recommendations.

To manually run the Device Offboarding Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select **Run**.  

The agent runs until it completes its evaluation. You can't stop or pause the process.

> [!NOTE]
> Each time the agent runs, it uses the identity and permissions of the Intune administrator it's configured to use.

## Refresh agent view

Select **Refresh** to update the agent's view with the latest data from its most recent run. This action doesn't trigger a new evaluation; it only refreshes the displayed information to reflect any changes since the last run.

## View and act on suggestions

After running the agent, review its findings to see which devices may need offboarding.

1. In the [Microsoft Intune admin center][INT-AC], go to **Agents** > **Device Offboarding Agent (preview)**.
2. View the agent's suggestions in the **Overview** or **Suggestions** tab.

:::image type="content" source="images/device-offboarding-agent/suggestions.png" alt-text="Screenshot of the suggestions tab of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/suggestions.png":::

Each offboarding suggestion includes detailed context and recommended actions. To manage these suggestions:

- View details and take action: Select a suggestion to review its rationale and initiate offboarding steps.
- Update status: Choose **Manage suggestion** to mark the offboarding action as *In progress* or *Completed*.

:::image type="content" source="images/device-offboarding-agent/suggestion.png" alt-text="Screenshot of a suggestion of the Device Offboarding Agent showing the details and options." border="false" lightbox="images/device-offboarding-agent/suggestion.png":::

## Device Offboarding Agent logs

You can track agent activity and troubleshoot issues using the available logs.

All agent management actions (create, delete, run) and any permission failures are available in [Security Copilot logs](/copilot/security/audit-log). Logs don't include which devices were offboarded or when recommended actions were completed.

[!INCLUDE [errors](includes/errors.md)]

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
