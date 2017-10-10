---
title: "SMS_InventoryReport Class"
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
ms.assetid: 2068768c-2746-42f0-b4d4-e7a43241b160searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_InventoryReport Server WMI Class
The `SMS_InventoryReport` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the classes and properties that are enabled to be collected.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InventoryReport : SMS_BaseClass  
{  
    UInt32 DefaultTimeout;  
    String Description;  
    String InventoryReportID;  
    SMS_InventoryReportClass ReportClasses[];  
    UInt32 ReportTimeout;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_InventoryReport` class.  

|Method|Description|  
|------------|-----------------|  
|[ImportInventoryReport Method in Class SMS_InventoryReport](../../../../../develop/reference/core/clients/manage/importinventoryreport-method-in-class-sms_inventoryreport.md)|Imports new inventory classes and enables the collection of existing classes.|  

## Properties  
 `DefaultTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The default timeout of the inventory collection cycle on the client.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The description of the inventory report.  

 `InventoryReportID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 A GUID that represents the inventory report type.  

 `ReportClasses`  
 Data type: `Object Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The classes that are enabled for collection in this report.  

 `ReportTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The timeout of the inventory collection cycle on the client.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
