---
title: Change Review Agent Overview
description: Learn about the Change Review Agent in Microsoft Intune, its prerequisites, and how it works.
ms.date: 11/10/2025
ms.topic: overview
author: brenduns
ms.author: brenduns
ms.reviewer: zinebtakafi
---

# Change Review Agent overview

In public preview, the Microsoft Intune Change Review Agent uses Microsoft Security Copilot’s generative AI to evaluate Multi Admin Approval requests for PowerShell scripts on Windows devices. It provides risk-based recommendations and contextual insights to help administrators understand script behavior and associated risks. These insights help Intune administrators make informed decisions more quickly about whether to approve or deny requests.

To generate these recommendations, the agent aggregates signals from multiple sources:

- Microsoft Defender Vulnerability Management - for threat insights
- Microsoft -Entra ID - for identity risk
- Microsoft Intune - for Multi Admin Approval requests and historical context of similar requests

The agent analyzes these signals to assess the potential risk associated with each request and then delivers actionable insights to support secure and efficient change management.

## Prerequisites

<!-- start cloud -->
:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]
:::column-end:::

:::column span="3":::
> The agent is supported on the public cloud only. It isn't supported on government clouds.
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
> - [Microsoft Entra ID P2](/entra/fundamentals/licensing)
> - [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/tvm-prerequisites)
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
> - [!INCLUDE [plugin-entra](includes/plugin-entra.md)]
> - [!INCLUDE [plugin-defender-xdr](includes/plugin-defender-xdr.md)]
> - [!INCLUDE [plugin-threat-intelligence](includes/plugin-threat-intelligence.md)]
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
> - [*Intune Administrator*](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
> - [*Security Reader*](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> - *Entra/Identity risky user (read)* - This permission maps to the Unified RBAC permission *Security posture / Identity risk / Risky users (read)*.
>
> :::image type="icon" source="../media/icons/admin-center/defender.svg" border="false"::: Defender roles - Defender role-based access control (RBAC) roles depend on your Defender XDR implementation:
> - [*Unified RBAC*](/defender-xdr/manage-rbac): Assign the Microsoft Entra ID Security Reader to the agent's identity account. This role provides read-only access to Defender Vulnerability Management data and automatically enforces device group scoping.
> - [*Granular RBAC*](/defender-endpoint/rbac): Assign a custom RBAC role with permissions equivalent to the Unified RBAC Security Reader role. For example: 
>   - *View data – Defender Vulnerability Management* - This permission maps to the Unified RBAC permission *Security posture / Posture management / Vulnerability management (read)*.
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

## How the agent works

The Change Review Agent operates using an Intune admins account identity and runs manually when an admin starts it.

At a high level, the agent does the following steps each time it runs:

1. **Signal aggregation** - The agent begins by aggregating signals from the following sources:

   - Microsoft Defender Vulnerability Management - for threat insights
   - Microsoft Entra ID - for identity risk
   - Microsoft Intune - for Multi Admin Approval requests and historical context of similar requests

2. **Evaluation** - The agent evaluates Windows PowerShell scripts for Multi Admin Approval requests using predefined logic that's built in to the agent configuration.

3. **Recommendations** - The agent reviews and then provides recomendations for a maximum of 10 requests per run.

   Suggestions are *suggestions* only. The approval or rejection of a request remains with an Intune administrator.

   The first column of the recommendation list presents Suggested Next Steps, which display the recommended action followed by the name of the request. Possible actions include:

   - Approve - Low-risk request; likely safe to approve.
   - Reject - High-risk request; shouldn't be approved.
   - Needs more info - Risk couldn't be fully assessed. This request requires further review.

   Each recommendation includes supporting details that explain:
   - The rationale behind the agent’s recommendation.
   - What the script is intended to accomplish or do.
   - A detailed list of factors that the agent reviewed as part of its process.

## Agent identity

The agent runs under the identity and permissions of the Intune admin account used during setup. The agent’s actions are limited to the permissions of that account, and the identity refreshes with each run. If the agent doesn’t run for 90 consecutive days, its authentication expires, and subsequent runs fail until its renewed. To maintain functionality, renew the agent identity before the 90-day limit.

## Operational considerations

Before setting up and starting the agent for the first time, review the following considerations:

- An admin must manually start the agent. Once started, there’s no option to stop or pause it.
- The agent can only be started from the Microsoft Intune admin center.
- Session details in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) are visible only to the user who set up the agent.
- The agent reviews and then provides recomendations for a maximum of 10 requests per run.
- Only one agent instance is supported per tenant/user context.

## Set up the agent

The agent operates under the identity and permissions of the Intune admin account used during setup. Its operations are limited to the permissions of that account, and the identity refreshes with each run. Any changes to the account’s permissions affect the agent’s capabilities during its next run.

**To set up the Change Review Agent:**

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Agents** > **Change Review Agent**.

2. In **Overview**, select **Set up Agent** to open the *Set up Change review agent* pane.

3. The **Set up Change review agent** pane lists the required permissions and provides details about setup requirements. When requirements are met, select **Start agent**.

   :::image type="content" source="./media/change-review-agent/setup.png" alt-text="Screenshot of the Set up Change review agent pane." :::

The agent operates until it completes its evaluation and displays results in the Overview tab. When the run finishes, the agent is ready to use.

To learn more about using the agent, see [Use the Change Review Agent](change-review-agent-use.md).

<!--  ## Remove the agent  --  H2 header is in the Include:  -->
[!INCLUDE [remove](includes/remove.md)]

## Related content

- [Use the Change Review Agent](/intune/agents/change-review-agent-use)
