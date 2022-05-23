---
title: "GenerateProvisioningXML Method"
titleSuffix: "Configuration Manager"
description: "The ImportForProfile Windows Management Instrumentation (WMI) class method generates provisioning data in XML format."  
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6f9999f1-92bd-4929-b88b-b35aa4f849e6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GenerateProvisioningXML Method in Class SMS_BulkEnrollmentProfiles
The `ImportForProfile` Windows Management Instrumentation (WMI) class method, in Configuration Manager, generates provisioning data in XML format.  

## Syntax  

```  
sint32 GenerateProvisioningXML(  
     String BulkEnrollmentProfileID,  
     Boolean IsEncrypted,  
     String EncrytionPassword,  
     String ProvisioningDataXML  
);  

```  

#### Parameters  
 `BulkEnrollmentProfileID`  
 Data type: `String`  

 Qualifiers: [in]  

 The ID of the bulk enrollment profile.  

 `IsEncrypted`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if the enrollment package is password-protected. The default value is `false`.  

 `EncrytionPassword`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 The password used to encrypt the  enrollment package.  

 `ProvisioningDataXML`  
 Data type: `String`  

 Qualifiers: [out]  

 The XML output that contains the provisioning data.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BulkEnrollmentProfiles Server WMI Class](../../../develop/reference/mdm/sms_bulkenrollmentprofiles-server-wmi-class.md)   
