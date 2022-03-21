---
title: UpdateFeatureExposureStatus method in class SMS_CM_UpdatePackageFeatures
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3bc02633-89ab-495a-8b26-82c59c84775b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# UpdateFeatureExposureStatus Method in Class SMS_CM_UpdatePackageFeatures
The `UpdateFeatureExposureStatus` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the feature exposure status for an update package feature extension.  

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

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackageFeatures Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackagefeatures-server-wmi-class.md)   
