---
title: Inventory Views
titleSuffix: Configuration Manager
description: Hardware and software inventory information about the clients, files, and products, in the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4487dbcb-1652-454f-8c45-3f543db1ad50
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Inventory Views in Configuration Manager

Inventory views contain hardware and software inventory information about the clients, files, products, and so forth in the Configuration Manager hierarchy. Configuration Manager collects inventory data when you enable the Hardware Inventory Client Agent or Software Inventory Client Agent. Because you can configure which hardware inventory to collect during the hardware inventory scan cycle and which file types to scan for during the software inventory scan cycle, each site will have a unique set of inventory that is collected.

For each Configuration Manager site, it is possible to retrieve a list of the hardware and software inventory schema to determine exactly what is inventoried. The topics in this section provide examples of how to do this for hardware and software inventory, as well as detailed information about the typical Configuration Manager SQL views.

## In This Section

- [Hardware Inventory Views in Configuration Manager](hardware-inventory-views-configuration-manager.md)

- [Software Inventory Views in Configuration Manager](software-inventory-views-configuration-manager.md)

- [Asset Intelligence Views in Configuration Manager](asset-intelligence-views-configuration-manager.md)

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)