---
title: "Remote Device Action: Pause Config Refresh"
description: Learn how to temporarily pause policy enforcement on Windows 11 devices using Intune's Pause Config Refresh remote action to support troubleshooting and manual changes.
ms.date: 10/27/2025
ms.topic: how-to
ms.reviewer: Mike Danoski
---

# Remote device action: pause Config Refresh

Use the *pause Config Refresh* remote action in Microsoft Intune to temporarily suspend automatic policy enforcement on Windows 11 devices. This action is helpful when you need to troubleshoot, perform maintenance, or apply manual changes that shouldn't be overwritten by Intune policies.

Config Refresh is a Windows feature that periodically reapplies policy settings to ensure devices stay compliant with your defined configurations. IT admins can configure the refresh cadence to run as frequently as every 30 minutes or as infrequently as once every 24 hours (1,440 minutes).

With the pause Config Refresh action, IT admins can suspend policy refresh for a specified duration—up to 1,440 minutes. After the pause period ends, Config Refresh resumes automatically.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
>
> - Windows 11
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> [!div class="checklist"]
> To use this remote action, make sure devices meet the following requirements:
>
> - Config Refresh is enabled.

To learn more, see [Config Refresh][LEARN-1].

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this remote action, use an account with at least one of the following roles:
>
> - [Intune Administrator][ENT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Run Pause Configuration Refresh**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to pause Config Refresh from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Pause Config Refresh**.
1. Specify the number of minutes to pause Config Refresh in the **Time period to Pause Config Refresh**. The maximum is 1,440 minutes (24 hours).
1. Select **Pause**.

> [!Note]
> If Config Refresh is paused and you want to resume, then select **Pause** again for 0 minutes to resume Config Refresh enforcement.

## Reference links

- Microsoft Graph API: [pauseConfigurationRefresh action][GRAPH-1] in the Microsoft Graph API documentation.
- Configuration service provider (CSP) used to initiate the remote action: [DMClient CSP][CSP-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[GRAPH-1]: /graph/api/intune-devices-manageddevice-pauseconfigurationrefresh

[CSP-1]: /windows/client-management/mdm/dmclient-csp#deviceproviderprovideridconfigrefresh
[LEARN-1]: /windows/security/book/operating-system-security-system-security#-config-refresh

