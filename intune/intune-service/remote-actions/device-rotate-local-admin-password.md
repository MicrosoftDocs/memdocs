---
title: Rotate local admin password
description: Learn how to rotate the local admin password on Windows and macOS devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

Initiates a rotation for the local admin password on the device.

# Rotate local admin password

> [!div class="checklist"]
> To execute this remote action, you must use an account that has a [Custom role][INT-RC] with the permission:
>   - Remote tasks/Rotate Local Admin Password

## Reference links

- Microsoft Graph API: [rotatelocaladminpassword action][GRAPH-1]


<!--links-->

[more info](../protect/windows-laps-policy.md#manually-rotate-passwords)

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->


[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotatelocaladminpassword
