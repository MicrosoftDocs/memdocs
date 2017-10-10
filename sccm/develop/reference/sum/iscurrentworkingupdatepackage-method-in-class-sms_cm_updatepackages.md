---
title: "IsCurrentWorkingUpdatePackage Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 01f3462e-0d03-455d-a05e-375fb8681337searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IsCurrentWorkingUpdatePackage Method in Class SMS_CM_UpdatePackages
The `IsCurrentWorkingUpdatePackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, checks whether the update package is the package that setup is currently working on.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 IsCurrentWorkingUpdatePackage(  
     boolean IsCurrentWorkingUpdatePackage  
);  

```  

#### Parameters  
 `IsCurrentWorkingUpdatePackage`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the update package is the package that setup is currently working on; otherwise, `false`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackages Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackages-server-wmi-class.md)   
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
