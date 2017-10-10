---
title: "SMS_TaskSequence_RegistryConditionExpression Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 3229c0e7-f7cd-4105-957a-11ba2339f25dsearchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_RegistryConditionExpression Server WMI Class
The `SMS_TaskSequence_RegistryConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to check for the existence of a registry key and, optionally, compare it to specified data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_RegistryConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      String Data;  
      String KeyPath;  
      String Operator;  
      String Type;  
      String Value;  
};  
```  

## Methods  
 The `SMS_TaskSequence_RegistryConditionExpression` class does not define any methods.  

## Properties  
 `Data`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 User-specified data to compare to the registry key information.  

 `KeyPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Path for the registry key.  

 `Operator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The condition operator to use in the comparison. Possible values are:  

-   exists  

-   nonExists  

-   equals  

-   notEquals  

-   less  

-   lessEqual  

-   greater  

-   greaterEqual  

 `Type`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Registry key type. Possible values are:  

-   REG_BINARY  

-   REG_DWORD  

-   REG_EXPAND_SZ  

-   REG_MULTI_SZ  

-   REG_NONE  

-   REG_QWORD  

-   REG_SZ  

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-250")]  

 Value of the registry key. The value length can be between 0 and 250 characters.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 You use `SMS_TaskSequence_RegistryConditionExpression` to check for the existence of a registry key, or alternatively to check for a registry key value. For example, if you have the registry key "HKEY_LOCAL_MACHINE\SYSTEM\Select" and the DWORD value set to 'Current' under it, then, `KeyPath` would be "HKEY...\Select", `Operator` would be 'Equals' (or 'NotEquals', and so on), `Type` would be REG_DWORD, `Value` would be 'Select', and `Data` would be the numeric value to compare against the value of the registry key ('Select').  

 `Type` applies only when checking for the existence of a registry value specified in `Value`; when comparing values, `Type` is not used. This means that if 'Exists' is the `Operator` and REG_SZ is the `Type`, the result will evaluate to `False` because 'Select' is a REG_DWORD.  

 However, when comparing values ('Equals', 'Greater', and so on), then `Type` is not used. Instead the value of `Data` is compared against `Value` regardless of the actual registry type and `Type`.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
