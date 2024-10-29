---
title: SMS_TaskSequence_Pointer Class
titleSuffix: Configuration Manager
description: The SMS_TaskSequence_Pointer WMI class is an SMS provider server class that represents information about an operating system deployment task sequence.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 4c5531c0-d8be-4cbd-96a0-7d8be828fbe5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_Pointer Server WMI Class
The `SMS_TaskSequence_Pointer` Windows Management Instrumentation (WMI) class is an SMS provider server class, in Configuration Manager, that represents information about an operating system deployment task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Pointer : SMS_TaskSequence_Step  
{  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueOnError;  
    String Description;  
    Boolean Enabled;  
    String Name;  
    String SupportedEnvironment;  
};  

```  

## Methods  
 The `SMS_TaskSequence_Pointer` class does not define any methods.  

## Properties  
 `Condition`  
 Data type:  `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [ValueMap, Not_Null:ToInstance]  

 The supported environment. The default value is WinPEandFullOS. Possible values are:  

|Value|
|-|  
|WinPE|  
|FullOS|  
|WinPEandFullOS|  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
