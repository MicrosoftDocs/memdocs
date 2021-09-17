---
title: Collections prerequisites
titleSuffix: Configuration Manager
description: Get prerequisites for using collections in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---
# Prerequisites for collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Collections in Configuration Manager contain only dependencies within the product.  

## Configuration Manager dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Reporting services point|The reporting services point site system role must be installed before you can run reports for collections. For more information, see [Introduction to reporting](../../../servers/manage/introduction-to-reporting.md).|  
|Specific security permissions must have been granted to manage collections|You must have the following security permissions to manage compliance settings:<br /><br /> - To create and manage collections: **Create**, **Delete**, **Modify**, **Modify Folder**, **Move Object**, **Read** and **Read Resource** for the **Collection** Object.<br /><br /> - To manage collection settings: **Modify Collection Setting** for the **Collection** Object.<br /><br /> The **Modify Folder** permission is required for all collection folders, including the root folder.|  
