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

After the [agent is set up](change-review-agent.md#set-up-the-agent), its recommendations can be viewed, and the agent can be run again on demand to refresh its recommendations.


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

After the Change Review Agent completes a run, this tab updates with the agent's list of top suggestions for Multi Admin Approval change requests. The Overview tab displays only a few suggestions at a time with the full list available on the *Suggestions* tab. You can use either tab to drill in and review and manage recommendations from the agent.

:::image type="content" source="./media/change-review-agent-use/overview.png" alt-text="Screenshot of the overview pane of the Change Review Agent." :::

# [**Suggestions**](#tab/suggestions)

This tab displays the full list of requests that the agent reviewed. Suggestions are generated after each agent run and are based on the latest data. In this tab, you can use search and filters to find specific suggestions. \

A list of suggestions includes columns with the following details:

- Risk threshold - An assessment of the change request.
- Resource type - The type of request, like PowerShell script
- Requested by - The user account that submitted the request.
- Approval expiration - When the request expires if not acted on.
- Status - The status of the request. Requests that require no further action are marked as *Completed*.

:::image type="content" source="./media/change-review-agent-use/suggestions.png" alt-text="Screenshot of the suggestions tab of the Change Review Agent." :::

# [**Settings**](#tab/settings)

Use this tab to view the details about the agent's identity and current configuration and requirements, like plugins the agent uses and the role-based access controls necessary to configure or use the agent.

---

## Run the Agent

Run the agent to refresh its recommendations and evaluate new Multi Admin Approval requests. When started, the agent operates until it completes its evaluation. You can’t stop or pause the process.

The agent operates under the identity and permissions of the assigned Intune admin account. Its operations are limited to the permissions of that account. If the agent doesn’t run for 90 consecutive days, its authentication expires and subsequent runs fail until the identity is renewed.

The agent doesn't support scheduled runs and must be started manually each time you want to update its results.

**To manually run the Change Review Agent:**

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Agents** > **Change Review Agent**.
2. Select **Run**, located above the agent’s tab selection.


## Manage suggestions

You can use the Change Review Agent node to deeply review and then manage (approve or reject) the Multi Admin Approval script request.

To review and manage a request that's been evaluated by the agent, select an agent suggestion from the **Suggested Next Steps** column in either the *Overview* or *Suggestions* tab. Intune opens a new window showing the detailed results of the agent’s review for that request. The detailed view is named after the selected suggestion and includes the agent’s recommendation followed by the name of the request. For example, the following image shows the upper part of the review details for a request named *ReputationScoreScript*, which the agent recommends rejecting:

:::image type="content" source="./media/change-review-agent-use/reject.png" alt-text="Screenshot of the details for a rejected request." :::

 The following are the agent recommendations you might see:

- **Approve** – A low-risk request assessed as safe to approve.
- **Reject** – A high-risk request that shouldn't be approved.
- **Needs more info** – The risk couldn’t be fully assessed, and the request requires careful admin review.

When you open an agent suggestion, the review page is divided into two main areas. Each area provides specific information to help you understand the recommendation. At the bottom of this information are details for the *View request* button, which is used to open the Multi Admin Approval request where you can then approve or reject the request. The final decision to approve or reject a request always remains with the admin.

- **Details tile**

  On the right side, this tile displays metadata related to the agent suggestion.

- **Main tile**

  On the left side, this tile displays the following sections and information:

  - **Suggested action:**  
    This provides a summary of the agent’s review and details that can help you make a decision to accept or reject the request:
    - The first paragraph explains the rationale behind the agent’s recommendation.
    - The second paragraph summarizes what the PowerShell script does or the potential effects if it's approved to run.

  - **Factors:**
    Factors are the specific details and conditions the agent considered when evaluating the script.

  - **Additional resources and feedback:**

    Below the *Factors* section, you’ll find:
    - Links to relevant content for the skills the agent used during evaluation.
    - A simple feedback system to share your input on the agent’s results.

  - **View request:**
    This button opens a review window for the current request. The review window provides the same options available in the *Multi Admin Approval* node of the admin center

    - Use the *Approver note* to explain your decision for this request.
    - Complete the approval process by selecting **Approve request** or **Reject request**.

    After you approve or reject the request, the agent suggestion status changes to **Completed**.

## Agent logs

You can track agent activity and troubleshoot issues using the available logs.

All agent management actions that are taken, and any permission failures are available in Security Copilot logs. Logs don't include details from the recommendations, or when recommended actions were completed.

## Related content

- [Change Review Agent in Intune](change-review-agent.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)