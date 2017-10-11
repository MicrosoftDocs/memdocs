---
title: "ReloadImageProperties Method"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 3e6c970d-beb0-441b-98c6-11a8c4d26152searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ReloadImageProperties Method in Class SMS_OperatingSystemInstallPackage
The `ReloadImageProperties` Windows Management Instrumentation WMI class method, in Configuration Manager, reloads metadata from the source .wim file and synchronizes the metadata with the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ReloadImageProperties();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application uses this method to update the .wim file associated with the operating system install package. The update is based on the location defined in the `PkgSourcePath` property of [SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md).  

 The application must:  

1.  Establish a connection to the SMS Provider. For more information, see About the SMS Provider in Configuration Manager.  

2.  Get the `SMS_OperatingSystemInstallPackage` object to update.  

3.  Call the `ReloadImageProperties` method.  

4.  Commit the `SMS_OperatingSystemInstallPackage` object.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md)   
 [GetImageProperties Method in Class SMS_OperatingSystemInstallPackage](../../../develop/reference/osd/getimageproperties-method-in-class-sms_operatingsysteminstallpackage.md)
