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
> Feature update policies supports devices that are:
> - Enrolled in Intune
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> Devices must also meet the following requirements:
> - Telemetry must be turned on, with a minimum setting of [*Required*](../../intune-service/configuration/device-restrictions-windows-10.md#reporting-and-telemetry).
>    Devices that receive a feature updates policy and that have Telemetry set to *Not configured* (off), might install a later version of Windows than defined in the feature updates policy.
>
>    To configure Telemetry as using the Settings catalog:
> 
>    1. [Create a Settings catalog policy](/intune/intune-service/configuration/settings-catalog) for the Windows platform and use the following setting:
> 
>      | Category | Setting name | Value |
>      |--|--|--|
>      | **System** | Allow Telemetry | **Basic** or **Full** |
> 
>     1. Assign the policy to a group that contains as members the devices that you want to configure.
> 
> - The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.
> - Have access to endpoints. To get a detailed list of endpoints required for the associated services listed here, see [Network endpoints](../../intune-service/fundamentals/intune-endpoints.md#access-for-managed-devices).
>    - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)
>    - Windows Autopatch

:::column-end:::
:::row-end:::