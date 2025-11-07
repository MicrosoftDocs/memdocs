---
title: Get Started with the Device Offboarding Agent
description: Learn about the Device Offboarding Agent in Microsoft Intune, its prerequisites, how it works, and how to configure it.
ms.date: 10/15/2025
ms.topic: overview
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Get Started with the Device Offboarding Agent

The Device Offboarding Agent helps IT admins offboard devices securely and efficiently across Microsoft Intune, Microsoft Entra ID, Microsoft Defender, Autopilot, and Apple Business Manager. It analyzes device signals from multiple sources to identify stale or misaligned devices and provides actionable offboarding recommendations. Device Offboarding Agent complements existing Intune automation by surfacing insights and handling ambiguous cases where automated cleanup may not suffice. All actions require admin approval.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> The agent is supported on the public cloud only. It isn't supported on government clouds.

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
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]

:::column-end:::
:::column span="3":::
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions.
>
> The Device Offboarding Agent requires the following plugin:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
> <!--- [!INCLUDE [plugin-entra](includes/plugin-entra.md)]-->
>
> [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474).

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
> - Window corporate devices
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
> Role requirements vary based on whether you're configuring the agent or using it, and on the specific actions performed.
>
> ---
>
> To **enable and configure** the Device Offboarding Agent, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
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
> To take action from within the agent, such as to [disable devices in Entra](/entra/identity/devices/manage-stale-devices#disable-devices), you must have the *Disable devices* in Entra permission. You don't need this permission to run or view results from the agent.

:::column-end:::
:::row-end:::

## How it works

To support secure and efficient device lifecycle management, the Device Offboarding Agent performs a series of automated evaluations and actions. Here's a breakdown of its workflow:

:::row:::
:::column span="1":::
**1. Signal aggregation**
:::column-end:::
:::column span="3":::
>The Device Offboarding Agent begins by aggregating signals from Microsoft Intune and Microsoft Entra. These signals include  indicators, that help determine whether a device is active, stale, or misconfigured.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**2. Evaluation**
:::column-end:::
:::column span="3":::
>The agent evaluates each device using predefined logic and any optional [custom instructions](#configure-custom-instructions) provided by an admin.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**3. Recommendations**
:::column-end:::
:::column span="3":::
>Based on this assessment, the agent generates recommendations that flag devices for offboarding, along with suggested actions and the rationale behind them.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**4. Admin approval**
:::column-end:::
:::column span="3":::
>No changes are made to devices without explicit admin approval. The agent provides detailed recommendations, but the final decision to offboard a device rests with the IT admin.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**5. Assisted remediation**
:::column-end:::
:::column span="3":::
>Upon admin approval, the Device Offboarding Agent disables the corresponding Entra ID objects. It also facilitates the offboarding process by providing guidance on additional remediation steps, such as removing devices from Microsoft Defender or Apple Business Manager.
:::column-end:::
:::row-end:::

### Agent identity

The Device Offboarding Agent runs under the identity and permissions of the Intune admin account used during setup. Its actions are limited to the permissions of that account, and the identity refreshes with each run. If the agent doesn't run for 90 consecutive days, its authentication expires, and subsequent runs fail until renewed. To maintain functionality, [renew the agent](#renew-the-agent) identity before the 90-day limit.

### Operational considerations

Before running the Device Offboarding Agent, keep these points in mind:

- An admin must manually start the agent. After starting, there's no option to stop or pause it.
- The agent can only be started from the Microsoft Intune admin center.
- Session details in the [Microsoft Security Copilot portal][COP-PORTAL] are visible only to the user who set up the agent.
- Suggestions don't persist across runs; re-running the agent clears previous recommendations.
- Only one agent instance is supported per tenant/user context.
- The agent disables Entra ID objects; other remediation steps are provided as instructions for admins.

[!INCLUDE [enable](includes/enable.md)]

:::image type="content" source="images/device-offboarding-agent/set-up.png" alt-text="Screenshot of the setup pane of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/set-up.png":::

## Explore the agent options

After you configure the agent, you can manage it from the Device Offboarding Agent pane.

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

## Configure custom instructions

Use custom instructions to guide the agent's logic based on your organization's needs. Custom instructions help refine the agent's evaluation criteria, allowing you to include or exclude specific devices from offboarding recommendations.

These instructions can be used to: 

- Include or exclude specific object IDs.
- Set thresholds for device activity.

For example, if your organization has executive devices that you don't want to flag for offboarding, you can use custom instructions to exclude them. Without this exclusion, the agent might detect identity mismatches on those devices and consume SCUs to suggest offboarding—even when it's not appropriate. Custom instructions help you prevent that issue by guiding the agent's logic based on your organizational needs.

Custom instructions persist between agent runs, so once you set them, they are evaluated every time the agent runs. You can change custom instructions at any time in the **Settings** tab and re-run the agent. The **Factors** section in a suggestion highlights details on which custom instructions were taken into account while forming the list of suggested devices to offboard.  

To configure custom instructions:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select the **Settings** tab.
1. In the **Instructions** field, enter a prompt to customize the agent's evaluation criteria.
  - Setting thresholds for device activity

### Examples of custom instructions you can use

```agent-prompt
Exclude from all recommendations if device has been inactive in Entra for less than [n] days 
```
```agent-prompt
Include in all recommendations if device has been active in Entra more than [n] days ago 
```
```agent-prompt
Exclude [device ID] from all recommendations 
```
```agent-prompt
Exclude [device ID] from recommendation if retired is true 
```
```agent-prompt
Include [device ID] in all recommendations 
```
```agent-prompt
Include only [device ID] in recommendations
```

[!INCLUDE [renew](includes/renew.md)]

[!INCLUDE [remove](includes/remove.md)]

## Next steps

> [!div class="nextstepaction"]
> [Learn how to use the Device Offboarding Agent](device-offboarding-agent-use.md)

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[COP-PORTAL]: https://go.microsoft.com/fwlink/?linkid=2247989
