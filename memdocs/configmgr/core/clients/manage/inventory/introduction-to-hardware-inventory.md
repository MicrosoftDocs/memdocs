---
title: Hardware inventory
titleSuffix: Configuration Manager
description: Understand the basics of hardware inventory in Configuration Manager.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: overview
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Introduction to hardware inventory

*Applies to: Configuration Manager (current branch)*

Use hardware inventory in Configuration Manager to collect information about the hardware configuration of client devices in your organization. To collect hardware inventory, you must select the **Enable hardware inventory on clients** setting in client settings.

After hardware inventory is enabled and the client runs a hardware inventory cycle, the client sends the information to a management point in the client's site. The management point then forwards the inventory information to the Configuration Manager site server, which stores the inventory information in the site database. Hardware inventory runs on clients according to the schedule that you specify in client settings.

## View hardware inventory

You can use several methods to view the hardware inventory data that Configuration Manager collects:

- [Create queries that return devices that are based on a specific hardware configuration](../../../servers/manage/introduction-to-queries.md).

- [Create query-based collections that are based on a specific hardware configuration](../collections/introduction-to-collections.md). Query-based collection memberships automatically update on a schedule. You can use collections for several tasks, including software deployment.

- [Run reports that display specific details about hardware configurations in your organization](../../../servers/manage/introduction-to-reporting.md).

- [Use Resource Explorer](use-resource-explorer-to-view-hardware-inventory.md) to view detailed information about the hardware inventory that's collected from client devices.

When hardware inventory runs on a client device, the first inventory data that the client returns is always a full inventory. The next set of inventory data contains only delta inventory information. The site server processes delta inventory information in the order received. If delta information for a client is missing, the site server rejects more delta information and directs the client to run a full inventory cycle.

Configuration Manager provides limited support for dual-boot computers. Configuration Manager can discover dual-boot computers but returns inventory information only from the OS that's active when the inventory cycle runs.

## Extend inventory

To collect more information than what Configuration Manager inventories by default, you can also use one of these methods to extend hardware inventory:

- Enable, disable, add, and remove inventory classes for hardware inventory from the Configuration Manager console.

- Use NOIDMIF files to collect information about client devices that can't be inventoried by Configuration Manager. For example, you might want to collect device asset number information that exists only as a label on the device. NOIDMIF inventory is automatically associated with the client device that it was collected from.

- Use IDMIF files to collect information about assets that aren't associated with a Configuration Manager client, for example, projectors, photocopiers, and network printers.

- Starting in version 2107, you can use the administration service to set custom properties on devices.<!--8939867--> You can then use the custom properties in Configuration Manager for reporting or to create collections. For more information, see [Custom properties for devices](../../../../develop/adminservice/custom-properties.md).

## Next steps

[How to configure hardware inventory](configure-hardware-inventory.md)
