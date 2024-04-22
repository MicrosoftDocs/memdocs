---
title: SMS_MachineVariable Class
titleSuffix: Configuration Manager
description: The SMS_MachineVariable WMI class defines the settings of a task sequence variable that is unique to a specific computer. 
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5a0951f6-f184-4c00-a7d3-94cd3f466de9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_MachineVariable Server WMI Class
The `SMS_MachineVariable` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager that defines the settings of a task sequence variable that is unique to a specific computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MachineVariable  
{  
      Boolean IsMasked;  
      String Name;  
      String Value;  
};  
```  

## Methods  
 The `SMS_MachineVariable` class doesn't define any methods.  

## Properties  
 `IsMasked`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 This property isn't currently used.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The name of the machine variable. The default value is "".  

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The machine variable value. The default value is `null`.  

## Remarks  
 The task sequence variable can customize the behavior of a task sequence for a specific computer, and it overrides any definition that is set by [SMS_CollectionVariable Server WMI Class](../../../develop/reference/osd/sms_collectionvariable-server-wmi-class.md). These variables are automatically replicated down through the site hierarchy. For example, if a variable is declared on the primary child site server, it will be available on the primary grandchild site server, but not on the primary site server.  

 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers that are included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class to create objects that are embedded by the [SMS_MachineSettings Server WMI Class](../../../develop/reference/osd/sms_machinesettings-server-wmi-class.md) and accessed by using the `MachineVariables` property. For an example of the use of this class, see How to Create a Computer Variable in Configuration Manager.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MachineSettings Server WMI Class](../../../develop/reference/osd/sms_machinesettings-server-wmi-class.md)   
 [SMS_CollectionVariable Server WMI Class](../../../develop/reference/osd/sms_collectionvariable-server-wmi-class.md)
