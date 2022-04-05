---
title: "SetSequence Method"
titleSuffix: "Configuration Manager"
description: "A Windows Management Instrumentation class method that updates the task sequence package with the specified task sequence."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4bfe9c19-7045-46b7-9e72-32ac8e02e031
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetSequence Method in Class SMS_TaskSequencePackage
The `SetSequence` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the task sequence package with the specified task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetSequence(  
      SMS_TaskSequencePackage TaskSequencePackage,  
      SMS_TaskSequence TaskSequence,  
      String SavedTaskSequencePackagePath  
);  
```  

#### Parameters  
 `TaskSequencePackage`  
 Data type: `SMS_TaskSequencePackage`  

 Qualifiers: [in]  

 The package that the task sequence `TaskSequence` is added to. See [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md).  

 `TaskSequence`  
 Data type: `SMS_TaskSequence`  

 Qualifiers: [in]  

 The [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object that represents the task sequence that is added to `TaskSequencePackage`.  

 `SavedTaskSequencePackagePath`  
 Data type: `String`  

 Qualifiers: [out]  

 The relative WMI object path for the updated task sequence package.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 `SetSequence` is used to associate a task sequence ([SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) with a task sequence package.  

 This method also updates other properties of the task sequence package, for example, package references and task sequence type, based on the specified task sequence.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)   
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)   
 [GetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getsequence-method-in-class-sms_tasksequencepackage.md)
