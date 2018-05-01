---
title: "GetSequence Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9606ae78-67c2-4b74-9736-b152c5ee0ce9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetSequence Method in Class SMS_TaskSequencePackage
The `GetSequence` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets a task sequence ([SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) from a task sequence package ([SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)).  

 The following syntax is simplified from Managed Object Format (MOF) code, and it defines the method.  

## Syntax  

```  
SInt32 GetSequence(  
      SMS_TaskSequencePackage TaskSequencePackage,  
      SMS_TaskSequence TaskSequence  
);  
```  

#### Parameters  
 `TaskSequencePackage`  
 Data type: `SMS_TaskSequencePackage`  

 Qualifiers: [in]  

 The task sequence package that contains the requested task sequence. See [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md).  

 `TaskSequence`  
 Data type: `SMS_TaskSequence`  

 Qualifiers: [out]  

 The [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object that represents the task sequence contained in the task sequence package specified in `TaskSequencePackage`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

> [!NOTE]
>  The task sequence is returned in the `TaskSequence` parameter.  

## Remarks  
 You use `GetSequence` to get a [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) WMI object that represents a task sequence from a task sequence package. With this object, you can make changes to the task sequence and then update the task sequence package by using the [SetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)   
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)   
 [SetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md)
