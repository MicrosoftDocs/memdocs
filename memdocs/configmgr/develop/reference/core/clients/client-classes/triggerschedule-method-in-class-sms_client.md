---
title: TriggerSchedule Method
titleSuffix: Configuration Manager
description: Trigger the client to run a specific schedule.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a4e13dea-899a-4d9e-8e5b-60b7f81c0c45
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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

 Complete GUID List:  

|Schedule  |GUID  |
|---------|---------|
|Hardware Inventory|{00000000-0000-0000-0000-000000000001}|
|Software Inventory|{00000000-0000-0000-0000-000000000002}|
|Data Discovery Record|{00000000-0000-0000-0000-000000000003}|
|File Collection|{00000000-0000-0000-0000-000000000010}|
|IDMIF Collection|{00000000-0000-0000-0000-000000000011}|
|Client Machine Authentication|{00000000-0000-0000-0000-000000000012}|
|Machine Policy Assignments Request|{00000000-0000-0000-0000-000000000021}|
|Machine Policy Evaluation|{00000000-0000-0000-0000-000000000022}|
|Refresh Default MP Task|{00000000-0000-0000-0000-000000000023}|
|LS (Location Service) Refresh Locations Task|{00000000-0000-0000-0000-000000000024}|
|LS (Location Service) Timeout Refresh Task|{00000000-0000-0000-0000-000000000025}|
|Policy Agent Request Assignment (User)|{00000000-0000-0000-0000-000000000026}|
|Policy Agent Evaluate Assignment (User)|{00000000-0000-0000-0000-000000000027}|
|Software Metering Generating Usage Report|{00000000-0000-0000-0000-000000000031}|
|Source Update Message|{00000000-0000-0000-0000-000000000032}|
|Clearing proxy settings cache|{00000000-0000-0000-0000-000000000037}|
|Machine Policy Agent Cleanup|{00000000-0000-0000-0000-000000000040}|
|User Policy Agent Cleanup|{00000000-0000-0000-0000-000000000041}|
|Policy Agent Validate Machine Policy / Assignment|{00000000-0000-0000-0000-000000000042}|
|Policy Agent Validate User Policy / Assignment|{00000000-0000-0000-0000-000000000043}|
|Retrying/Refreshing certificates in AD on MP|{00000000-0000-0000-0000-000000000051}|
|Peer DP Status reporting|{00000000-0000-0000-0000-000000000061}|
|Peer DP Pending package check schedule|{00000000-0000-0000-0000-000000000062}|
|SUM Updates install schedule|{00000000-0000-0000-0000-000000000063}|
|Hardware Inventory Collection Cycle|{00000000-0000-0000-0000-000000000101}|
|Software Inventory Collection Cycle|{00000000-0000-0000-0000-000000000102}|
|Discovery Data Collection Cycle|{00000000-0000-0000-0000-000000000103}|
|File Collection Cycle|{00000000-0000-0000-0000-000000000104}|
|IDMIF Collection Cycle|{00000000-0000-0000-0000-000000000105}|
|Software Metering Usage Report Cycle|{00000000-0000-0000-0000-000000000106}|
|Windows Installer Source List Update Cycle|{00000000-0000-0000-0000-000000000107}|
|Software Updates Assignments Evaluation Cycle|{00000000-0000-0000-0000-000000000108}|
|Branch Distribution Point Maintenance Task|{00000000-0000-0000-0000-000000000109}|
|Send Unsent State Message|{00000000-0000-0000-0000-000000000111}|
|State System policy cache cleanout|{00000000-0000-0000-0000-000000000112}|
|Scan by Update Source|{00000000-0000-0000-0000-000000000113}|
|Update Store Policy|{00000000-0000-0000-0000-000000000114}|
|State system policy bulk send high|{00000000-0000-0000-0000-000000000115}|
|State system policy bulk send low|{00000000-0000-0000-0000-000000000116}|
|Application manager policy action|{00000000-0000-0000-0000-000000000121}|
|Application manager user policy action|{00000000-0000-0000-0000-000000000122}|
|Application manager global evaluation action|{00000000-0000-0000-0000-000000000123}|
|Power management start summarizer|{00000000-0000-0000-0000-000000000131}|
|Endpoint deployment reevaluate|{00000000-0000-0000-0000-000000000221}|
|Endpoint AM policy reevaluate|{00000000-0000-0000-0000-000000000222}|
|External event detection|{00000000-0000-0000-0000-000000000223}|


## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## Examples 

### Example 1: Trigger hardware inventory via PowerShell using the `WMICLASS` type accelerator

```powershell
([wmiclass]"root\ccm:SMS_Client").TriggerSchedule("{00000000-0000-0000-0000-000000000001}")
```

### Example 2: Trigger location service refresh task via PowerShell using the Invoke-CIMMethod method

```powershell
Invoke-CimMethod -Namespace 'root\CCM' -ClassName SMS_Client -MethodName TriggerSchedule -Arguments @{sScheduleID='{00000000-0000-0000-0000-000000000024}'}
```
### Example 3: Trigger Software Update Scan cache deletion and scan via Command Prompt using WMIC

```batchfile
%windir%\System32\wbem\WMIC.exe /namespace:\\root\ccm\invagt path inventoryActionStatus where InventoryActionID="{00000000-0000-0000-0000-000000000113}" DELETE /NOINTERACTIVE
%windir%\System32\wbem\WMIC.exe /namespace:\\root\ccm path sms_client CALL TriggerSchedule "{00000000-0000-0000-0000-000000000113}" /NOINTERACTIVE
```

## See also

 [SMS_Client Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_client-client-wmi-class.md)   
 [EvaluateMachinePolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/evaluatemachinepolicy-method-in-class-sms_client.md)   
 [GetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/getassignedsite-method-in-class-sms_client.md)   
 [RequestMachinePolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/requestmachinepolicy-method-in-class-sms_client.md)   
 [ResetPolicy method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/resetpolicy-method-in-class-sms_client.md)   
 [SetAssignedSite method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setassignedsite-method-in-class-sms_client.md)   
 [SetGlobalLoggingConfiguration method in Class SMS_Client](../../../../../develop/reference/core/clients/client-classes/setgloballoggingconfiguration-method-in-class-sms_client.md)
