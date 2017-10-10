---
title: "Prerequisites for power management"
description: "Get the prerequisites for power management in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98ms.author: angrobemanager: angrobe

---
# Prerequisites for power management in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Power management in System Center Configuration Manager has external dependencies and dependencies within the product.  

## Dependencies external to Configuration Manager  
 The following table lists the dependencies external to Configuration Manager for using power management.  

|Dependency|More information|  
|----------------|----------------------|  
|Client computers must be able to support the required power states|To use all features of power management, client computers must be able to support the sleep, hibernate, wake from sleep, and wake from hibernate actions. You can use the **Power Capabilities** report to determine if computers can support these actions. For more information, see [Power Capabilities report](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) in the topic [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## Configuration Manager dependencies  
 The following table lists the dependencies within Configuration Manager for using power management.  

|Dependency|More Information|  
|----------------|----------------------|  
|Power management must be enabled before you can create and monitor power plans.|For information about how to enable and configure power management, see [Configuring power management in System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Reporting services point|You must configure a reporting services point before you can view power management reports. For more information, see [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
