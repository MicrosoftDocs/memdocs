---
title: Inventory views
description: Hardware and software inventory information about the clients, files, and products, in the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.subservice: sdk
ms.topic: reference


ms.collection: tier3
---

# Inventory views in Configuration Manager

Inventory views contain hardware and software inventory information about the clients, files, products, and so forth, in the Configuration Manager hierarchy. Configuration Manager collects inventory data when you enable the Hardware Inventory Client Agent or Software Inventory Client Agent. Because you can configure which hardware inventory to collect during the hardware inventory scan cycle and which file types to scan for during the software inventory scan cycle, each site will have a unique set of inventory that is collected.

For each Configuration Manager site, it's possible to retrieve a list of the hardware and software inventory schema to determine exactly what is inventoried. The articles in this section provide examples of how to do get the hardware and software inventory lists, and detailed information about the typical Configuration Manager SQL views.

## In This Section

- [Hardware inventory views in Configuration Manager](hardware-inventory-views-configuration-manager.md)

- [Software inventory views in Configuration Manager](software-inventory-views-configuration-manager.md)

- [Asset intelligence views in Configuration Manager](asset-intelligence-views-configuration-manager.md)

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
