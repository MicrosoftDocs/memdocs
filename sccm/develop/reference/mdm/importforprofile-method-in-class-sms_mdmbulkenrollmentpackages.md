---
title: "ImportForProfile Method"
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
ms.assetid: fdbb743a-c476-474e-a129-e789180c1bf5searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ImportForProfile Method in Class SMS_MDMBulkEnrollmentPackages
The `ImportForProfile` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports an On-Premises Mobile Device Management (MDM)  bulk enrollment package for a profile.  

## Syntax  

```  
sint32 ImportForProfile(  
     String ProfileGUID,  
     String CertificateGUID,  
     String PackageName,  
     String Certificate  
);  

```  

#### Parameters  
 `ProfileGUID`  
 Data type: `String`  

 Qualifiers: [in]  

 The GUID of the profile.  

 `CertificateGUID`  
 Data type: `String`  

 Qualifiers: [in]  

 The GUID of the certificate.  

 `PackageName`  
 Data type: `String`  

 Qualifiers: [in]  

 Package name.  

 `Certificate`  
 Data type: `String`  

 Qualifiers: [in]  

 The root certificate.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MDMBulkEnrollmentPackages Server WMI Class](../../../develop/reference/mdm/sms_mdmbulkenrollmentpackages-server-wmi-class.md)   
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)
