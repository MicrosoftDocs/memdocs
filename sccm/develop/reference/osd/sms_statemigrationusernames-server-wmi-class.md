---
title: "SMS_StateMigrationUserNames Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 26d7ad7d-e8e6-41f4-9300-a4a4359dba31
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_StateMigrationUserNames Server WMI Class
The `SMS_StateMigrationUserNames` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a localized user name during state migration.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StateMigrationUserNames  
{  
      UInt32 LocaleID;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_StateMigrationUserNames` class does not define any methods.  

## Properties  
 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the locale associated with the user name.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The localized user name. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class to create objects that are embedded by the [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md) and accessed using the `UserNames` property. For an example of the use of this class, see How to Create an Association Between Two Computers in Configuration Manager.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)
