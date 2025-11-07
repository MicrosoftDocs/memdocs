---
title: Change Review Agent Overview
description: Learn about the Change Review Agent in Microsoft Intune, its prerequisites, and how it works.
ms.date: 11/17/2025
ms.topic: overview
author: brenduns
ms.author: brenduns
ms.reviewer: 
---

# Change Review Agent overview
<!-- READY! -->
The Change Review Agent helps Intune admins make faster, more informed decisions in Multi Admin Approval workflows by providing AI-driven recommendations to approve or deny requests, along with contextual insights. It gathers signals from Microsoft Defender for vulnerability as threat data, Microsoft Entra ID as identity risk, and Intune for device and deployment context. The agent uses these signals to assess the risk of Multi Admin Approval requests and offers actionable insights and suggestions to help you take the appropriate action.

## Prerequisites

<!-- start cloud -->
:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]
:::column-end:::

:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.
:::column-end:::
:::row-end:::
<!-- end cloud -->

<!-- start license -->
:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> To use Security Copilot agents in Microsoft Intune, your organization must meet specific licensing requirements.
>
> Required licenses:
> - [Microsoft Intune Plan 1 subscription](../intune-service/fundamentals/licenses.md)
> - [Microsoft Security Copilot](/copilot/security/get-started-security-copilot) with sufficient security compute units (SCUs)
:::column-end:::
:::row-end:::
<!-- end license -->

<!-- stat plugin -->
:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]

:::column-end:::
:::column span="3":::
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions.
>
> The Change Review Agent requires the following plugins:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
>
> Optional plugins:
> 
> - [!INCLUDE [plugin-entra](includes/plugin-entra.md)]
> - [!INCLUDE [plugin-defender](includes/plugin-defender.md)]
>
> [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474).

:::column-end:::
:::row-end:::
<!-- end plugin -->

<!-- start platform ../../media/icons/admin-center/devices.svg  -->
:::row:::
:::column span="1":::
:::image type="icon" source="../media/icons/admin-center/devices.svg" border="false"::: **Platform requirements and scenarios**
:::column-end:::
:::column span="3":::
> The agent supports evaluation and recommendations for the following platforms and scenarios:
> - Windows
> - PowerShell scripts in Intune
:::column-end:::
:::row-end:::
<!-- end platform -->

