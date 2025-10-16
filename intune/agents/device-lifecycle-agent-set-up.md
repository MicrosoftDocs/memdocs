---
title: Set up the device lifecycle agent
description: 
ms.date: 10/15/2025
ms.topic: how-to
---

# Set up the device lifecycle agent

The Device Lifecycle Agent helps IT admins offboard devices securely and efficiently across Microsoft Intune, Microsoft Entra ID, Microsoft Defender, Autopilot, and Apple Business Manager. It analyzes device signals from multiple sources to identify stale or misaligned devices and provides actionable offboarding recommendations. Device Lifecycle Agent complements existing Intune automation by surfacing insights and handling ambiguous cases where automated cleanup may not suffice. All actions require admin approval. 

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune admin roles:
> - Intune Administrator
> - Read Only Operator
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra admin roles:
> - Security Reader
>
> For initial setup:
> - Copilot Owner required for setup
>
> For results:
> - Copilot Contributor 
>
> To take action from within the agent, such as to disable devices in Entra, you must have the *Disable devices* in Entra permission. You don't need this permission to set up, run, or view results from the agent.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
> - Microsoft Intune subscription (Plan 1 or equivalent). 
> - Microsoft Security Copilot access with sufficient security compute units (SCUs). 
> - Microsoft Entra ID integrated with Intune (Free or P1). 
> - Optional: Microsoft Defender for Endpoint (Plan 2) for Defender offboarding steps. 

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.

:::column-end:::
:::row-end:::
 

## Agent identity 

By default, the device lifecycle agent runs under the identity and permissions of the admin account that is used to set up the agent.  

The agent behavior is limited to the permissions of the user identity that the agent runs under. 

The agent persistently runs in the identity and permissions of the Intune admin account that is assigned as the agent's identity. 

The agent identity refreshes with each agent run and expires if the agent doesn't run for 90 consecutive days. When the expiration date nears, each Copilot owner and Copilot contributor receives a warning banner about renewal of the agent identity when they view the agent overview page. If the agent authentication expires, subsequent agent runs fail until authentication is renewed. For more information about renewing authentication, see [Renew the agent](#renew-the-agent). 

Agent identity: the agent runs using the identity of the user who first set up the agent. Agent authentication expires after 90 days and needs to be renewed. Learn more about agent authentication.

## Limitations 

- An admin must manually start the agent. Once the agent starts, there are no options to stop or pause it. 
- Only start the agent from within the Microsoft Intune admin center. 
- Only the user who sets up the agent can view session details in the Microsoft Security Copilot portal. 
- No suggestion history across runs. If you re-run the agent, the suggestions from the previous runs will be lost.  
- One agent instance per tenant/user context. 
- Only disables Entra ID objects; other remediation steps are instructions for admins. 

## How it works 

Signal Aggregation: Collects device data from Intune and Entra ID. 

Evaluation: Assesses devices using predefined logic and optional custom admin instructions. 

Recommendations: Flags devices for offboarding, with suggested actions and rationale. 

Admin Approval: No changes are made without explicit admin approval. 

Assisted Remediation: Upon approval, Device Lifecycle Agent disables Entra ID objects and guides further steps (e.g., Defender offboarding). 

<!--
Workspace: This agent will run in the same preferred workspace you selected for Security Copilot.
Once started, the agent will immediately run in your tenant. You will not be able to cancel an agent mid-run. When the run finishes, you can choose to [remove the agent](#remove-the-agent).

Select **Start agent** to begin the setup process.-->


## Supported Platforms & Scope 

Supports Windows, iOS/iPadOS, macOS, Android, and Linux devices managed by Intune. 

Both corporate-owned and BYOD devices are included. 

Excluded: Shared devices, hybrid Azure AD-joined Windows devices, Teams Phones 

## Configure the agent

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent**.

## Agent action: run

To manually run the Device Lifecycle Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Lifecycle Agent (preview)**.
1. Select **Run**.  

When an agent run starts, the agent runs until it completes its evaluation. It can't be stopped or paused. 

> [!NOTE]
> Each time the agent runs, it runs under the identity and permissions of the Intune administrator that its been configured to use. 

## Agent action: refresh

<!--##remove-->
[!INCLUDE [remove](includes/remove.md)]

## Use the agent

```agent-prompt
Find all devices that were removed from Intune but might still exist in Microsoft Entra. Provide steps to properly remove them from Entra.
```

```agent-response
Summary
There are 23 devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Users accessing corporate apps without MDM enrollment.
- Cannot enforce compliance policies or data protection.
- Personal devices may have corporate data without proper controls.
- Conditional access limited to user-based policies only.
```

<!--##renew-->

[!INCLUDE [renew](includes/renew.md)]

## Device Lifecycle Agent logs 

All agent management, create, delete, run, and any permission failures are available in Security Copilot logs. Logging of which devices were offboarded or when a recommended actions were complete aren't available. Instead, use the options to mark a suggestion as complete.  

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431