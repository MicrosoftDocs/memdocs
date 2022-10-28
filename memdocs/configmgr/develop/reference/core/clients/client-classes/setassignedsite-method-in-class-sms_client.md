---
description: Learn how the SetAssignedSite method, in Configuration Manager, sets the client's assigned site.
title: SetAssignedSite Methodt
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2a8b79cd-9aaa-4aff-a8cb-74d8b8102dfd
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SetAssignedSite Method in Class SMS_Client
The `SetAssignedSite` method, in Configuration Manager, sets the client's assigned site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 SetAssignedSite(  
     String sSiteCode  
);  
```  

#### Parameters  
 `sSiteCode`  
 Data type: `String`  

 Qualifiers: [in]  

 Site code to which the client is being assigned.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

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
 [SetGlobalLoggingConfiguration method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setgloballoggingconfiguration-method-in-class-sms_client.md)   
 [TriggerSchedule method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/triggerschedule-method-in-class-sms_client.md)
