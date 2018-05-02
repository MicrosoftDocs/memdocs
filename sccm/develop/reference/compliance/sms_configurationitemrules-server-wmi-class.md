---
title: "SMS_ConfigurationItemRules Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 870fb139-d723-4d65-b4e8-a1ff15fd19b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ConfigurationItemRules Server WMI Class
The `SMS_ConfigurationItemRules` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents configuration item rules.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationItemRules : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    String ModelName;  
    UInt32 Rule_ID;  
    String Rule_UniqueID;  
    String RuleDescription;  
    String RuleName;  
};  
```  

## Methods  
 The `SMS_ConfigurationItemRules` class does not define any methods.  

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

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The database identifier of a rule defined in a configuration item.  

 `Rule_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Uniquely identifies a rule defined in the configuration item and is used for reporting rule level details.  

 `RuleDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the rule.  

 `RuleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_CollectionRule Server WMI Class](../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md)  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
