---
title: "SetIgnorePrereqWarning Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 843a2227-7adb-4472-a907-e4f02fb13bf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SetIgnorePrereqWarning Method in Class SMS_CM_UpdatePackages
The `SetIgnorePrereqWarning` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the ignore pre-requisites  warning flag of the update packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetIgnorePrereqWarning(  
     UInt32 flag  
);  

```  

#### Parameters  
 `flag`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Flag to ignore the  pre-requisites  warning flag of the update packages. Possible values are:  

|||  
|-|-|  
|0|NOT_CONTINUE_ON_PREREQ_WARNING. During installation, stop the upgrade if there is a prerequisite warning.|  
|1|PREREQ_ONLY. Run only the prerequisite.|  
|2|CONTINUE_ON_PREREQ_WARNING. During installation, ignore the prerequisite warning.|  

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
