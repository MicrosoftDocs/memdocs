---
title: "Hardware inventory "
titleSuffix: "Configuration Manager"
description: "Get an introduction to hardware inventory in Configuration Manager."
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby


---
# Introduction to hardware inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use hardware inventory in Configuration Manager to collect information about the hardware configuration of client devices in your organization. To collect hardware inventory, you must select the **Enable hardware inventory on clients** setting in client settings.  

 After hardware inventory is enabled and the client runs a hardware inventory cycle, the client sends the information to a management point in the client's site. The management point then forwards the inventory information to the Configuration Manager site server, which stores the inventory information in the site database. Hardware inventory runs on clients according to the schedule that you specify in client settings.  
## View hardware inventory 

 You can use several methods to view the hardware inventory data that Configuration Manager collects, including these methods:  

- [Create queries that return devices that are based on a specific hardware configuration](../../../../core/servers/manage/introduction-to-queries.md).  

- [Create query-based collections that are based on a specific hardware configuration](../../../../core/clients/manage/collections/introduction-to-collections.md). Query-based collection memberships automatically update on a schedule. You can use collections for several tasks, including software deployment.

- [Run reports that display specific details about hardware configurations in your organization](../../../../core/servers/manage/reporting.md).

- [Use Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) to view detailed information about the hardware inventory that's collected from client devices.

When hardware inventory runs on a client device, the first inventory data that the client returns is always a full inventory. Subsequent inventory data contains only delta inventory information. The site server processes delta inventory information in the order received. If delta information for a client is missing, the site server rejects additional delta information and directs the client to run a full inventory cycle.  

 Configuration Manager provides limited support for dual-boot computers. Configuration Manager can discover dual-boot computers but returns inventory information only from the operating system that's active when the inventory cycle runs.  

> [!NOTE]  
>  For information about how to use hardware inventory with clients that run Linux and UNIX, see [Hardware inventory for Linux and UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## Extending Configuration Manager hardware inventory  
 In addition to the built-in hardware inventory in Configuration Manager, you can also use one of these methods to extend hardware inventory to collect more information:  

- Enable, disable, add and remove inventory classes for hardware inventory from the Configuration Manager console.  
- Use NOIDMIF files to collect information about client devices that can't be inventoried by Configuration Manager. For example, you might want to collect device asset number information that exists only as a label on the device. NOIDMIF inventory is automatically associated with the client device that it was collected from.  
- Use IDMIF files to collect information about assets that aren't associated with a Configuration Manager client, for example, projectors, photocopiers, and network printers.


## Next steps
For more information about using these methods to extend Configuration Manager hardware inventory, see [How to configure hardware inventory](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
