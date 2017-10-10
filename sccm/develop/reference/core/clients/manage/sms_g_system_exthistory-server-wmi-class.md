---
title: "SMS_G_System_ExtHistory Class"
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
ms.assetid: 4d8e6146-36dc-4c88-9d38-15c89ca4ee6fsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_G_System_ExtHistory Server WMI Class
The `SMS_G_System_ExtHistory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that serves as an abstract base class representing operating system extended history for a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_ExtHistory : SMS_G_System  
{  
     UInt32 GroupID;  
     UInt32 ResourceID;  
     UInt32 RevisionID;  
     DateTime TimeStamp;  
};  
```  

## Methods  
 The `SMS_G_System_ExtHistory` class does not define any methods.  

## Properties  
 `GroupID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 ID of the group that distinguishes one hardware inventory instance from another within one client resource. For example, each logical disk object for a client is assigned a unique `GroupID` value.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 `RevisionID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 ID that increments if the object changes after the last time inventory was taken. The highest number indicates the most recent update. Objects with the same `ResourceID` and `GroupID` values are deltas. They differ from one another by the `RevisionID` number.  

 `TimeStamp`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Date and time of the inventory.  

## Remarks  
 Your application uses this class to determine the state of a client at any given time. Names of derived extended history classes are prefixed with "SMS_GEH_System_" followed by the inventoried object name. An example class name is `SMS_GEH_System_ACCOUNT`. Your application can use the derived classes to determine the state of a hardware component on a client at a given point in time.  

 The SMS Provider determines the state by using the information from classes derived from both [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md) and [SMS_G_System_History Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_history-server-wmi-class.md). However, the application cannot query `SMS_G_System_ExtHistory` to determine the state of all hardware components on a client at a given point in time.  

 Your query must include the `ResourceID` and `TimeStamp` values in the WHERE clause, as shown in the following example.  

```  
SELECT * FROM SMS_GEH_System_Logical_Disk  
WHERE ResourceID = <resourceid>  
AND Timestamp = "<timestamp>"  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)
