---
title: Get Started with the Device Offboarding Agent
description: Learn about the Device Offboarding Agent in Microsoft Intune, its prerequisites, how it works, and how to configure it.
ms.date: 10/15/2025
ms.topic: overview
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Get started with the Device Offboarding Agent

The *Device Offboarding Agent* identifies stale or misaligned devices across Intune and Entra ID, providing actionable insights and requiring admin approval before offboarding any devices. The Device Offboarding Agent complements existing Intune automation by surfacing insights and handling ambiguous cases where automated cleanup may not suffice.

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
> - Hybrid Entra-joined Windows devices
> - Windows Autopilot devices
> - Shared devices
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
> To **enable**, **configure**, and **delete** the Device Offboarding Agent, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles, either:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) 
> - [Custom role](/intune/intune-service/fundamentals/role-based-access-control#custom-roles) with **Audit data/Read** and **Organization/Read** permissions
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles, either:
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> - [Custom role](/entra/identity/role-based-access-control/custom-create) with **Microsoft.Directory/Devices/Standard/Read** permissions
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Security Copilot owner](/copilot/security/authentication#security-copilot-roles) 
>
> ---
>
> To **use** the agent and perform offboarding actions, use an account with at least the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles, either:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) 
> - [Custom role](/intune/intune-service/fundamentals/role-based-access-control#custom-roles) with **Audit data/Read** and **Organization/Read** permissions
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles, either:
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> - [Custom role](/entra/identity/role-based-access-control/custom-create) with **Microsoft.Directory/Devices/Standard/Read** permissions\
>     To take action from within the agent, such as to [disable devices in Entra](/entra/identity/devices/manage-stale-devices#disable-devices), you must have the **[Disable devices](/entra/identity/role-based-access-control/custom-device-permissions#enable-or-disable-devices)** permission. You don't need this permission to run or view results from the agent.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Security Copilot contributor](/copilot/security/authentication#security-copilot-roles)

:::column-end:::
:::row-end:::

## How it works

To support secure and efficient device lifecycle management, the Device Offboarding Agent performs a series of automated evaluations and actions. Here's a breakdown of its workflow:

:::row:::
:::column span="1":::
**1. Signal aggregation**

:::image type="icon" source="icons/signal-aggregation.svg" border="false":::
:::column-end:::
:::column span="3":::
>The Device Offboarding Agent begins by aggregating signals from Microsoft Intune and Microsoft Entra ID. These signals include  indicators, that help determine whether a device is active, stale, or misconfigured.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**2. Evaluation**

:::image type="icon" source="icons/evaluation.svg" border="false":::
:::column-end:::
:::column span="3":::
>The agent evaluates each device using predefined logic and any optional [custom instructions](#configure-custom-instructions) provided by an admin.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**3. Recommendations**

:::image type="icon" source="icons/recommendations.svg" border="false":::
:::column-end:::
:::column span="3":::
>Based on this assessment, the agent generates recommendations that flag devices for offboarding, along with suggested actions and the rationale behind them.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**4. Admin approval**

:::image type="icon" source="icons/approval.svg" border="false":::
:::column-end:::
:::column span="3":::
>No changes are made to devices without explicit admin approval. The agent provides detailed recommendations, but the final decision to offboard a device rests with the IT admin.
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
**5. Assisted remediation**

:::image type="icon" source="icons/remediation.svg" border="false":::
:::column-end:::
:::column span="3":::
>Upon admin approval, the Device Offboarding Agent disables the corresponding Entra ID objects. It also facilitates the offboarding process by providing guidance on additional remediation steps, such as removing devices from Microsoft Defender or Apple Business Manager.
:::column-end:::
:::row-end:::

### Agent identity

The Device Offboarding Agent runs under the identity and permissions of the Intune admin account used during setup. Its actions are limited to the permissions of that account, and the identity refreshes with each run. If the agent doesn't run for 90 consecutive days, its authentication expires, and subsequent runs fail until renewed. To maintain functionality, [renew the agent](#renew-the-agent) identity before the 90-day limit.

### Operational considerations

Before running the Device Offboarding Agent, note the following:

- Admins must start the agent manually; once launched, it cannot be paused or stopped.
- Admins can only launch the agent from the Microsoft Intune admin center.
- Only the admin who set up the agent can view session details in the [Microsoft Security Copilot portal][COP-PORTAL].
- The agent identifies devices that were retired, wiped, or deleted from Intune within the last 30 days.
- The agent limits results to the first 10,000 devices.
- Upon admin approval to offboard, the agent disables Entra ID objects. Other remediation steps are provided as instructions for admins.
- The agent doesn't persist suggestions across runs; re-running clears previous recommendations.
- Only one agent instance is supported per tenant.

>[!IMPORTANT]
>Data reported by the agent is surfaced through agent suggestions. This information may be visible to admins who have access to the agent in the Intune admin center, even if it includes data outside their assigned Administrative Units (AUs) in Microsoft Entra ID.

[!INCLUDE [enable](includes/enable.md)]

:::image type="content" source="images/device-offboarding-agent/set-up.png" alt-text="Screenshot of the setup pane of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/set-up.png":::

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

### Examples of custom instructions you can use

```agent-prompt
Exclude devices with IDs […]
```
```agent-prompt
Exclude devices with last activity after […]
```
```agent-prompt
Exclude devices with last activity before […]
```
```agent-prompt
Include only devices with IDs […]
```

>[!IMPORTANT]
>If you include one or more deviceIds and none of them have been retired, wiped, or deleted within the last 30 days, the agent will fail to run.

```agent-prompt
Include only devices with last activity after […]
```
```agent-prompt
Include only devices with last activity before […]
```

[!INCLUDE [renew-alternative](includes/renew-alternative.md)]

[!INCLUDE [remove](includes/remove.md)]

## Next steps

> [!div class="nextstepaction"]
> [Learn how to use the Device Offboarding Agent](device-offboarding-agent-use.md)

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[COP-PORTAL]: https://go.microsoft.com/fwlink/?linkid=2247989
