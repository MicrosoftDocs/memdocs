---
title: CCM_Scheduler_ScheduledMessage Class
titleSuffix: Configuration Manager
description: A client Windows Management Instrumentation class that represents the configuration for a scheduled message.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bb58b677-85f9-4888-8d6d-5e5e8379b05e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_Scheduler_ScheduledMessage Client WMI Class
In Configuration Manager, the `CCM_Scheduler_ScheduledMessage` class is a client Windows Management Instrumentation (WMI) class that represents the configuration for a scheduled message. There is an instance of this class for each scheduled message.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Scheduler_ScheduledMessage : CCM_Policy  
{  
      String ActiveMessage;  
      DateTime ActiveTime;  
      Boolean ActiveTimeIsGMT;  
      UInt32 DeadlineMinutes;  
      String DeliverMode;  
      String ExpireMessage;  
      DateTime ExpireTime;  
      Boolean ExpireTimeIsGMT;  
      UInt32 LaunchConditions;  
      String MessageName;  
      String MessageTimeout;  
      UInt32 Order;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      String ReplyToEndpoint;  
      String ScheduledMessageID;  
      String TargetEndpoint;  
      String TriggerMessage;  
      String Triggers[];  
};  
```  

## Methods  
 The `CCM_Scheduler_ScheduledMessage` class does not define any methods.  

## Properties  
 `ActiveMessage`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Message to send when the schedule becomes active. If the value is omitted, no message is sent to the target endpoint.  

 `ActiveTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the schedule becomes active.  

 `ActiveTimeIsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if ActiveTime is in Universal Coordinated Time (UTC). If the value is omitted or set to FALSE, the time specifies the client computer's local time.  

 `DeadlineMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Defines how long the schedule will be on hold if its launch conditions are not met. The default value is 4320 minutes (3 days).  

 `DeliverMode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Mode set for every message delivered under the schedule. Possible values are:  

- Express  

- Recoverable  

  `ExpireMessage`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  Message to send when the schedule expires. If the value is omitted, no message is sent to the target endpoint.  

  `ExpireTime`  
  Data type: `DateTime`  

  Access type: Read/Write  

  Qualifiers: None  

  Date and time when the schedule expires.  

  `ExpireTimeIsGMT`  
  Data type: `Boolean`  

  Access type: Read/Write  

  Qualifiers: None  

  `true` if `ExpireTime` is in Universal Coordinated Time (UTC). If the value is omitted or set to `false`, the time specifies the client computer's local time.  

  `LaunchConditions`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: None  

  Defines the system resource conditions to fire this schedule. The default value is 1. Possible values are a combination of the following:  

| Value | Launch Condition type |
| ----- | --------------------- |
|0|eTaskCondition_None|  
|1|eTaskCondition_AboveCriticalBattery|  
|2|eTaskCondition_AboveLowBattery|  
|4|eTaskCondition_OnAC|  
|8|eTaskCondition_Idle|  
|16|eTaskCondition_NetworkConnected|  

> [!IMPORTANT]
>  Only one of these power conditions should be supplied in the schedule policy. If more than one is supplied, we honor:  
>   
>  OnAC > AboveLowBattery > AboveCriticalBattery  

 `MessageName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name to set for every message delivered under the schedule. If the value is omitted, this property is not set on the message.  

 `MessageTimeout`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Timeout set for every message delivered under the schedule. If the value is omitted or set to 0, the timeout is set to INFINITE.  

 `Order`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Defines the order of the firing if multiple schedules were waiting on conditions and now all the conditions have been met. The smaller the number, the higher the priority. The default value is 4294967295 (0xFFFFFFFF).  

 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyPrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyRuleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `ReplyToEndpoint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reply-to endpoint set for every message delivered under the schedule. If the value is omitted, this property is not set on the message.  

 `ScheduledMessageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifier: [RealKey, Not_Null]  

 ID of the scheduled message, which can be any unique string.  

 `TargetEndpoint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Endpoint address to send messages to when a trigger fires or when activation/expiration occurs. This address is relative to the computer on which the scheduler evaluates the schedule.  

 `TriggerMessage`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Message to send when a trigger on the schedule occurs. If the value is omitted, an empty message is sent to the target endpoint.  

 `Triggers`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of trigger strings that define when the message should be sent.  

### Syntax  

```  

<TriggerString> := <TriggerType> [ ';' <Name> '=' <Value>]*  

<TriggerType> :=  The type of  trigger.  
<Name> := Name of a property defined by the trigger type.  
<Value> := Value of the property.  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Scheduling Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/scheduling-client-wmi-classes.md)   
 [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md)
