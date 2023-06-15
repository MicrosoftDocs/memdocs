---
description: The SMS_TaskSequence_Reference Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents the package ID and optional program name.
title: SMS_TaskSequence_Reference Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7df3c90d-eba4-4ece-a2b8-e12e4781ed8b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_Reference Server WMI Class
The `SMS_TaskSequence_Reference` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the package ID and optional program name used by the task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Reference  
{  
      String Package;  
      String Program;  
      UInt32 Type  
};  
```  

## Methods  
 The `SMS_TaskSequence_Reference` class does not define any methods.  

## Properties  
 `Package`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 If `Type` is 0, the identifier of the package. If `Type` is 1, the identifier of the application (the model name).  

 `Program`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional. The name of the program associated with the package. See [SMS_Program Server WMI Class](../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md).  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of reference. The possible values are:  

| Value | Reference type |  
| ----- | -------------- |  
|0|Package Reference|  
|1|Application Reference|  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application can obtain the packages referenced by a task sequence from the `References` property of [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)
