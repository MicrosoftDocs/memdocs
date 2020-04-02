---
title: Monitor Linux/UNIX clients
titleSuffix: Configuration Manager
description: Monitor clients on Linux and UNIX servers in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# How to monitor clients for Linux and UNIX servers in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!Important]  
> Starting in version 1902, Configuration Manager doesn't support Linux or UNIX clients. 
> 
> Consider Microsoft Azure Management for managing Linux servers. Azure solutions have extensive Linux support that in most cases exceed Configuration Manager functionality, including end-to-end patch management for Linux.

You can view information from Linux and UNIX servers in the Configuration Manager console using the same methods you use to view information from Windows-based clients.  

 The information you can view includes:  

- Status details from clients, in the Configuration Manager console dashboards  

- Details about clients in the default Configuration Manager reports  

- Inventory details in the Resource Explorer  

  The following sections describe how to get these details from the resource explorer and reports.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Use resource explorer to view inventory for Linux and UNIX servers  

 After a Configuration Manager client submits hardware inventory to the Configuration Manager site, you can use Resource Explorer to view this information. The Configuration Manager client for Linux and UNIX doesn't add new classes or views for inventory to the Resource Explorer. The Linux and UNIX inventory data maps to existing WMI classes. You can view the inventory details for your Linux and UNIX servers in the Windows-based classifications using Resource Explorer.  

 For example, you can collect the list of all natively installed programs found on your Linux and UNIX servers. Examples of natively installed programs include **.rpms** in Linux or **.pkgs** in Solaris. After inventory has been submitted by a Linux or UNIX client, you can view the list of all the natively installed Linux or UNIX programs in Resource Explorer in the Configuration Manager console.  

 For information about how to use Resource Explorer, see [How to use Resource Explorer to view hardware inventory](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> How to use Reports to View Information for Linux and UNIX Servers  
 Reports for Configuration Manager include information from Linux and UNIX servers along with information from Windows-based computers. No additional configurations are required to integrate the Linux and UNIX data in the reports.  

 For example, if you run the report named Count of Operating System Versions, it displays the list of the different operating systems and the number of clients that are running each operating system. The report is based on the hardware inventory information that was sent by the different Configuration Manager clients that run on the different operating systems.  

 It's also possible to create custom reports that are specific to Linux and UNIX server data. The **Caption** property of the hardware inventory class **Operating System** is a useful attribute that you can use to identify specific Operating Systems in the report query.  

 For information about reports in Configuration Manager, see [Introduction to reporting](/configmgr/core/servers/manage/introduction-to-reporting).  
