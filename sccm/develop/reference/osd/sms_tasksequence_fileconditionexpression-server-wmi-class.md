---
title: "SMS_TaskSequence_FileConditionExpression Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 50f9834c-2f20-48ca-80a2-676b388abe63searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_FileConditionExpression Server WMI Class
The `SMS_TaskSequence_FileConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to check for the existence of a file and its creation time.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_FileConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      DateTime DateTime;  
      String DateTimeOperator;  
      String Path;  
      String Version;  
      String VersionOperator;  
};  
```  

## Methods  
 The `SMS_TaskSequence_FileConditionExpression` class does not define any methods.  

## Properties  
 `DateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time used to evaluate the target computer for a specific, user-specified timestamp on a file.  

 The timestamp that is displayed in the Configuration Manager console is the local time on the computer running the Configuration Manager console. The timestamp is converted to Coordinated Universal Time (UTC). The comparison on the target computer uses the UTC timestamp so that time zones and daylight savings time do not affect the comparison.  

 `DateTimeOperator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time operator. Possible values are:  

-   equals  

-   notEquals  

-   less  

-   lessEqual  

-   greater  

-   greaterEqual  

 `Path`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The path on the target computer for the file that is being verified. The path can contain embedded task sequence and system environment variables, for example, %*windir*%\notepad.exe.  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Value used to evaluate the target computer for a specific, user-specified version of a file.  

 `VersionOperator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The version operator. Possible values are:  

-   equals  

-   notEquals  

-   less  

-   lessEqual  

-   greater  

-   greaterEqual  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
