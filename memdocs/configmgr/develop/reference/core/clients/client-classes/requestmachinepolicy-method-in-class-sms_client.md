---
title: RequestMachinePolicy Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the RequestMachinePolicy method initiates a request for machine policy.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3a2d4d06-074f-4174-9398-e3df3d230414
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RequestMachinePolicy Method in Class SMS_Client
The `RequestMachinePolicy` method, in Configuration Manager, initiates a request for machine policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 RequestMachinePolicy(  
      UInt32 uFlags  
);  
```  

#### Parameters  
 `uFlags`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Flags identifying the policy. Possible values are:  

| Value | Description |
| ----- | ----------- |
|0|A machine policy retrieval cycle is initiated.|  
|1|A machine policy validation cycle is initiated, and the server and client cyclical redundancy checks (CRCs) are compared to verify that the policies are in agreement. If the policies are not in agreement, then a resynchronization is initiated.|  

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
 [ResetPolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/resetpolicy-method-in-class-sms_client.md)   
 [SetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setassignedsite-method-in-class-sms_client.md)   
 [SetGlobalLoggingConfiguration method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setgloballoggingconfiguration-method-in-class-sms_client.md)   
 [TriggerSchedule method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/triggerschedule-method-in-class-sms_client.md)
