---
title: "SMS_UpdateRelations Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 206ef5cb-9bad-45c9-bda5-91499383a66a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UpdateRelations Server WMI Class
The `SMS_UpdateRelations` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines the relationship between two software updates.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdateRelations : SMS_BaseClass  
{  
      UInt32 RelatedUpdateID;  
      UInt32 Relation;  
      UInt32 UpdateID;  
};  
```  

## Methods  
 The `SMS_UpdateRelations` class does not define any methods.  

## Properties  
 `RelatedUpdateID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for one of the updates.  

 `Relation`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Relationship between `RelatedUpdateID` and `UpdateID`. Possible values are defined for [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md).  

 `UpdateID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for the other update.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)   
 [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md)   
 [Configuration Manager Software Updates](../../../develop/sum/software-updates.md)
