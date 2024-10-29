---
title: Prerequisites for power management
titleSuffix: Configuration Manager
description: Get the prerequisites for power management in Configuration Manager.
ms.date: 10/06/2016
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Prerequisites for power management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Power management in Configuration Manager has external dependencies and dependencies within the product.  

## Dependencies external to Configuration Manager  
 The following table lists the dependencies external to Configuration Manager for using power management.  

|Dependency|More information|  
|----------------|----------------------|  
|Client computers must be able to support the required power states|To use all features of power management, client computers must be able to support the sleep, hibernate, wake from sleep, and wake from hibernate actions. You can use the **Power Capabilities** report to determine if computers can support these actions. For more information, see [Power Capabilities report](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) in the topic [How to monitor and plan for power management](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## Configuration Manager dependencies  
 The following table lists the dependencies within Configuration Manager for using power management.  

|Dependency|More Information|  
|----------------|----------------------|  
|Power management must be enabled before you can create and monitor power plans.|For information about how to enable and configure power management, see [Configuring power management](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Reporting services point|You must configure a reporting services point before you can view power management reports. For more information, see [Introduction to reporting](../../../servers/manage/introduction-to-reporting.md).|  
