---
title: "SMS_WhatsNewFeature Class"
titleSuffix: "Configuration Manager"
description: "The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9cf5d7ff-d13d-4e1d-9df9-3c644e709be4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_WhatsNewFeature Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WhatsNewFeature : SMS_BaseClass  
{  
    String Description;  
    UInt32 Milestone;  
    String Name;  
    SMS_WhatsNewScenario Scenarios[];  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_WhatsNewFeature` class.  

|Method|Description|  
|------------|-----------------|  
|[GetFeatures Method in Class SMS_WhatsNewFeature](../../../develop/reference/misc/getfeatures-method-in-class-sms_whatsnewfeature.md)|Reserved for internal use.|  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for internal use.  

 `Milestone`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for internal use.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for internal use.  

 `Scenarios`  
 Data type: `SMS_WhatsNewScenario Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for internal use.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)
