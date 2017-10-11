---
title: "SMS_ClientBaselineStatus Class"
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
ms.assetid: fbc0259a-4be5-4157-985d-fb387060e4f1searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ClientBaselineStatus Server WMI Class
The `SMS_ClientBaselineStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment baseline status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientBaselineStatus: SMS_BaseClass  
{  
    UInt32 BaselineType;  
    String InstalledClientVersion;  
    UInt32 LastErrorCode;      
    UInt32 ResourceID;  
    String  SMSID;  
    UInt32 Status;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_ClientBaselineStatus` class.  

|Method|Description|  
|------------|-----------------|  
|[GetClientBaselineStatusSummary Method in Class SMS_ClientBaselineStatus](../../../../../develop/reference/core/clients/deploy/getclientbaselinestatussummary-method-in-class-sms_clientbaselinestatus.md)|Gets baseline status summary information by BaselineType and CollectionID.|  

## Properties  
 `BaselineType`  
 Data type: `uint32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The client baseline type. Possible values are:  

|||  
|-|-|  
|1|Production|  
|2|Staging|  

 `InstalledClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Client version that deployed through client deployment.  

 `LastErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last error code sent by the client.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Resource ID of the client.  

 `SMSID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The SMSID of the client.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The status of the client against the client baseline. Possible values are:  

|||  
|-|-|  
|1|Compliant|  
|2|InProgress|  
|3|NotCompliant|  
|4|CriticalError|  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Client Deployment Server WMI Classes](../../../../../develop/reference/core/clients/deploy/client-deployment-server-wmi-classes.md)
