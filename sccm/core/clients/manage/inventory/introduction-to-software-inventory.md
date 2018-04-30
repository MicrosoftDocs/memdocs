---
title: "Software inventory"
titleSuffix: "Configuration Manager"
description: "Get an introduction to software inventory in System Center Configuration Manager."
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Introduction to software inventory in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use software inventory to collect information about files on client devices. Software inventory can also collect files from client devices and store them on the site server. Software inventory is collected when you choose the **Enable software inventory on clients** setting in client settings, where you can also schedule the operation.  

After software inventory is enabled and the clients run a software inventory cycle, the client sends the information to a management point in the client's site. The management point then forwards the inventory information to the Configuration Manager site server, which stores the information in the site database.   

 Here are ways to view the software inventory data:  

-   [Create queries](../../../../core/servers/manage/queries-technical-reference.md) that return devices with specified files.   

-   Create [query-based collections](../../../../core/clients/manage/collections/introduction-to-collections.md) that include devices with specified files.   

-   [Run reports](../../../../core/servers/manage/reporting.md) that provide details about files on devices.

-   Use [Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) to examine detailed information about the files that were inventoried and collected from client devices.   

 When software inventory runs on a client device, the first report is a full inventory. Subsequent  reports contain only delta inventory information. The site server processes delta information in the order received. If delta information for a client is missing, the site server rejects further delta information and instructs the client to run a full inventory.  

 Configuration Manager can discover dual-boot computers but only returns inventory information from the operating system that was active at the time of inventory.  

**Mobile Devices:** See [software inventory for mobile devices enrolled with Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md)  for information about collecting inventory for apps installed on mobile devices.
