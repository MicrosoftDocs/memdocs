---
title: SMS_G_System_History Class
description: The SMS_G_System_History class is an SMS Provider server class that serves as an abstract base class representing hardware component state history for a client computer.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a1681a18-9456-4d91-b0d0-26831d469868
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_History Server WMI Class
The `SMS_G_System_History` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as an abstract base class representing hardware component state history for a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_History : SMS_G_System  
{  
     UInt32 GroupID;  
     UInt32 ResourceID;  
     UInt32 RevisionID;  
     DateTime TimeStamp;  
};  
```  

## Methods  
 The `SMS_G_System_History` class does not define any methods.  

## Properties  
 `GroupID`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: [key]  

 ID of the group that distinguishes one hardware inventory instance from another within one client resource. For example, each logical disk object for a client is assigned a unique `GroupID` value.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 `RevisionID`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: [key]  

 ID that increments if the object changes after the last time inventory was taken. The highest number indicates the most recent update. Objects with the same `ResourceID` and `GroupID` values are deltas. They differ from one another by the `RevisionID` number.  

 `TimeStamp`  
 Data type: **DateTime**  

 Access type: Read-only  

 Qualifiers: None  

 Date and time of the inventory.  

## Remarks  
 History objects are created from the current hardware component object when the component has changed since the last inventory. This class represents a collection of prior hardware component states for the client.  

 Your application uses this class to determine the state of client hardware at any given time. Names of derived history classes are prefixed with "SMS_GEH_System_" followed by the inventoried object name. An example class name is `SMS_GEH_System_ACCOUNT`. Your application can use the derived classes to determine the state of a hardware component on a client at a given point in time.  

 Hardware history is deleted on a schedule if the Delete Aged Inventory History database maintenance task is set to `true` in the Configuration Manager console. You can also enable this task and set the schedule by updating the site control file. The site control item [SMS_SCI_SQLTask Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_sqltask-server-wmi-class.md) object, and the `TaskName` value is "Delete Aged Inventory History". For an example that updates the site control file, see [About the site control file](../../../../core/understand/about-the-configuration-manager-site-control-file.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)
