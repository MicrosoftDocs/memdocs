---
description: Learn how to check if the default application catalog website point in the client agent settings is set to portalUrl.
title: CheckPortalUrl Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 377797dd-dd3c-476f-995c-647dbda78123
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CheckPortalUrl Method for Class SMS_ClientSettings
The `CheckPortalUrl` Windows Management Instrumentation (WMI) class method, in Configuration Manager, checks whether the default application catalog website point in the default or custom client agent settings is set to `portalUrl`.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 CheckPortalUrl(  
     string PortalUrl,  
     boolean isUsed  
);  
```  

#### Parameters  
 `PortalUrl`  
 Data type: `String`  

 Qualifiers: `[in]`  

 PortalUrl.   

 `isUsed`  
 Data type: `Boolean`  

 Qualifiers: `[out]`  

 isUsed.   

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ClientSettings Server WMI Class](../../../../../develop/reference/core/clients/config/sms_clientsettings-server-wmi-class.md)
