---
title: "GetCurrentUser Method"
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
ms.assetid: b156164d-d873-47fe-8fc8-043ccdb6b75asearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetCurrentUser Method in Class SMS_Identification
The `GetCurrentUser` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the domain\user name that is used by the SMS Provider for authentication.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetCurrentUser(  
     String UserName  
);  
```  

#### Parameters  
 `UserName`  
 Data type: `String`  

 Qualifiers: [out]  

 Domain\user name being used by the SMS Provider. This name might differ from the domain\user name supplied by the application, depending on the domain trust model that is used.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Example Code  
 The following example shows how to call this method to get the current user.  

```  
Dim Identification As SWbemObject  
Dim UserName As String  

Set Identification = GetObject("winmgmts:\root\sms\site_<sitecode>:SMS_Identification")  
Identification.GetCurrentUser UserName  

MsgBox "UserName = " & UserName  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)
