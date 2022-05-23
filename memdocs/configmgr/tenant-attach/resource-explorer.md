---
title: Tenant attach - Resource explorer the admin center
titleSuffix: Configuration Manager
description: View hardware inventory for uploaded Configuration Manager devices using resource explorer in the admin center.
ms.date: 01/25/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# <a name="bkmk_hinv"></a> Tenant attach: Resource explorer in the admin center
<!--cm 6479284 in 7220536 pubpreview Sept 8, 2020, GA 2201-->
*Applies to: Configuration Manager (current branch)*

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. From the Microsoft Endpoint Management admin center, you can view hardware inventory for uploaded Configuration Manager devices by using resource explorer.

   :::image type="content" source="media/6479284-resource-explorer.png" alt-text="Resource explorer in Microsoft Endpoint Manager admin center" lightbox="media/6479284-resource-explorer.png":::

## Prerequisites

The following items are required to use resource explorer from the admin center:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md).
- A minimum of Configuration Manager version 2006 and the corresponding version of the console installed.
   - Historical inventory data requires Configuration Manager version 2103, or later. 
- Upgrade the target devices to the latest version of the Configuration Manager client.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read Resource** permission for the device's **Collection** in Configuration Manager.
- An [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned to the user <!--7980141-->

## <a name="bkmk_launch"></a> Launch resource explorer

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Resource explorer** to view hardware inventory.
1. Search for or select a class to retrieve information from the client.

   :::image type="content" source="media/6479284-resource-explorer-details.png" alt-text="Resource explorer with the motherboard class selected" lightbox="media/6479284-resource-explorer-details.png":::

## <a name="bkmk_historical"></a> Historical inventory data in resource explorer
<!--9546584, June 2021-->

*Applies to Configuration Manager 2103, or later*

Resource explorer can display a historical view of the device inventory in the Microsoft Endpoint Manager admin center. When troubleshooting, having historical inventory data can provide valuable information about changes to the device.

1. From the Microsoft Endpoint Manager admin center, select **Resource explorer**.
1. Select a class.
1. Enter a custom date in the date time picker to get historical inventory data.

:::image type="content" source="./media/9546584-resource-explorer-historical-inventory.png" alt-text="Screenshot of choosing a date from Resource explorer in the Microsoft Endpoint Manager admin center " lightbox="./media/9546584-resource-explorer-historical-inventory.png":::
## Close resource explorer

To close resource explorer and return to the device information, use the `X` icon in the top right of resource explorer.

   :::image type="content" source="media/6479284-close-resource-explorer.png" alt-text="Close resource explorer with the x icon in Microsoft Endpoint Manager admin center" lightbox="media/6479284-close-resource-explorer.png":::

## Next steps

[Troubleshoot resource explorer](troubleshoot-resource-explorer.md)