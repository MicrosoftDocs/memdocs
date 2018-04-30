---
title: "SMS_InstanceChangeNotification Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: feda268d-16d9-43a0-8bef-d26070e5deca
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_InstanceChangeNotification Server WMI Class
The `SMS_InstanceChangeNotification` WMI class is an SMS Provider server class, in System Center Configuration Manager, that notifies the administrator console that an alert has changed its status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InstanceChangeNotification : SMS_BaseClass  
{  
   String Action;  
   String ClassName;   
   ref:SMS_BaseClass InstancePath;  
   UInt8[] SECURITY_DESCRIPTOR;  
   UInt64 TIME_CREATED;  
};  
```  

## Methods  
 The `SMS_InstanceChangeNotification` class does not define any methods.  

## Properties  
 `Action`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The action that caused the change notification.  

|Possible values|  
|----|  
|Insert|  
|Update|  
|Delete|  

 `ClassName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the class that caused the change notification. For example, for an alert, the name of the class is SMS_Alert.  

 `InstancePath`  
 Data type: `ref:SMS_BaseClass`  

 Access type: Read/Write  

 Qualifiers: None  

 The instance path of the object that caused the change notification.  

 `SECURITY_DESCRIPTOR`  
 Data type: `UInt8[]`  

 Access type: Read/Write  

 Qualifiers: None  

 For internal use only.  

 `TIME_CREATED`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 For internal use only.  

## Remarks  
 This class allows alert tiles to be updated with the most recent status information.  

 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers that are included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Console Folder Server WMI Classes](../../../../../develop/reference/core/servers/console/console-folder-server-wmi-classes.md)
