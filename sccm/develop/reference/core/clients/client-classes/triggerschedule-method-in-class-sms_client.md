---
title: "TriggerSchedule Method"
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
ms.assetid: a4e13dea-899a-4d9e-8e5b-60b7f81c0c45searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# TriggerSchedule Method in Class SMS_Client
The `TriggerSchedule` method, in Configuration Manager, triggers the client to run the specified schedule.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 TriggerSchedule(  
     String sScheduleID  
);  
```  

#### Parameters  
 `sScheduleID`  
 Data type: `String`  

 Qualifiers: [in]  

 GUID of the schedule to be triggered.  

 Example GUIDs:  

 Hardware Inventory  

 {00000000-0000-0000-0000-000000000001}  

 Software Inventory  

 {00000000-0000-0000-0000-000000000002}  

 Data Discovery Record  

 {00000000-0000-0000-0000-000000000003}  

 File Collection  

 {00000000-0000-0000-0000-000000000010}  

 Machine Policy Assignments Request  

 {00000000-0000-0000-0000-000000000021}  

 Machine Policy Evaluation  

 {00000000-0000-0000-0000-000000000022}  

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
 [SetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setassignedsite-method-in-class-sms_client.md)   
 [SetGlobalLoggingConfiguration method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setgloballoggingconfiguration-method-in-class-sms_client.md)
