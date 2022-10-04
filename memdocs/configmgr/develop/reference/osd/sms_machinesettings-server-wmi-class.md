---
title: SMS_MachineSettings Class
titleSuffix: Configuration Manager
description: The SMS_MachineSettings WMI class describes attributes that are specific to a single computer that is managed by Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 940ea289-0ae3-4b72-a394-58cb63f2a158
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_MachineSettings Server WMI Class
The `SMS_MachineSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes attributes that are specific to a single computer that is managed by Configuration Manager.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MachineSettings  
{  
      DateTime LastModificationTime;  
      UInt32 LocaleID;  
      SMS_MachineVariable MachineVariables[];  
      UInt32 ResourceID;  
      String SourceSite;  
};  
```  

## Methods  
 The `SMS_MachineSettings` class does not define any methods.  

## Properties  
 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The date and time when the computer settings were last modified.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the locale used to convert the localized name and description of the computer. The default locale ID is 1033, English (United States).  

 `MachineVariables`  
 Data type: `SMS_MachineVariable` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The [SMS_MachineVariable Server WMI Class](../../../develop/reference/osd/sms_machinevariable-server-wmi-class.md) objects representing computer variables for the computer resource.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Key]  

 The unique resource ID for the computer.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3"), Not_null]  

 The code of the source site. The code length can be up to three characters. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application can use this class as described in How to Create a Computer Variable in Configuration Manager.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_MachineVariable server WMI class](sms_machinevariable-server-wmi-class.md)
