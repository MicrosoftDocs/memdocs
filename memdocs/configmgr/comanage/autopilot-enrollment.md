---
title: How to enroll with Autopilot
titleSuffix: Configuration Manager
description: Enable clients to enroll with co-management when they provision with Windows Autopilot.
ms.date: 09/03/2021
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to enroll with Autopilot

<!-- Intune 5637106 -->

When you use [Windows Autopilot](../../autopilot/windows-autopilot.md) to provision a device, it first enrolls to Azure Active Directory (Azure AD) and Microsoft Intune. If the intended end-state of the device is co-management, previously this experience was difficult because of component timing and policy delays.

Now you can configure device enrollment in Intune to enable co-management, which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

You no longer need to create and assign an Intune app to install the Configuration Manager client. The Intune enrollment policy automatically installs the Configuration Manager client as a first-party app. The device gets the client content from the Configuration Manager cloud management gateway, so you don't need to provide and manage the client content in Intune. You do still specify the command-line parameters. This list can optionally include the [PROVISIONTS property](../core/clients/deploy/about-client-installation-properties.md#provisionts) to specify a task sequence.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../../intune/enrollment/windows-enrollment-status.md), the device waits for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

## Requirements

The following components are required to support Autopilot into co-management:

- Windows devices running one of the following versions:

  - Windows 10 version 20H2 with the latest cumulative update, or later

  - Windows 11

- Register the device for Autopilot. For more information, see [Windows Autopilot registration overview](../../autopilot/registration-overview.md).

  - Azure AD-joined only

  - User-driven scenario only

- Configuration Manager version 2010 or later

  - Set up a cloud management gateway. For more information, see [Cloud management gateway overview](../core/clients/manage/cmg/overview.md).

  - Enable co-management with automatic enrollment into Intune for **All** devices.<!-- or does pilot limitation refer to workloads? --> For more information, see [How to enable co-management](how-to-enable.md).

## Limitations

Autopilot into co-management currently doesn't support the following functionality:

- Hybrid Azure AD-joined devices

- Autopilot preprovisioning, also known as _white glove_ provisioning

- It's not supported with this scenario to enable co-management for automatic enrollment into Intune as a **Pilot**.<!-- or does pilot limitation refer to workloads? -->

## Configure

Use the following process to configure the co-management policy in Intune:

1. Go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
1. Select the **Devices** menu, select **Enroll devices**, and then select **Windows enrollment**.
1. Select **Co-management settings**, and then select **Create**.
1. Select **Yes** to automatically install the Configuration Manager client.
1. Specify the client installation command-line parameters. You can copy these parameters from the co-management properties page.

:::image type="content" source="media/intune-comanage-settings.png" alt-text="Co-management settings in Microsoft Intune.":::

<!-- what are specific next steps? save, assign -->

By default, the device waits for and uses the workload assignments from the Configuration Manager co-management policy. In the **Advanced** area of this policy, you can select **Yes** to override the co-management policy and use Intune for all workloads.<!-- why? -->

## Next steps

<!-- what's bigger next step(s)? -->
