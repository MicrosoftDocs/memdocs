---
title: "SMS_G_System_Current Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 01e0699f-7031-47a7-a3c2-5e98aeebe5f6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_G_System_Current Server WMI Class
The `SMS_G_System_Current` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that serves as an abstract base class and represents the current client state at the time of the last hardware inventory.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_Current : SMS_G_System  
{  
     UInt32 GroupID;  
     UInt32 ResourceID;  
     UInt32 RevisionID;  
     DateTime TimeStamp;  
};  
```  

## Methods  
 The `SMS_G_System_Current` class does not define any methods.  

## Properties  
 `GroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the group that distinguishes one hardware inventory instance from another within one client resource. For example, each logical disk instance for a client is assigned a unique `GroupID` value.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `RevisionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID that increments if the object changes after the last time inventory was taken. The highest number indicates the most recent update. Objects with the same `ResourceID` and `GroupID` values are deltas. They differ from one another by the `RevisionID` number.  

 `TimeStamp`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of the inventory.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application can query classes derived from `SMS_G_System_Current` to get the current state of individual client hardware components. Alternatively the application can query `SMS_G_System_Current` itself to get the current state of all client hardware components. For example, the following query retrieves all hardware components for the given client.  

```  
SELECT * FROM SMS_G_System_Current  
WHERE ResourceID = <resourceid>  
```  

 Although using this query is a simple solution for getting all the hardware components for a client, it is inefficient. WMI turns the query into multiple queries, one for each subclass, and creates a thread for each query. If performance is critical, your application should query each subclass specifically.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)
