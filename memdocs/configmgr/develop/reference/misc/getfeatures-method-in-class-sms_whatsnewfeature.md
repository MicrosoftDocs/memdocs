---
title: GetFeatures Method
titleSuffix: Configuration Manager
description: This article describes the Get Features Method in Class SMS_WhatsNewFeature. The syntax is detailed below.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8ad3467f-9726-4ede-ab1f-60991ea16ce2
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetFeatures Method in Class SMS_WhatsNewFeature
For internal use only.  

## Syntax  

```  
SInt32 GetFeatures(  
     UInt32 MinMilestone,  
     UInt32 MaxMilestone,  
     UInt32 LocaleID,  
     SMS_WhatsNewFeature Features[]  
);  

```  

#### Parameters  
 `MinMilestone`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Reserved for internal use.  

 `MaxMilestone`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Reserved for internal use.  

 `LocaleID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Reserved for internal use.  

 `Features`  
 Data type: `SMS_WhatsNewFeature Array`  

 Qualifiers: [out]  

 Reserved for internal use.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_WhatsNewFeature Server WMI Class](../../../develop/reference/misc/sms_whatsnewfeature-server-wmi-class.md)
