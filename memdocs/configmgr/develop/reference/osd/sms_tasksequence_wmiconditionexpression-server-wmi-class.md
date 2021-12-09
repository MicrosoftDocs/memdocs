---
title: "SMS_TaskSequence_WMIConditionExpression Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a412bf10-51d1-4f51-9767-fb024d85f9c6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_WMIConditionExpression Server WMI Class
The `SMS_TaskSequence_WMIConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to check for the existence of results of a WMI query.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_WMIConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      String Namespace;  
      String Query;  
};  
```  

## Methods  
 The `SMS_TaskSequence_WMIConditionExpression` class does not define any methods.  

## Properties  
 `Namespace`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Namespace for the query.  

 `Query`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, AllowedLen("1-16384")]  

 The WQL query for the condition expression. The length is between 1 and 16,384 characters.  

## Remarks  
 The query result set is the results that satisfy the condition. For example, if you need to identify if a computer has at least one NTFS partition, you would use the following query:  

```  
Select * from win32_logicaldisk where FileSystem='NTFS'  
```  

 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers that are included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
