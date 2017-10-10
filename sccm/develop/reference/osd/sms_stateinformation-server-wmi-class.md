---
title: "SMS_StateInformation Class"
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
ms.assetid: 7cf84467-bfe5-4517-8cec-c6a6380850cfsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_StateInformation Server WMI Class
The `SMS_StateInformation` WMI class is an SMS Provider server class, in Configuration Manager, that provides information about a state message.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StateInformation : SMS_BaseClass  
{  
      String StateDescription;  
      UInt32 StateID;  
      String StateName;  
      UInt32 TopicType;  
};  
```  

## Methods  
 The `SMS_StateInformation` class does not define any methods.  

## Properties  
 `StateDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the state.  

 `StateID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the state.  

 `StateName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the state.  

 `TopicType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 State message topic type. Possible values are:  

|||  
|-|-|  
|500|Software update detection|  
|501|Software update scan status|  
|403|Settings management scan status|  
|401|Settings Management compliance|  
|402|Software updates installation|  
|300|Software updates or desired configuration management assignment compliance|  
|301|Software updates assignment enforcement (installation)|  
|302|Software updates or desired configuration management assignment evaluation|  
|200|NAP|  
|100|State migration (server only)|  
|600|PXE (server only)|  
|700|State system resync (server only)|  
|701|State system heartbeat (server only)|  
|800|Client deployment FSP|  
|801|Device client deployment FSP|  
|900|Branch distribution point status|  
|502|WSUS synch status|  
|1000,1001|Client health state (FSP)|  
|1002,1003,1004|Device client health state (FSP)|  
|1100|Client mode readiness state|  
|702|ClientKeyData updates (server only)|  
|1500, 1501|CAL tracking (user)|  
|1502, 1503|CAL tracking (computer)|  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class allows you to access information about a Configuration Manager state message. These messages are sent by clients to notify of important changes of state. Each message provides a snapshot of the state of a process at a specific time. These messages can be helpful when troubleshooting or verifying that processes are working correctly.  

 State messages are used with software updates, Network Access Protection (NAP), desired configuration management, client deployment, and client communication. Generally you will use state messages only through reports and client logs.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)
