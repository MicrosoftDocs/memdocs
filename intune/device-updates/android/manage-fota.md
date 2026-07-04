---
title: Manage Android FOTA updates with Microsoft Intune
description: Use Microsoft Intune to manage firmware updates on Android devices. A FOTA update can include software and security patches, feature updates, and other changes to the device's firmware.
ms.date: 05/12/2026
ms.topic: how-to
ms.reviewer: jieyan
ms.subservice: suite
---

# Manage Firmware Over-the-Air updates on Android

Firmware Over-the-Air (FOTA) updates let you remotely update device firmware over a wireless connection. A FOTA update can include software and security patches, feature updates, and other changes to the device's firmware. This method is more efficient, convenient, and more secure than manual updates and can be performed on a scheduled or on-demand basis.

In the context of FOTA, a *deployment* is an update policy that includes instructions about the firmware update to be deployed to devices and other update-related settings. For example, Schedule type, and charging requirements.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> FOTA updates are supported on Android Enterprise devices enrolled in Intune. This includes the following enrollment types:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

>[!INCLUDE [additional-licensing-plan2](../../includes/licensing/additional-licensing-plan2.md)]
:::column-end:::
:::row-end:::

## Manage FOTA updates

You have two ways to manage software updates:

- Use Firmware Over-the-Air (FOTA), which works for some OEMs.

    > [!NOTE]
    > If Zebra updated the available firmware list in the last 24 hours, then the list of firmware available might take up to 24 hours to populate.

- If FOTA isn't available you can use Device restrictions profiles, which work for all OEMs.

### FOTA update management for specific OEMs

Manufacturer-specific FOTA support might offer more controls beyond what device restrictions profiles offer.

Intune supports FOTA update management for supported devices from the following manufacturers:

- **Zebra**: For Zebra devices, see [LifeGuard Over-the-Air Integration with Microsoft Intune](setup-zebra-lifeguard.md).
- **Samsung**: For Samsung devices, see [E-FOTA Update Management with Microsoft Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/samsung-e-fota-update-management-with-microsoft-endpoint-manager/ba-p/2002552).

### Use device restrictions profiles to manage FOTA updates

Device restrictions profiles offer control over how the device handles over-the-air updates and allow you to set a freeze period for these updates. A freeze period is a specified time frame during which over-the-air updates are blocked from being installed on the device. This can be useful for organizations that want to prevent updates from being installed during critical business periods or when devices are in use.

> [!NOTE]
> Not all device manufacturers support over-the-air updates.

To manage FOTA updates using device restrictions profiles:

1. In the [Microsoft Intune admin center], select [**Devices**] > **Android**.
1. Select **Manage devices** > **Configuration** > **Create** > **New policy**
1. Under **Platform**, select **Android Enterprise**.
1. Under **Policy type**, select **Templates**.
1. Under **Fully Managed, Dedicated, and Corporate-Owned Work Profile**, select **Device restrictions** > **Create**.
1. Configure the system update settings as needed. For more information about these settings, see [Device restrictions for Android Enterprise](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
