---
title: Updates in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about feature updates in Desktop Analytics.
ms.date: 04/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# Updates in Desktop Analytics

In the Desktop Analytics portal, view the status of feature updates. Select these nodes in the Monitor group of the Desktop Analytics main menu. These nodes give you insights into the status of these updates in your environment.

<!--7362999-->

> [!IMPORTANT]
> Desktop Analytics displays the feature update status for devices with the commercial ID associated with your Desktop Analytics workspace. This behavior happens whether or not you enrolled the devices with Configuration Manager. The number of total devices on these tiles may not match the number of enrolled devices in [**Connected Services**](monitor-connection-health.md#commercial-id-configuration).

## Feature updates

To review the current status of feature updates, select **Feature updates** in the **Monitor** section of Desktop Analytics:

:::image type="content" source="media/feature-updates.png" alt-text="Feature updates node of Desktop Analytics" lightbox="media/feature-updates.png":::

This view summarizes *feature* updates for devices that are running Windows 10.

For more information on service periods, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

### Categories

Devices in the bar chart are categorized by the following labels:

#### In service

Devices are running the latest feature update for that version and channel.  

#### Near end of service

Devices are running a feature update that's within 90 days of reaching end of service.

#### End of service

Devices are running a feature update that's past the end of service date. These dates are specific to Enterprise and Education editions of Windows. They don't apply to Home, Pro, Pro Education, or Pro for Workstations editions. For more information, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### Not measured

Desktop Analytics hasn't assessed the device. This state includes devices running Windows 7, Windows 8.1, or Windows 10 devices registered for the Windows Insider Program.

Select the tile to see the adoption trends for feature updates. The stacked area chart categorizes devices by the feature update they've installed over time.

## Next steps

- [Learn about Desktop Analytics assets](about-assets.md): devices, drivers, and apps  

- [Learn about deployment plans](about-deployment-plans.md)  

> [!IMPORTANT]
> Starting in March 2021, Desktop Analytics doesn't report on security updates.<!-- 8099536,9614078 --> To monitor your devices' Windows updates and Microsoft Defender status, use [Update Compliance](/windows/deployment/update/update-compliance-get-started).
