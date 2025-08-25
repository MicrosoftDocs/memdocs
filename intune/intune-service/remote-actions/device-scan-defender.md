---
# required metadata

title: "Intune Remote Actions: Full Scan and Quick Scan"
titleSuffix: Microsoft Intune
description: Learn how to initiate on demand Microsoft Defender full scans and quick scans with Microsoft Intune.
ms.date: 08/14/2025
ms.topic: how-to

ms.reviewer:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
AppliesTo:
  - ✅ Windows 10/11
---


# Full scan and quick scan with Microsoft Defender

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows 10/11


### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute these remote actions, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] with the permission:
>   - Remote tasks/Windows defender

## How to initiate a full scan or quick scan

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device, and then select **...** > **Quick scan** or **Full scan**.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [windowsDefenderScan action][GRAPH-1].

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-windowsdefenderscan


<!--to add link
/defender-endpoint/run-scan-microsoft-defender-antivirus#use-microsoft-intune-to-run-a-scan
-->
