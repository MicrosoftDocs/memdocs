---
title: "LoadFromXml Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e51e9945-604f-4e58-b82f-0acf21df49ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# LoadFromXml Method in Class SMS_TaskSequence
The `LoadFromXml` Windows Management Instrumentation (WMI) class method, in Configuration Manager, loads a task sequence into WMI objects from task sequence XML.  

> [!CAUTION]
>  As of Configuration Manager SP1, `LoadFromXml` has been replaced by the `ImportSequence` method on the `SMS_TaskSequencePackage` server WMI class.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SMS_TaskSequence LoadFromXml(  
      String Xml  
);  
```  

#### Parameters  
 `Xml`  
 Data type: `String`  

 Qualifiers: [in]  

 The task sequence XML to use to build the WMI objects.  

## Return Values  
 An [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application uses this method to import XML from an outside provider, for example, the user interface. It builds and returns a WMI object model based on the represented task sequence.  

> [!CAUTION]
>  You should not make changes to task sequences by using the XML. Rather, you should use the task sequence object model to create and edit task sequences. For more information, see [Operating System Deployment Task Sequence Object Model](../../../develop/osd/operating-system-deployment-task-sequence-object-model.md).  

> [!NOTE]
>  Use the [SetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md) method to add a task sequence to a task sequence package.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)
