---
title: CCM_InstanceEvent Class
titleSuffix: Configuration Manager
description: The CCM_InstanceEvent Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents an instance event.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 75240595-d0c1-48d9-9279-f3165934b888
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_InstanceEvent Client WMI Class
The `CCM_InstanceEvent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an instance event.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_InstanceEvent : __ExtrinsicEvent  
{  
    UInt32 ActionType;  
    String ClassName;  
    UInt32 MessageLevel;  
    UInt8 SECURITY_DESCRIPTOR[];  
    UInt32 SessionID;  
    String TargetInstancePath;  
    UInt64 TIME_CREATED;  
    String UserSID;  
    String Value;  
    UInt32 Verbosity;  
};  
```  

## Methods  
 The `CCM_InstanceEvent` class does not define any methods.  

## Properties  
 `ActionType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 Action type. Possible values are:    

|Value|Action type|  
|-|-|  
|1|Update|  
|2|Delete|  
|3|Reboot|  
|4|RebootCountdonwStart|  
|5|Logoff|  
|6|ProgramAvailable|  
|7|ProgramDownloadProgress|  
|8|OptionalProgramReady|  
|9|AssignedProgramReady|  
|10|ProgramExecuteComplete|  
|11|UpdateAvailable|  
|12|UpdateDeleted|  
|13|UpdateManadatoryInstallStart|  
|14|UpdateInstallComplete|  
|15|InstallJobStart|  
|16|InstallJobComplete|  
|19|AppEvaluationStarted|  
|20|AppEvaluationComplete|  
|21|AppAvailable|  
|22|AppEnforcementStarted|  
|23|AppEnforcementProgress|  
|24|AppEnforcementSuccess|  
|25|AppEnforcementFailure|  
|26|AppRemoved|  

 `ClassName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Event target class.    

 `MessageLevel`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 Message level. Possible values are:    

|Value|Message level|  
|-|-|  
|0|Informational|  
|1|Warning|  
|2|Error|  

 `SECURITY_DESCRIPTOR`  
 Data type: `UInt8 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Security descriptor.   

 `SessionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 User logon session identifier.   

 `TargetInstancePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Event target instance path.    

 `TIME_CREATED`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Time created.   

 `UserSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User identifier (SID).    

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Value for an event.    

 `Verbosity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 Verbosity. Possible values are:  

|Value|Verbosity|  
|-|-|  
|10|Low|  
|20|Medium_Low|  
|30|Medium|  
|40|Medium_High|  
|50|High|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
