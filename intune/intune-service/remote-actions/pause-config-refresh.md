---
title: "Intune Remote Actions: Pause Config Refresh"
description: Learn how to temporarily pause policy enforcement on Windows 11 devices using Intune's Pause Config Refresh remote action to support troubleshooting and manual changes.
ms.date: 08/27/2025
ms.topic: how-to
ms.reviewer: Mike Danoski
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Pause Config Refresh using Intune

Use the **Pause Config Refresh** remote action in Microsoft Intune to temporarily suspend automatic policy enforcement on Windows 11 devices. This action is helpful when you need to troubleshoot, perform maintenance, or apply manual changes that shouldn't be overwritten by Intune policies.

**Config Refresh** is a Windows feature that periodically reapplies policy settings to ensure devices stay compliant with your defined configurations. IT admins can configure the refresh cadence to run as frequently as every 30 minutes or as infrequently as once every 24 hours (1,440 minutes).

With the **Pause Config Refresh** action, IT admins can suspend policy refresh for a specified duration—up to 1,440 minutes. After the pause period ends, Config Refresh resumes automatically.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows 11

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Intune Administrator][ENT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Run Pause Configuration Refresh**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### :::image type="icon" source="../media/icons/headers/config.svg" border="false"::: Device configuration

> [!div class="checklist"]
> For users to receive notifications, the following requirements must be met:
>
> - Devices must have Config Refresh enabled for this remote action to take effect.

To learn more, see [Config Refresh][LEARN-1].

## How to pause Config Refresh from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Pause Config Refresh**.
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
[LEARN-1]: /windows/security/book/operating-system-security-system-security#-config-refresh)

