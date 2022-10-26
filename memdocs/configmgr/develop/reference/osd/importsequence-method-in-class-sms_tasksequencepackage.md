---
title: ImportSequence Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the ImportSequence WMI class method imports a task sequence package file based on the provided XML data of a previously exported task sequence package.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 70b08f66-fa17-482d-80d8-d2a3fb999e23
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ImportSequence Method in Class SMS_TaskSequencePackage
The `ImportSequence` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports a task sequence package file based on the provided XML data of a previously exported task sequence package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ImportSequence(  
      String SequenceXML,  
      SMS_TaskSequence TaskSequence  
);  
```  

#### Parameters  
 `SequenceXML`  
 Data type: `String`  

 Qualifiers: [in]  

 A `string` variable which contains the XML data of the task sequence package to import.  

 `TaskSequence`  
 Data type: `SMS_TaskSequence`  

 Qualifiers: [out]  

 The produced `SMS_TaskSequence` object.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)
