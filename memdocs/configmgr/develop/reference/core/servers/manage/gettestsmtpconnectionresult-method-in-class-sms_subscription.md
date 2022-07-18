---
title: "GetTestSmtpConnectionResult Method"
description: Learn how the GetTestSmtpConnectionResult Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the test SMTP connection result.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 933bdb86-7a0e-457d-826e-80c349744ab6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetTestSmtpConnectionResult Method in Class SMS_Subscription
The `GetTestSmtpConnectionResult` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the test SMTP connection result.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetTestSmtpConnectionResult(  
     UInt32 TestID,  
     UInt32 ErrorCode  
);  
```  

#### Parameters  
 `TestID`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Test identifier returned by `TestSmtpConnection`.  

 `ErrorCode`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 Represents the test results. Possible values are:  

| Value | Error code |
| ----- | ---------- |
|0|Success.|  
|1|The test is initializing.|  
|2|Email address formatting error.|  
|3|Failed recipients error.|  
|4|Connection error.|  
|5|Other error.|  
|6|Operation timed out.|  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_Subscription server WMI class](sms_subscription-server-wmi-class.md)
