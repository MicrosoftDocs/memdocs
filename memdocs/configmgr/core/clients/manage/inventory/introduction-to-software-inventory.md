---
title: Software inventory
titleSuffix: Configuration Manager
description: Get an introduction to software inventory in Configuration Manager.
ms.date: 04/29/2019
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Introduction to software inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use software inventory to collect information about files on client devices. Software inventory can also collect files from client devices and store them on the site server. Software inventory is collected when you select the **Enable software inventory on clients** setting in client settings. You can also schedule the operation in client settings.  

After you enable software inventory and the clients run a software inventory cycle, the client sends the information to a management point in the client's site. The management point then forwards the inventory information to the Configuration Manager site server, which stores the information in the site database.

 There are a few ways to view software inventory data:  

- [Create queries](../../../../core/servers/manage/create-queries.md) that return devices with specified files.   

- Create [query-based collections](../../../../core/clients/manage/collections/introduction-to-collections.md) that include devices with specified files.   

- [Run reports](../../../servers/manage/introduction-to-reporting.md) that provide details about files on devices.

- Use [Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) to examine detailed information about the files that were inventoried and collected from client devices.   

 When software inventory runs on a client device, the first report is a full inventory. Subsequent reports contain only delta inventory information. The site server processes delta information in the order received. If delta information for a client is missing, the site server rejects further delta information and directs the client to run a full inventory.  

 Configuration Manager can discover dual-boot computers but only returns inventory information from the operating system that's active at the time of inventory.  
