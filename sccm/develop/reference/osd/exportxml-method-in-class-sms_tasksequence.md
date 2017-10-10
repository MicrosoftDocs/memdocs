---
title: "ExportXml Method"
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
ms.assetid: d6d3f17e-75fc-48c6-b6ed-b7b0d6169f41searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ExportXml Method in Class SMS_TaskSequence
The `ExportXml` Windows Management Instrumentation(WMI) class method, in Configuration Manager, exports task sequence XML in a format that is suitable to use on another site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
String ExportXml(  
      String Xml  
);  
```  

#### Parameters  
 `Xml`  
 Data type: `String`  

 Qualifiers: [in]  

 The task sequence XML. This XML comes from a previous call to the [SaveToXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/savetoxml-method-in-class-sms_tasksequence.md).  

## Return Values  
 A `String` data type defining the exported task sequence XML.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  

> [!IMPORTANT]
>  Your application must use secure techniques when calling the [SaveToXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/savetoxml-method-in-class-sms_tasksequence.md) method, because it retains all passwords (secret information) and product keys (quasi-secret information). Used by itself, this method is not secure when used for saving XML to a file for use by another site.  

 Your application uses `ExportXml` to translate between task sequence WMI code and task sequence XML. It first calls the [SaveToXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/savetoxml-method-in-class-sms_tasksequence.md) to create task sequence XML, preserving passwords and product keys. Then the application must call `ExportXml` and save the resulting information to a file, clearing all passwords (secret information) and product keys (quasi-secret information).  

 Remember that this method does not serialize task sequence XML for an [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) object. For a package, you must reflect the task sequence XML by using the \<sequence>\</sequence> tags.  

## Requirements  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)   
 [SaveToXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/savetoxml-method-in-class-sms_tasksequence.md)
