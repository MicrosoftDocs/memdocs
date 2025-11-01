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

The Device Offboarding Agent helps IT admins remove devices from Microsoft Entra ID. It analyzes signals from Microsoft Intune and Entra ID to identify stale or misaligned devices and provides actionable recommendations for offboarding. This agent complements Intune's automation by surfacing insights and addressing ambiguous cases where automated cleanup might not be sufficient.

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
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]

:::column-end:::
:::column span="3":::
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions.
>
> The Device Offboarding Agent requires the following plugins:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
> - [!INCLUDE [plugin-entra](includes/plugin-entra.md)]
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
> For detailed guidance, see:
> - [Configure the Device Offboarding Agent](device-offboarding-agent-configure.md)
> - [Use the Device Offboarding Agent](device-offboarding-agent-use.md)

:::column-end:::
:::row-end:::

## How it works

The Device Offboarding Agent begins by aggregating signals from Microsoft Intune and Microsoft Entra ID. These signals include device status, alignment indicators, and other metadata that help determine whether a device is active, stale, or misconfigured.

Next, the agent evaluates each device using predefined logic and any optional custom instructions provided by admins. Based on this assessment, it generates recommendations that flag devices for offboarding, along with suggested actions and the rationale behind them.

>[!NOTE]
> The Device Offboarding Agent rusn in the same preferred workspace you selected for Security Copilot.

### Agent identity

The Device Offboarding Agent runs under the identity and permissions of the Intune admin account used during setup. Its actions are limited to the permissions of that account, and the identity refreshes with each run. If the agent doesn't run for 90 consecutive days, its authentication expires, and subsequent runs fail until renewed. To maintain functionality, renew the agent identity before the 90-day limit.

For more information about renewing authentication, see [Renew the agent](device-offboarding-agent-configure.md#renew-the-agent). 

## Operational considerations

Before running the Device Offboarding Agent, keep these points in mind:

- An admin must manually start the agent. After starting, there's no option to stop or pause it.
- The agent can only be started from the Microsoft Intune admin center.
- Session details in the [Microsoft Security Copilot portal][COP-PORTAL] are visible only to the user who set up the agent.
- Suggestions don't persist across runs; re-running the agent clears previous recommendations.
- Only one agent instance is supported per tenant/user context.
- The agent disables Entra ID objects; other remediation steps are provided as instructions for admins.

## Next steps

- [Configure the Device Offboarding Agent](device-offboarding-agent-configure.md)
- [Use the Device Offboarding Agent](device-offboarding-agent-use.md)

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[COP-PORTAL]: https://go.microsoft.com/fwlink/?linkid=2247989