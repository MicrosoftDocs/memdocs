---
title: "ExportRole Method"
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
ms.assetid: 75620ffa-b4ad-45b7-a738-7e2c52ef0f62searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ExportRole Method in Class SMS_Role
The `ExportRole` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, exports roles to an XML string.  

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
