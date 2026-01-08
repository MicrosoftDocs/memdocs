---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 01/08/2026
---

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> This policy type supports devices that are:
>
> - Managed by Intune
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> Devices must also meet the following requirements:
> - Telemetry must be turned on, with a minimum setting of [*Required*](../../../intune-service/configuration/device-restrictions-windows-10.md#reporting-and-telemetry).
> - To support reporting on all status and events for driver updates, enable [Windows diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) collection on devices at the *Required* level or higher.
>   - For more information, see [Configure Windows diagnostic data collection](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-settings).
> - The *Microsoft Account Sign-In Assistant* service (`wlidsvc`) must be enabled and running.

:::column-end:::
:::row-end:::


<!--
>    To configure Telemetry as using the Settings catalog:
> 
>    1. [Create a Settings catalog policy](/intune/intune-service/configuration/settings-catalog) for the Windows platform and use the following setting:
> 
>      | Category | Setting name | Value |
>      |--|--|--|
>      | **System** | Allow Telemetry | **Basic** or **Full** |
> 
>     1. Assign the policy to a group that contains as members the devices that you want to configure.
-->