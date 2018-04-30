---
title: "UpdatePackageSiteState Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 5c597141-bccd-4c52-a1d6-767a82e77019
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# UpdatePackageSiteState Method in Class SMS_CM_UpdatePackageSiteStatus
The `UpdatePackageSiteState` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the package installation state of the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UpdatePackageSiteState(  
     UInt32 State  
);  

```  

#### Parameters  
 `State`  
 Data type: `UInt32`  

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
 [SMS_CM_UpdatePackageSiteStatus Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackagesitestatus-server-wmi-class.md)   
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
