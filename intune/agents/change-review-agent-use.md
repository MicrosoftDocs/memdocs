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

In public preview, the [Change Review Agent](change-review-agent.md) is a generative AI feature in Intune. The agent evaluates Multi Admin Approval requests for PowerShell scripts on Windows devices to provide risk-based recommendations and contextual insights to help administrators understand script behavior and associated risks for the change requests. These insights help Intune administrators make informed decisions more quickly about whether to approve or deny requests.

After the [agent is set up](change-review-agent.md#set-up-the-agent), it's recommendations can be viewed, and the agent can be run again on demand to refresh its recommendations.


## Prerequisites

Before you begin, make sure you meet the requirements detailed in the [Change Review Agent overview](change-review-agent.md#prerequisites) article.

## Explore the agent

After you configure the agent, you can manage it from the Change Review Agent pane.

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Change Review Agent**:
- On the **Overview** tab, review the agent run status, suggestions for the top Multi Admin Approval requests, and the records of recent agent activity.
- On the **Suggestions** tab, view the full list of suggestions for approval requests, including suggestions that are *Not started*, *In progress*, or *Completed*.
- On the **Settings** tab, review details about the agent's configuration.

To learn more about each tab, select the following tabs:

# [**Overview**](#tab/overview)
 
The following information is available on this tab: 

- The agent's availability and run status.
- Agent suggestion for a list of top change requests. This list displays a few of the results, focused on requests that are assessed to have the least risk and are safe to approve.
- Activity section that tracks the current and past run activity of the agent.

After the Change Review Agent completes a run, thos tab updates with the agent's list of top suggestions for Multi Admin Approval change requests The Overview tab displays only a few suggestions at a time with the full list available on the *Suggestions* tab. You can use either tab to drill in and review and manage recomendations from the agent.

<!-- No image source yet:
:::image type="content" source="images/change-review-agent/overview.png" alt-text="Screenshot of the overview pane of the Change Review Agent." border="false" lightbox="images/change-review-age/overview.png":::
-->

# [**Suggestions**](#tab/suggestions)

On the Suggestions tab you can view the full list of Agent suggestions for Multi Admin Approval change requests. Suggestions are generated after each agent run and are based on the latest data. In this tab, you can use search and filters to find specific suggestions.

A list of suggestions includes columns with the following details:

- A risk assessment of the change request.
- The account used to submit the request.
- When the request expires.
- Status of the request, from *Not started* to *Completed*.
- Details about the associated suggestions. 

<!-- No image source yet:
:::image type="content" source="images/change-review-agent/suggestions.png" alt-text="Screenshot of the suggestions tab of the Change Review Agent." border="false" lightbox="images/change-review-agent/suggestions.png":::
-->

After an admin reviews and completes the recommended actions for a request, they can self-attest to applying those actions by updating the **Manage Suggestions** to *complete*. Marking a suggestion as *complete* doesn't trigger any changes by the agent.

# [**Settings**](#tab/settings)

Use the **Settings** tab to view the details about the agent's identity and current configuration.

<!-- No image source yet:
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

Upon review of each change request, the agent appends a recommendation to the name of the request and presents it on a list of *Suggested next steps*. You can find and manage suggestions from both the *Overview* and *Suggestions* tab of the agent. The agents recommendations include: 

   - **Approve** - This is a low-risk request that is assessed to be save to approve. 
   - **Reject** - A high-risk request that shouldn't be approved.
   - **Needs more info** - Risk couldn't be fully assessed. This request requires further review.
 
To review what went into the agents recommendation for a request, select the name of the request from either the *Overview* or *Suggestions* tab of the agent. Selecting the name opens the *Manage suggestion* view, which is a detailed review of that request. THis view includes the following information:

- **Suggested action** - The suggested action section begins with one of three recommendations, *Approve*, *Reject*, or *Needs more info*. The first paragraph of this section explains how the agent arrived at its recommendation. The second paragraph provides details about the requests PowerShell script including what it does and interacts with, and details should it identified as malicious.

- **Factors** - This is a detailed break down of specific details the agent reviewed for its assessment, including a script analysis, identity reviews of the account used to submit the request, and more.

- **View request** - Near the bottom of the *Manage suggestion* view is the *View request* button. TFor a PowerShell request, this option opens a pane where you can review the scripts contents, line by line.

- **Details** - This tile displays high-level status details about the request, including its risk level, current approval status, and business justification. 

## Agent logs

You can track agent activity and troubleshoot issues using the available logs.

All agent management actions that are taken, and any permission failures are available in Security Copilot logs. Logs do not include details from the recomendations, or when recommended actions were completed.

## Related content

- [Change Review Agent in Intune](change-review-agent.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)