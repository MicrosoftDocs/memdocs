---
title: "GetCategorizationRequestText Method"
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
ms.assetid: 0181433b-d409-4739-8582-2d11dadf2f5bsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetCategorizationRequestText Method in Class SMS_AISoftwareList
The `GetCategorizationRequestText` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, retrieves the XML that is sent to System Center Online for categorization.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetCategorizationRequestText(      
     String SoftwareKey,  
     String CategorizationRequestText  
);  
```  

#### Parameters  
 `SoftwareKey`  
 Data type: `String`  

 Qualifiers: [in]  

 The MD5 hash of the software to be categorized. The hash is made up of the software name, publisher, and version.  

 This property name has changed from `SoftwarePropertiesHash` to `SoftwareKey` in SP1.  

 `CategorizationRequestText`  
 Data type: `String`  

 Qualifiers: [out]  

 XML formatted string which contains the hash, name, version, publisher, evidence type, and system default locale identifier (LCID) of the software.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AISoftwareList Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aisoftwarelist-server-wmi-class.md)
