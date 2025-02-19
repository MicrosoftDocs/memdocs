---
title: Reset and wipe Education devices
description: Learn about the reset and wipe options for Windows devices using Intune for Education, including scenarios when to delete devices.
ms.date: 5/2/2024
ms.topic: tutorial
zone_pivot_groups: platforms-windows-ios
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
ms.service: microsoft-intune
ms.subservice: education
---

# Reset and wipe devices

## Device reset options

There are different scenarios that require a device to be reset, for example:

- The device isn't responding to commands.
- The device is lost or stolen.
- It's the end of the life of the device.
- It's the end of the school year and you want to prepare the device for a new school year.
- The device has hardware problems and you want to send it to the service center.

:::image type="content" source="./images/retire.png" alt-text="The device lifecycle for Intune-managed devices - retirement" border="false":::

Intune provides reset functionalities that enable IT administrators to remotely execute them:
::: zone pivot="windows"

- **Factory reset** (also known as **wipe**) is used to wipe all data and settings from the device, returning it to the default factory settings.
- **Autopilot reset** is used to return the device to a fully configured or known IT-approved state.

::: zone-end

::: zone pivot="ios"

- **Factory reset** (also known as **wipe**) is used to wipe all data and settings from the device, returning it to the default factory settings.

::: zone-end

### Factory reset (wipe)

✅ Return a device to original settings

A factory reset, or a wipe, reverts a device to the original settings when it was purchased. All settings, applications, and data installed on the device after purchase are removed. By default, the device is also removed from Intune management.

Once the wipe is completed, the device is in out-of-box experience.

#### [Intune](#tab/intune)

Here are the steps to perform a factory reset from Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **All devices**.
1. Select the device you want to reset.
1. Select **Wipe** and follow the instructions.
1. Select **Wipe** to confirm the action.

#### [Intune For Education](#tab/intune-for-education)

Here are the steps to perform a factory reset from Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Devices**.
1. Select the device you want to reset > **Factory reset**.
1. Select **Factory reset** to confirm the action.

---

::: zone pivot="windows"
:::image type="content" source="./images/win11-wipe.png" alt-text="Three screenshots showing the device being wiped, ending up in OOBE" lightbox="./images/win11-wipe.png" border="false":::
::: zone-end

Consider using factory reset in the following example scenarios:

- The device isn't working properly.
- It's the end of school year and you want to prepare the device for a new school year.
- You need to reassign the device to a different student, and you want to reset the device to its original settings.
- You're returning a device to the service center, and you want to remove all data and settings from the device.

::: zone pivot="windows"

> [!TIP]
> Consider that once the device is wiped, the new user will go through OOBE. This option may be ideal if the device is also registered in Autopilot to make the OOBE experience seamless, or if you plan to use a provisioning package to re-enroll the device.

### Autopilot Reset

✅ Return a device to original settings but maintain enrollment

Autopilot Reset is ideal when all data on a device needs to be wiped, but the device remains enrolled in your tenant.

Once the Autopilot reset action is completed, the device asks to chose region and keyboard layout, then it displays the sign-in screen.

#### [Intune](#tab/intune)

Here are the steps to perform an Autopilot reset from Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **All devices**.
1. Select the device you want to reset.
1. Select **Autopilot Reset** and follow the instructions.
1. Select **Yes** to confirm the action.

#### [Intune For Education](#tab/intune-for-education)

Here are the steps to perform an Autopilot reset from Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Devices**.
1. Select the device you want to reset > **Autopilot reset**.
1. Select **Autopilot reset** to confirm the action.

---

:::image type="content" source="./images/win11-autopilot-reset.png" alt-text="Three screenshots showing the device being wiped, ending up in the login screen" border="false":::

Consider using Autopilot reset in the following example scenarios:

- The device isn't working properly, and you want to reset it without reimaging it.
- It's the end of school year and you want to prepare the device for a new school year.
- You need to reassign the device to a different student, and you want to reset the device to without requiring the student to go through OOBE.

> [!TIP]
> Consider that the end user will **not** go through OOBE, and the association of the user to  the device in Intune doesn't change. For this reason, this option may be ideal for devices that have been enrolled in Intune as *shared devices* (for example, a device that was enrolled with a provisioning package or using Autopilot self-deploying mode).

::: zone-end

## Wiping and deleting a device

✅ Wipe and remove a device from management

There are scenarios that require a device to be deleted from your tenant, for example:

- The device is lost or stolen (for iOS devices, you may consider using [Lost Mode](/mem/intune/remote-actions/device-lost-mode) instead).
- It's the end of the life of the device.
- The device is replaced or has a new hardware components.

> [!IMPORTANT]
> The following actions should only be performed for devices that are no longer going to be used in your tenant.

 To completely remove a device, you need to perform the following actions:

::: zone pivot="windows"

1. If possible, perform a **factory reset (wipe)** of the device. If the device can't be wiped, delete the device from Intune using [these steps][MEM-1].
1. If the device is registered in Autopilot, delete the Autopilot object using [these steps][MEM-2].
1. Delete the device from Microsoft Entra ID using [these steps][MEM-3].

::: zone-end

::: zone pivot="ios"

1. If possible, perform a **factory reset (wipe)** of the device. If the device can't be wiped, delete the device from Intune using [these steps][MEM-1].
1. Delete the device from Microsoft Entra ID using [these steps][MEM-3].

::: zone-end

________________________________________________________

> [!div class="nextstepaction"]
> [Next: Troubleshoot and get help >](troubleshoot-overview.md)

<!-- Reference links in article -->

[MEM-1]: /mem/intune/remote-actions/devices-wipe#delete-devices-from-the-intune-portal
[MEM-2]: /mem/intune/remote-actions/devices-wipe#delete-devices-from-the-intune-portal
[MEM-3]: /mem/intune/remote-actions/devices-wipe#delete-devices-from-the-azure-active-directory-portal
