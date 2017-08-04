---
title: "Remote control prerequisites | Microsoft Docs"
description: "Get the prerequisites for remote control in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe

---
# Prerequisites for remote control in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Remote control in System Center Configuration Manager has external dependencies and dependencies in the product.  

## Dependencies external to Configuration Manager  

|Dependency|More information|  
|----------------|----------------------|  
|Computer video card driver|Ensure that the most up-to-date video driver is installed on client computers to ensure optimal remote control performance.|  

 Devices that run Windows Embedded, Windows Embedded for Point of Service (POS), and Windows Fundamentals for Legacy PCs do not support the remote control viewer, but they do support the remote control client.  

 Configuration Manager remote control cannot be used to remotely administer client computers that run Systems Management Server 2003 or Configuration Manager 2007.  

> [!NOTE]  
>  No Windows services are required as an external dependency for remote control.  

### Supported operating systems for the remote control viewer  
The remote control viewer is supported on all operating systems that are supported for the Configuration Manager console. For information , see [Supported configurations for System Center Configuration Manager consoles](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## Configuration Manager dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Remote control must be enabled for clients|By default, remote control is not enabled when you install Configuration Manager. For information about how to enable and configure remote control, see [Configuring remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Reporting services point|The reporting services point site system role must be installed before you can run reports for remote control. For more information, see [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Security permissions to manage remote control|To access collection resources and to initiate a remote control session from the Configuration Manager console: **Read**, **Read Resource**, and **Remote Control** permission for the **Collection** object.<br /><br /> The **Remote Tools Operator** security role includes these permissions that are required to manage remote control in Configuration Manager.<br /><br /> For more information, see [Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Additionally, you must add users whom you want to give permission to use remote control and remote assistance to the remote control permitted views list by using the option **Permitted viewers of Remote Control and Remote Assistance** in the **Remote Tools** client settings.|  
