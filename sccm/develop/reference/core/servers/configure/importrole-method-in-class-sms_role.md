---
title: "ImportRole Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8ba0735a-95ed-4ee6-9dea-b7d680f41c6a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ImportRole Method in Class SMS_Role
The `ImportRole` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, imports a role defined by an XML string to the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ImportRole(  
     String RolesXml,  
     Boolean OverwrittenExisted,   
     String ErrorStr,  
);  
```  

#### Parameters  
 `RolesXml`  
 Data type: `String`  

 Qualifiers: [in]  

 The id of the role.  

 `OverwrittenExisted`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true`, if an existing role should be overwritten. The default value is true.  

 `ErrorStr`  
 Data type: `String`  

 Qualifiers: [out]  

 The error information if there is any error while importing the role.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Role Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_role-server-wmi-class.md)
