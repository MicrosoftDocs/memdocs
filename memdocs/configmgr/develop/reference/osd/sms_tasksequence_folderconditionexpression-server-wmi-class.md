---
title: SMS_TaskSequence_FolderConditionExpression Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a condition expression to check for the existence of a folder and when it was created.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 03960b7a-7ca6-40f8-bca0-538cb8f7700d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_FolderConditionExpression Server WMI Class
The `SMS_TaskSequence_FolderConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to check for the existence of a folder and when it was created.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_FolderConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      DateTime DateTime;  
      String DateTimeOperator;  
      String Path;  
};  
```  

## Methods  
 The `SMS_TaskSequence_FolderConditionExpression` class does not define any methods.  

## Properties  
 `DateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time used to evaluate the target computer for a specific, user-specified timestamp on a folder.  

 The timestamp that is displayed in the Configuration Manager console is the local time on the computer running the Configuration Manager console. The timestamp is converted to Coordinated Universal Time (UTC). The comparison on the target computer uses the UTC timestamp so that time zones and daylight savings time do not affect the comparison.  

 `DateTimeOperator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time operator. Possible values are:  

- equals  

- notEquals  

- less  

- lessEqual  

- greater  

- greaterEqual  

  `Path`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [Not_Null]  

  The path on the target computer for the folder that is being verified. The path can contain embedded task sequence and system environment variables, for example, %*windir*%\Temp.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

> [!NOTE]
>  The evaluation of the path is affected by the value of the SMSTSDisableWow64Redirection environment variable.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
