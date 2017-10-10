---
title: "UpdateFeatureExposureStatus Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b01f156d-97c2-4cf1-870c-96623fa30262searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# UpdateFeatureExposureStatus Method in Class SMS_CM_UpdateFeatures
The `UpdateFeatureExposureStatus` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the feature exposure status for an update feature extension.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
 SInt32 UpdateFeatureExposureStatus(  
     UInt32 Status  
);  

```  

#### Parameters  
 `Status`  
 Data type: `uint32`  

 Qualifiers: [in]  

 The installation state.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdateFeatures Server WMI Class](../../../develop/reference/sum/sms_cm_updatefeatures-server-wmi-class.md)   
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
