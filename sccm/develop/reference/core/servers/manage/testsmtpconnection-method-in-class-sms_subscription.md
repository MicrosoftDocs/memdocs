---
title: "TestSmtpConnection Method"
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
ms.assetid: ff6b4c0d-9482-4169-9035-2af757c50450searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# TestSmtpConnection Method in Class SMS_Subscription
The `TestSmtpConnection` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, tests the SMTP connection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 TestSmtpConnection(  
     String ServerFqdn,  
     UInt32 Port,  
     String Sender,  
     String Recipients,  
     UInt32 AuthenticationType,  
     String UserName,  
     String EncryptPassword,   
     UInt32 TestID  
);  
```  

#### Parameters  
 `ServerFqdn`  
 Data type: `String`  

 Qualifiers: `[in]`  

 The FQDN of the SMTP server.  

 `Port`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 The port for the SMTP server.  

 `Sender`  
 Data type: `String`  

 Qualifiers: `[in]`  

 Email address of the sender.  

 `Recipients`  
 Data type: `String`  

 Qualifiers: `[in]`  

 Email addresses of the recipients.  

 `AuthenticationType`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Authentication type. Possible values are:  

|||  
|-|-|  
|0|Anonymous access.|  
|1|Use the computer account of the site server.|  
|2|Use the specified user name and password.|  

 `UserName`  
 Data type: `String`  

 Qualifiers: `[in]`  

 User name of the SMTP server connection account. This is used when `AuthenticationType` is 2.  

 `EncryptPassword`  
 Data type: `String`  

 Qualifiers: `[in]`  

 The encrypted password for the SMTP server connection account. This is used when `AuthenticationType` is 2.  

 `TestID`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 Test identifier. Used by `GetTestSmtpConnectionResult` to the test result.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Subscription Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_subscription-server-wmi-class.md)   
 [Alert System WMI Server Classes](../../../../../develop/reference/core/servers/manage/alert-system-server-wmi-classes.md)   
 [SMS_Subscription Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_subscription-server-wmi-class.md)
