---
title: SetSourceSite method in class SMS_OperatingSystemInstallPackage
titleSuffix: Configuration Manager
description: The SetSourceSite Windows Management Instrumentation class method, in Configuration Manager, sets the code of the source site for the operating system install package.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 68576571-adfc-4c34-b8c8-6eefaf9cb3cf
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SetSourceSite Method in Class SMS_OperatingSystemInstallPackage
The `SetSourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the code of the source site for the operating system install package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetSourceSite(  
      String SourceSite  
);  
```  

#### Parameters  
 `SourceSite`  
 Data type: `String`  

 Qualifiers: [in]  

 The code of the source site for the operating system install package.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md)
