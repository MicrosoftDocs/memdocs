---
title: Use the Change Review Agent
description: Learn how to use the Change Review Agent in Microsoft Intune.
ms.date: 11/17/2025
ms.topic: how-to
author: brenduns
ms.author: brenduns
ms.reviewer: 
---

# Use the Change Review Agent

> [!WARNING]
> This article is still being written. Do not use it or share any information from this article.




## Prerequisites

Before you begin, make sure you meet the requirements detailed in the Get Started with the [Change Review Agent](change-review-agent.md#prerequisites) article.

## Explore the agent

To explore and use the agent, open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Agents** > **Change Review Agent**, which opens the agent page. Depending on what you want to accomplish, choose one of the following tabs:

- Overview – Displays the agent’s status, recent runs, and results.
- Suggestions – Shows risk assessments and manage recommendations for Multi Admin Approval requests.
- Settings – Provides configuration options, including the agent identity and custom instructions.

To learn more about each tab, select its name for detailed information.

# [**Overview**](#tab/overview)
<!-- REVIEW For accuracy to agent - Add Images -->
After the Change Review Agent completes a run, the **Overview** tab updates with the agent's list of top suggestions for Multi Admin Approval change requests. The **Overview** tab only displays the suggestions that are *Not started* or *In progress*.

The following information is available on this tab: 

- The agent's availability and run status. 
- Agent suggestion for a list of top change requests. This list includes requests that are assessed to have the least risk and are safe to approve. 
- Activity section that tracks the current and past run activity of the agent.

<!-- No image source yet - Figma has not been updated >
:::image type="content" source="images/change-review-agent/overview.png" alt-text="Screenshot of the overview pane of the Change Review Agent." border="false" lightbox="images/change-review-age/overview.png":::
-->

# [**Suggestions**](#tab/suggestions)
<!-- REVIEW For accuracy to agent - Add Images -->
Agent suggestions are a list of all Multi Admin Approval change requests. Suggestions are generated after each agent run based on the latest data. In this tab, you can use search and filters to find specific suggestions.

A suggestion displays the following details: 
- A risk assessment of the change request. 
- The account used to submit the request.
- When the request expires.
- Status of the request, from *Not started* to *Completed*.
- Details about the associated suggestions. 

<!-- No image source yet - Figma has not been updated >
:::image type="content" source="images/change-review-agent/suggestions.png" alt-text="Screenshot of the suggestions tab of the Change Review Agent." border="false" lightbox="images/change-review-agent/suggestions.png":::
-->

After an admin reviews and completes the recommended actions, they can self-attest to applying those actions by updating the **Manage Suggestions** to *complete*. Marking a suggestion as complete doesn't trigger any changes by the agent.

# [**Settings**](#tab/settings)
<!-- REVIEW For accuracy to agent - Add Images -->
Use the **Settings** tab to view the details about the agent's identity and current configuration.

<!-- No image source yet - Figma has not been updated >
:::image type="content" source="images/change-review-agent/settings.png" alt-text="Screenshot of the settings tab of the Change Review Agent." border="false" lightbox="images/change-review-agent/settings.png":::
-->

---
## Run the Agent

Run the agent to refresh its recommendations and evaluate new Multi Admin Approval requests. When started, the agent operates until it completes its evaluation. You can’t stop or pause the process.

The agent operates under the identity and permissions of the assigned Intune admin account. Its operations are limited to the permissions of that account. If the agent doesn’t run for 90 consecutive days, its authentication expires and subsequent runs fail until the identity is renewed.

The agent doesn't support scheduled runs and must be started manually each time you want to update its results.

**To manually run the Change Review Agent:**

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Agents** > **Change Review Agent**.
2. Select **Run**, located above the agent’s tab selection.

## Manage recommendations

## Agent logs

## Related content
