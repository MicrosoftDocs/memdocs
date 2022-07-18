---
title: "ExportRole Method"
titleSuffix: "Configuration Manager"
description: The ExportRole Windows Management Instrumentation class method, in Configuration Manager, exports roles to an XML string.
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 75620ffa-b4ad-45b7-a738-7e2c52ef0f62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ExportRole Method in Class SMS_Role
The `ExportRole` Windows Management Instrumentation (WMI) class method, in Configuration Manager, exports roles to an XML string.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ExportRole(  
     String RoleID,  
     String ExportedXML,  
);  
```  

#### Parameters  
 `RoleID`  
 Data type: `String`  

 Qualifiers: [in]  

 The id of the role.  

 `ExportedXML`  
 Data type: `String`  

 Qualifiers: [out]  

 The XML blob for the role.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Role Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_role-server-wmi-class.md)
