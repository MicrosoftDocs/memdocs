---
title: "SMS_CIRelation_Flat Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b6cde26a-9d69-4b24-bb21-dfd209fe1aca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CIRelation_Flat Server WMI Class
The `SMS_CIRelation_Flat` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides a flat list of relationship information for directly or indirectly related configuration items.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIRelation_Flat : SMS_BaseClass  
{  
    UInt32 FromCIID;  
    Boolean IsVersionSpecific;  
    UInt32 Level;  
    UInt32 RelationType;  
    UInt32 ToCIID;  
};  
```  

## Methods  
 The `SMS_CIRelation_Flat` class does not define any methods.  

## Properties  
 `FromCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md)  

 `IsVersionSpecific`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md)  

 `Level`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Level represents the depth of the relationships between configuration items. A direct relationship to the configuration item is 1 and an indirect relationship can be 2 or higher.  

 `RelationType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md)  

 `ToCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_CIRelation Server WMI Class](../../../develop/reference/sum/sms_cirelation-server-wmi-class.md)  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
