---
title: Use the Change Review Agent
description: Learn how to use the Change Review Agent in Microsoft Intune.
ms.date: 11/17/2025
ms.topic: how-to
author: brenduns
ms.author: brenduns
ms.reviewer: zinebtakafi
---

# Use the Change Review Agent

The [Change Review Agent](change-review-agent.md) (public preview) is a generative AI feature in Intune. It evaluates Multi Admin Approval requests for PowerShell scripts on Windows devices and provides risk-based recommendations with contextual insights. These insights help administrators understand script behavior and associated risks, so they can decide whether to approve or deny requests more quickly.

After the [agent is set up](change-review-agent.md#set-up-the-agent), its recommendations can be viewed, and the agent can be run again on demand to refresh its recommendations.


## Prerequisites

Before you start, review the requirements in the [Change Review Agent overview](change-review-agent.md#prerequisites) article.

## Explore the Change Review Agent

After configuration, manage the agent from the Change Review Agent pane.

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Change Review Agent**. The agent includes the following three tabs:

- **Overview** - View the agent's current status, suggestions for the top Multi Admin Approval requests, and the records of recent agent activity.
- **Suggestions** - Here you'll find the full list of suggestions for assessed approval requests.
- **Settings** - This tab displays the agent's configuration details.

To learn more about each tab, select the following tabs:

# [**Overview**](#tab/overview)
 
The Overview tab includes:

- **Agent status** - Various tiles introduce the agent, detail whether the agent is available and its current run status.
- **Agent suggestions** – This short list highlights the top suggestions for Multi-Admin Approval requests. Recommended actions include approving low-risk requests and rejecting those assessed as high-risk.
- **Activity** – This area displays records  of the current and past agent runs. 

After the agent completes a run, the Overview tab updates with its top suggestions for Multi Admin Approval requests. This tab shows only a few suggestions at a time; the full list is available on the Suggestions tab. Use either tab to drill down and review or manage recommendations.

:::image type="content" source="./media/change-review-agent-use/overview.png" alt-text="Screenshot of the overview pane of the Change Review Agent." :::

# [**Suggestions**](#tab/suggestions)

The *Suggestions* tab shows the full list of requests reviewed by the agent. Suggestions are generated after each agent run and reflect the latest data. Use search and filters to find specific suggestions.

Each suggestion includes columns with these details:

- **Risk threshold** - An assessment of the change request.
- **Resource type** - The type of request, such as PowerShell script
- **Requested by** - The user account that submitted the request.
- **Approval expiration** - The Date when the request expires if no action is taken.
- **Status** - Current status of the request. Requests that require no further action are marked as *Completed*.

:::image type="content" source="./media/change-review-agent-use/suggestions.png" alt-text="Screenshot of the suggestions tab of the Change Review Agent." :::

# [**Settings**](#tab/settings)

Use the Settings tab to view details about the agent's identity, current configuration, and requirements. This includes:

- **Agent jobs** - Request types that agent reviews.
- **Identity** - Details about the agents use of a user account as its identity.
- **Required permissions** – Role-based access controls required to configure or use the agent.
- **Plugins** – Components the agent uses during evaluation.

:::image type="content" source="./media/change-review-agent-use/settings.png" alt-text="Screenshot of the settings tab of the Change Review Agent." :::

---

## Run the Change Review Agent

Run the agent to refresh recommendations and evaluate new Multi Admin Approval requests. The agent runs until evaluation completes; you can't stop or pause it.

The agent uses the identity and permissions of the assigned Intune admin account. Its operations are limited to the permissions of that account. If the agent doesn't run for 90 consecutive days, its authentication expires and subsequent runs fail until the identity is renewed.

The agent doesn't support scheduled runs and must be started manually each time you want to update its results.

**To manually run the Change Review Agent:**

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Agents** > **Change Review Agent**.
2. Select **Run**, located above the agent's tab selection.


## Manage agent suggestions

Use the Change Review Agent node to review and manage (approve or reject) Multi Admin Approval script requests.

To review and manage a request that's been evaluated by the agent, select an agent suggestion from the **Suggested Next Steps** column in either the *Overview* or *Suggestions* tab. Intune opens a new window showing the detailed results of the agent's review for that request. The detailed view is named after the selected suggestion and includes the agent's recommendation followed by the name of the request. For example, the following image shows the upper part of the review details for a request named *ReputationScoreScript*, which the agent recommends rejecting:

:::image type="content" source="./media/change-review-agent-use/reject.png" alt-text="Screenshot of the details for a rejected request." :::

 The following are the agent recommendations you might see:

- **Approve** – A low-risk request assessed as safe to approve.
- **Reject** – A high-risk request that shouldn't be approved.
- **Needs more info** – The risk couldn't be fully assessed, and the request requires careful admin review.

When you open an agent suggestion, the review page is divided into two main areas. Each area provides specific information to help you understand the recommendation. 

> [!TIP]
> Near the end of this section are details for the *View request* button. You can use this button to open the Multi Admin Approval request and then *approve* or *reject* it. The final decision to approve or reject a request always remains with the admin.

- **Details tile**

  On the right side, this tile displays metadata related to the agent suggestion.

- **Main tile**

  On the left side, this tile displays the following sections and information:

  - **Suggested action:**  
    This section provides a summary of the agent's review, including key details to help you decide whether to accept or reject the request. It outlines the rationale behind the assessment and includes a brief overview of the script.

  - **Factors:**
    Factors are the specific details and conditions the agent considered when evaluating the script.

  - **Additional resources and feedback:**

    Below the *Factors* section, you'll find:
    - Links to relevant content for the skills the agent used during evaluation.
    - A simple feedback system to share your input on the agent's results.

  - **View request:**
    This button opens a review window for the current request. The review window provides the same options available in the *Multi Admin Approval* node of the admin center

    - Use the *Approver note* to explain your decision for this request.
    - Complete the approval process by selecting **Approve request** or **Reject request**.

    After you approve or reject the request, the agent suggestion status changes to **Completed**.

## Agent logs

Security Copilot logs include all agent management actions and permission failures. Logs don't include recommendation details or completion times.

[!INCLUDE [errors](includes/errors.md)]

### Security Copilot couldn’t retrieve details for this factor at this time

The agent was unable to retrieve details related to the specified factor. The exact reason for this failure is unknown.

### Couldn't complete your request. Security Copilot doesn't currently support that type of request

The agent cannot proceed because the request violates Microsoft's Responsible AI policies. This typically occurs when the system detects a prohibited action, like a prompt injection attempt.


## Related content

- [Change Review Agent in Intune](change-review-agent.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)