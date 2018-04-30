---
title: "SaveToXml Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b6ee24cd-893b-4342-ae0e-36ef4640a98c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SaveToXml Method in Class SMS_TaskSequence
The `SaveToXml` Windows Management Instrumentation (WMI) class method, in Configuration Manager serializes a task sequence from WMI objects to XML.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
String SaveToXml(  
      SMS_TaskSequence TaskSequence,  
      SMS_TaskSequence_Reference References[],  
      UInt32 Flags  
);  
```  

#### Parameters  
 `TaskSequence`  
 Data type: `SMS_TaskSequence`  

 Qualifiers: [in]  

 An [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object representing the task sequence to serialize.  

 `References`  
 Data type: `SMS_TaskSequence_Reference` Array  

 Qualifiers: [out]  

 [SMS_TaskSequence_Reference Server WMI Class](../../../develop/reference/osd/sms_tasksequence_reference-server-wmi-class.md) objects representing any packages and programs referenced in the XML that are required by the task sequence. The provider uses these objects to check against the packages and programs that exist on the site.  

 `Flags`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Flags identifying serialization details. The only flag currently supported is 0x00000001, sequence deploys an operating system image.  

## Return Values  
 A `String` data type containing the XML representation of the task sequence.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  

> [!IMPORTANT]
>  Your application must use secure techniques when calling this method, because it retains all passwords (secret information) and product keys (quasi-secret information). It is secure if the XML is being saved to the database through the task sequence package. This method is not secure, however, if the XML is being saved to a file for use by another site. In this case, the call must be followed by a call to the [ExportXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/exportxml-method-in-class-sms_tasksequence.md) to strip out the passwords and product keys.  

 Your application uses this method when saving task sequences and translating between task sequence WMI code and task sequence XML, preserving passwords and product keys. The most common use is by an outside provider that is manipulating the WMI object model.  

 Remember that this method does not serialize task sequence XML for an [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) object. For a package, you must reflect the task sequence XML using the \<sequence>\</sequence> tags.  

## Requirements  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)   
 [SMS_TaskSequence_Reference Server WMI Class](../../../develop/reference/osd/sms_tasksequence_reference-server-wmi-class.md)   
 [ExportXml Method in Class SMS_TaskSequence](../../../develop/reference/osd/exportxml-method-in-class-sms_tasksequence.md)