<!-- start rbac -->
:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> Role requirements vary based on whether you're configuring the agent or using it, and on the specific actions performed.
>
> ---
>
> To **enable and configure** the Change Review Agent, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
>
> :::image type="icon" source="../media/icons/admin-center/defender.svg" border="false"::: Defender roles - Defender role-based access control (RBAC) roles depend on your Defender XDR implementation:
> - [Unified RBAC](/defender-xdr/manage-rbac): Assign the Microsoft Entra ID Security Reader to the agent's identity account. This role provides read-only access to Defender Vulnerability Management data and automatically enforces device group scoping.
> - [Granular RBAC](/defender-endpoint/rbac): Assign a custom RBAC role with permissions equivalent to the Unified RBAC Security Reader role. For example: 
>   - **View data** – **Defender Vulnerability Management** - This permission maps to the Unified RBAC permission *Security posture / Posture management / Vulnerability management (read)*.
>   - **Entra/Identity risky user (read)** - This permission maps to the Unified RBAC permission *Security posture / Identity risk / Risky users (read)*.
>
>    For details about mapping permissions to the Unified RBAC Security Reader role, see [Microsoft Entra Global roles access](/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access) in the *Map Microsoft Defender XDR Unified role-based access control (RBAC)* article in the Defender documentation.
>
>    Ensure the agent’s identity is scoped in Microsoft Defender to include all relevant device groups. The agent can't access or report on devices outside its assigned scope.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot owner](/copilot/security/authentication#security-copilot-roles) 
>
> ---
>
> To **use** the agent and perform offboarding actions, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) or [custom role](/intune/intune-service/fundamentals/role-based-access-control#custom-roles) with equivalent permissions.
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> 
> :::image type="icon" source="../media/icons/admin-center/defender.svg" border="false"::: Defender roles
> - Use of the agent requires the same access as *enabling and configuring* the agent.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot contributor](/copilot/security/authentication#security-copilot-roles)

:::column-end:::
:::row-end:::

## How it works
<!-- READY -->
The Change Review Agent operates using an Intune admins account identity and runs manually when an admin starts it. When started, the agent gathers signals from:

- **Microsoft Defender** for vulnerability and threat insights
- **Microsoft Entra ID** for identity risk
- **Intune** for device and deployment context

After the agent collects signals, it evaluates each Multi Admin Approval request to determine its risk level and generate recommendations. These results are provided for admin review and decision-making.

> [!NOTE]
> The agent runs in the same preferred workspace you selected for the Security Copilot

## Agent identity
<!-- READY! -->
The agent runs under the identity and permissions of the Intune admin account used during setup. You can [change-the-agent-identity](#change-the-agent-identity) after setup if needed.

The agent’s actions are limited to the permissions of that account, and the identity refreshes with each run. If the agent doesn’t run for 90 consecutive days, its authentication expires, and subsequent runs fail until its renewed. To maintain functionality, renew the agent identity before the 90-day limit.

### Change the agent identity
<!-- READY -->
After setup, the agent identity can be changed. A change of the agent identity doesn't affect the agent's run history. The identity changes when:

- A different admin account than current identity is used to [renew](#renew-the-agent) the agent.
- The agent settings are edited to explicitly assign a new agent identity. 

**To assign a new agent identity**:
1. Open the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Agents** > select the Agent's tile > and then select the **Settings** tab.
1. Locate *Identity*, which displays the current user account the agent uses. 
1. Select the **Chose another identity** button to open an account sign-in prompt. Use the prompt to select and authenticate a new account as the agents identity.

> [!IMPORTANT]
> The agent can only perform operations allowed by the permissions of the account it runs under. If that  account lacks [required permissions](#prerequisites), the agent fails to run.


## Operational considerations
<!-- READY -->
Before running the Change Review Agent, keep these points in mind:

- An admin must manually start the agent. After it starts, there's no option to stop or pause it.
- The agent can only be started from the Microsoft Intune admin center.
- Session details in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) are visible only to the user who set up the agent.
- Suggestions don't persist across runs; rerunning the agent clears previous recommendations.
- Only one agent instance is supported per tenant/user context.

## Enable the agent
<!-- READY -->
To enable the Change Review Agent, follow these steps:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** and select the agent you want to enable.
2. On the **Overview** tab, select **Set up Agent** to open the set-up pane.
3. Review the details to ensure requirements are in place, then select **Start agent**.

The agent runs until it finishes and then displays its results in the **Overview** tab.

## Explore the agent options
<!-- REVIEW after DEMO ---  Pending -->
After you configure the agent, you can manage it from the Change Review Agent pane.

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Change Review Agent**:
- On the **Overview** tab, see the agent runt status, review suggestions for the top Multi Admin Approval requests, and see the record of recent agent activity. 
- On the **Suggestions** tab, view the full list of suggestions for approval requests, including suggestions that are *Not started*, *In progress*, or *Completed*.
- On the **Settings** tab, review details about the agent's configuration.

To learn more about each tab, select the following tabs:

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

## Configure custom instructions 

Use custom instructions to guide the agent's logic based on your organization's needs. Custom instructions help refine the agent's evaluation criteria, allowing you to include or exclude specific devices from offboarding recommendations.

These instructions can be used to:
- Exclude changes that affect specific accounts, like break-glass/emergency accounts from all policy suggestions.
- Prioritize approvals for specify policy types, like compliance policies.
- Triage high-risk users first (executives and admins).

For example, << **EXAMPLE HERE**>>. Custom instructions help you prevent that issue by guiding the agent's logic based on your organizational needs.

Custom instructions persist between agent runs. Once they're set, they're evaluated every time the agent runs. You can change custom instructions at any time in the Settings tab and rerun the agent. The Factors section in a suggestion highlights details on which custom instructions were taken into account while forming the list of suggested devices to offboard.

To configure custom instructions:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Change Review Agent**.
1. Select the **Settings** tab.
In the **Instructions** field, enter a prompt to customize the agent's evaluation criteria.

<!-- ## Renew the agent  --  H2 header is in the Include:  -->
[!INCLUDE [renew](includes/renew.md)]

<!-- My version of the note in the Include:
> [!IMPORTANT]
> When renewing agent authentication, the agent adopts the credentials of the user performing the renewal. To keep the agent’s identity unchanged, the same user who originally authorized the agent must also renew it.
 -->

<!--  ## Remove the agent  --  H2 header is in the Include:  -->
[!INCLUDE [remove](includes/remove.md)]


## Next steps

- [Use the Change Review Agent](/intune/agents/change-review-agent-use)