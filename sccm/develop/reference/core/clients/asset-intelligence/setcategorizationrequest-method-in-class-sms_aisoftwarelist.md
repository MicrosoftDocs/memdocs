---
title: "SetCategorizationRequest Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9c2b8373-39ed-4296-863d-70ddb4cbb3b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SetCategorizationRequest Method in Class SMS_AISoftwareList
The `SetCategorizationRequest` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, initiates a System Center Online software categorization request.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetCategorizationRequest(      
     String SoftwareKey,  
);  
```  

#### Parameters  
 `SoftwareKey`  
 Data type: `String`  

 Qualifiers: [in]  

 Hash of the software to be categorized. After this method is called, the hash is sent to the System Center Online server to be categorized during its next release.  

 This property name has changed from `SoftwarePropertiesHash` to `SoftwareKey` in SP1.  

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
