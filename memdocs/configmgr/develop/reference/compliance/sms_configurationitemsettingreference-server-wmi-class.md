---
title: SMS_ConfigurationItemSettingReference Class
titleSuffix: Configuration Manager
description: Provides the rule relationship to the settings that are referenced from different configuration items.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a44098ad-7baf-4bee-ad5e-240dca2e95bf
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ConfigurationItemSettingReference Server WMI Class
The `SMS_ConfigurationItemSettingReference` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides the rule relationship to the settings that are referenced from different configuration items.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationItemSettingReference : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    Boolean IsBroken;  
    UInt32 Rule_ID;  
    UInt32 Setting_ID;  
    String SettingName;  
};  
```  

## Methods  
 The `SMS_ConfigurationItemSettingReference` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

 `IsBroken`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_ConfigurationItemRules Server WMI Class](../../../develop/reference/compliance/sms_configurationitemrules-server-wmi-class.md)  

 `Setting_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_ConfigurationItemSettings Server WMI Class](../../../develop/reference/compliance/sms_configurationitemsettings-server-wmi-class.md).  

 `SettingName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_ConfigurationItemSettings Server WMI Class](../../../develop/reference/compliance/sms_configurationitemsettings-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
