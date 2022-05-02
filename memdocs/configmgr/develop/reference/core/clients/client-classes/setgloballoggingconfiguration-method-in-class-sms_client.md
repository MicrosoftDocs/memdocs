---
description: Learn how to define the global logging configuration for the client with SetGlobalLoggingConfiguration method.
title: "SetGlobalLoggingConfiguration Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e8bd00a9-c0a6-4b3c-9906-39fb2c342af4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetGlobalLoggingConfiguration Method in Class SMS_Client
The `SetGlobalLoggingConfiguration` method, in Configuration Manager, defines the global logging configuration for the client. This configuration represents either component-level logging or default logging if component-level logging is not defined.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 SetGlobalLoggingConfiguration(  
     UInt32 LogLevel,  
     UInt32 LogMaxSize,  
     UInt32 LogMaxHistory,  
     Boolean DebugLogging  
);  
```  

#### Parameters  
 `LogLevel`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The level of detail that the log will capture. Possible values are shown below. The default value is 1.  

| Value | Description |
| ----- | ----------- |
|0|Verbose logging|  
|1|Normal logging|  
|2|No logging|  

 `LogMaxSize`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The maximum size, in bytes, of a given log file.  

 `LogMaxHistory`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The number of incremented log files to accumulate before deleting. When this number has been reached, the creation of a new log file will result in the deletion of the oldest existing log file.  

 `DebugLogging`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if debug logging should be enabled. Debug logging is rarely used except for troubleshooting.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Remarks  
 This method manipulates registry keys. These keys should not be manipulated directly. However, for reference, these keys can be found at HKEY_LOCAL_MACHINE/Software/Microsoft/CCM/logging/@GLOBAL. Enabling debug logging with `DebugLogging` will result in the creation of a new key: HKEY_LOCAL_MACHINE/Software/Microsoft/CCM/logging/debuglogging.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMS_Client Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_client-client-wmi-class.md)   
 [EvaluateMachinePolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/evaluatemachinepolicy-method-in-class-sms_client.md)   
 [GetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/getassignedsite-method-in-class-sms_client.md)   
 [RequestMachinePolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/requestmachinepolicy-method-in-class-sms_client.md)   
 [ResetPolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/resetpolicy-method-in-class-sms_client.md)   
 [SetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setassignedsite-method-in-class-sms_client.md)   
 [TriggerSchedule method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/triggerschedule-method-in-class-sms_client.md)
