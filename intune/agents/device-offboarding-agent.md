---
title: Device Offboarding Agent Overview
description: Learn about the Device Offboarding Agent in Microsoft Intune, its prerequisites, and how it works.
ms.date: 10/15/2025
ms.topic: overview
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Device Offboarding Agent overview

The Device Offboarding Agent helps IT admins offboard devices securely and efficiently across Microsoft Intune, Microsoft Entra ID, Microsoft Defender, Autopilot, and Apple Business Manager. It analyzes device signals from multiple sources to identify stale or misaligned devices and provides actionable offboarding recommendations. The Device Offboarding Agent complements existing Intune automation by surfacing insights and handling ambiguous cases where automated cleanup may not suffice. All actions require admin approval.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
>To use Security Copilot agents in Microsoft Intune, your organization must meet specific licensing requirements.
>
>Required licenses:
>
> - [Microsoft Intune Plan 1 subscription](../intune-service/fundamentals/licenses.md)
> - [Microsoft Security Copilot](/copilot/security/get-started-security-copilot) with sufficient security compute units (SCUs)
>
> Optional licenses for enhanced functionality:
>
> - [Microsoft Defender for Endpoint (Plan 2)](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint): required for Defender offboarding steps

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]

:::column-end:::
:::column span="3":::
>Required plugins:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
> - [!INCLUDE [plugin-entra](includes/plugin-entra.md)]
>
> [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> The agent supports devices managed by Intune across multiple platforms, including Windows, iOS/iPadOS, macOS, Android, and Linux.\
> It applies to both corporate-owned and BYOD (bring-your-own-device) scenarios.
>
> The agent doesn't support:
> - Shared devices
> - Hybrid Entra-joined Windows devices
> - Microsoft Teams Phones
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> There are different role requirements depending on the action being taken with the agent. For details, see:
>
> - [Configure the Device Offboarding Agent](device-offboarding-agent-configure.md)
> - [Use the Device Offboarding Agent](device-offboarding-agent-use.md)

:::column-end:::
:::row-end:::

## How it works

Signal Aggregation: Collects device data from Intune and Entra ID. 

Evaluation: Assesses devices using predefined logic and optional custom admin instructions. 

Recommendations: Flags devices for offboarding, with suggested actions and rationale. 

Admin Approval: No changes are made without explicit admin approval. 

Assisted Remediation: Upon approval, the Device Offboarding Agent disables Entra ID objects and guides further steps (e.g., Defender offboarding). 

<!--
Workspace: This agent will run in the same preferred workspace you selected for Security Copilot.
Once started, the agent will immediately run in your tenant. You will not be able to cancel an agent mid-run. When the run finishes, you can choose to [remove the agent](#remove-the-agent).

Select **Start agent** to begin the setup process.-->

### Agent identity 

By default, the Device Offboarding Agent runs under the identity and permissions of the admin account that is used to set up the agent.  

The agent behavior is limited to the permissions of the user identity that the agent runs under. 

The agent persistently runs in the identity and permissions of the Intune admin account that is assigned as the agent's identity. 

The agent identity refreshes with each agent run and expires if the agent doesn't run for 90 consecutive days. When the expiration date nears, each Copilot owner and Copilot contributor receives a warning banner about renewal of the agent identity when they view the agent overview page. If the agent authentication expires, subsequent agent runs fail until authentication is renewed. For more information about renewing authentication, see [Renew the agent](device-offboarding-agent-configure.md#renew-the-agent). 

Agent identity: the agent runs using the identity of the user who first set up the agent. Agent authentication expires after 90 days and needs to be renewed. Learn more about agent authentication.

## Limitations 

- An admin must manually start the agent. Once the agent starts, there are no options to stop or pause it. 
- Only start the agent from within the Microsoft Intune admin center. 
- Only the user who sets up the agent can view session details in the Microsoft Security Copilot portal. 
- No suggestion history across runs. If you re-run the agent, the suggestions from the previous runs will be lost.  
- One agent instance per tenant/user context. 
- Only disables Entra ID objects; other remediation steps are instructions for admins. 

## Next steps

- [Configure the Device Offboarding Agent](device-offboarding-agent-configure.md)
- [Use the Device Offboarding Agent](device-offboarding-agent-use.md)

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431