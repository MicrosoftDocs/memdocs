---
description: Learn how to represent configuration item settings using the SMS_ConfigurationItemSettings class in Configuration Manager. 
title: "SMS_ConfigurationItemSettings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1a412c5a-39de-4ba0-8fe7-c52f67cd076d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ConfigurationItemSettings Server WMI Class
The `SMS_ConfigurationItemSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents configuration item settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationItemSettings : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    UInt32 DataType;  
    String ModelName;  
    UInt32 Setting_ID;  
    String Setting_UniqueID;  
    String SettingDescription;  
    String SettingName;  
    UInt32 SourceType;  
};  
```  

## Methods  
 The `SMS_ConfigurationItemSettings` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

 `DataType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Defines the type of setting (integer, string, and so on) to facilitate rule authoring and evaluation.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

 `Setting_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The database identifier of a setting in the configuration item.  

 `Setting_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Uniquely identifies a setting defined in the configuration item.  

 `SettingDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the setting.  

 `SettingName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the setting.  

 `SourceType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The setting discovery provider type defined, if this setting is discovered from the registry, file system, WMI and so on.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
