---
title: "Collections prerequisites"
titleSuffix: "Configuration Manager"
description: "Get prerequisites for using collections in System Center Configuration Manager."
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Prerequisites for collections in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Collections in System Center Configuration Manager contain only dependencies within the product.  

## Configuration Manager dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Reporting services point|The reporting services point site system role must be installed before you can run reports for collections. For more information, see [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Specific security permissions must have been granted to manage collections|You must have the following security permissions to manage compliance settings:<br /><br /> - To create and manage collections: **Create**, **Delete**, **Modify**, **Modify Folder**, **Move Object**, **Read** and **Read Resource** for the **Collection** Object.<br /><br /> - To manage collection settings: **Modify Collection Setting** for the **Collection** Object.<br /><br /> The **Modify Folder** permission is required for all collection folders, including the root folder.|  
