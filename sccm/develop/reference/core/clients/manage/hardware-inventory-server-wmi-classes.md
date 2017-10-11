---
title: "Hardware Inventory Server WMI Classes"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 2cc63027-0dbd-4842-933d-171ee66d7c0dsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Hardware Inventory Server WMI Classes
The System Center Configuration Manager hardware inventory server Windows Management Instrumentation (WMI) classes are generated dynamically.  

 During the System Center Configuration Manager hardware inventory process, the name for a class is transformed from "Win32_hardware" to "SMS_G_System_hardware". For example, "Win32_DiskDrive" translates to "SMS_G_System_DISK".  

 In addition to the class name change, the following differences are found between the Win32 classes and the System Center Configuration Manager hardware inventory server classes:  

-   Each System Center Configuration Manager class inherits four properties from [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

-   The System Center Configuration Manager hardware inventory classes do not support the Win32 class methods.  

-   Many of the System Center Configuration Manager hardware inventory classes contain a subset of the Win32 class properties.  

## In This Section  
 [SMS_G_System_SYSTEM Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_system-server-wmi-class.md)  
 Contains information about the operating system that is running on a client computer.  

 [SMS_G_System_WORKSTATION_STATUS Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_workstation_status-server-wmi-class.md)  
 Contains information about the last time inventory was collected on a client computer.  

 [SMS_InventoryClass Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_inventoryclass-server-wmi-class.md)  
 Represents inventory classes that exist in the system.  

 [SMS_InventoryClassProperty Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_inventoryclassproperty-server-wmi-class.md)  
 Represents the properties associated with an inventory class.  

 [SMS_InventoryReport Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_inventoryreport-server-wmi-class.md)  
 Represents the classes and properties that are enabled to collect.  

 [SMS_InventoryReportClass Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_inventoryreportclass-server-wmi-class.md)  
 Represents the classes that are enabled to collect in this inventory report.  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)
