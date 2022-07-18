---
title: Surface Device Dashboard
titleSuffix: Configuration Manager
description: Review information about Surface devices using the dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/15/2021
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.localizationpriority: medium
---

# Surface device dashboard in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The Surface device dashboard gives you information about Surface devices found in your environment at a single glance.<!--1355788-->

## How to open

To open the Surface device dashboard, use the following steps:

1. Open the Configuration Manager console.
2. Select the **Monitoring** workspace.
3. To load the dashboard, select the **Surface Devices** node.

:::image type="content" source="media/Surface-device-dashboard.PNG" alt-text="An example view of the Surface device dashboard.":::

## Review information

The Surface device dashboard shows three graphs:

- **Percent of Surface devices**: The percentage of Surface devices throughout your environment.

    :::image type="content" source="media/Percent-Surface-Devices.PNG" alt-text="Percent of Surface devices graph.":::

- **Surface Models**: The number of devices per Surface model. Hover over a graph section to see the percentage of Surface devices for that model.

    :::image type="content" source="media/Surface-Models-Hover.PNG" alt-text="Surface models graph.":::

  - Select a graph section to go through to a device list for that model.

    :::image type="content" source="media/Surface-Model-Device-List.PNG" alt-text="Surface model device list.":::

- **Top five firmware versions**: The top five firmware models in your environment. Hover over a graph section to see the number of Surface devices with that firmware version. Select a graph section to go through to a device list.<!--1358654-->

    :::image type="content" source="media/Surface-Firmware-Hover.PNG" alt-text="Surface top five firmware versions graph.":::

## Next steps

You can use Configuration Manager to deploy Surface firmware updates. For more information, see [Managing Surface driver updates](../../../sum/deploy-use/surface-drivers.md).

For more information about Surface devices, see the [Surface](https://www.microsoft.com/surface) website.
