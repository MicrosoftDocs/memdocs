---
title: "CCM_Service_EndpointConfiguration Class"
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
ms.assetid: 2c1a08fa-687a-4a62-87d3-bf1699a3a01csearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_Service_EndpointConfiguration Client WMI Class
> [!IMPORTANT]
>  This class supports the Configuration Manager 2007 infrastructure; any access to this class or class properties should be read-only.  

 In System Center Configuration Manager, the `CCM_Service_EndpointConfiguration` class is a client Windows Management Instrumentation (WMI) class that supports endpoint configuration for the CCMEXEC service. There is an instance of this class for each endpoint on the computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Service_EndpointConfiguration : CCM_Policy  
{  
      String ACL;  
      UInt32 ActiveMessageThreshold;  
      String CoClass;  
      String Concurrency;  
      String DisplayName;  
      Boolean ManualStart;  
      UInt32 MessageTimeout;  
      String Name;  
      String NotificationQueries[];  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      UInt32 ReleaseTimeout;  
      String ThreadType;  
      String Visibility;  
};  
```  

## Methods  
 The `CCM_Service_EndpointConfiguration` class does not define any methods.  

## Properties  
 `ACL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Value indicating the management point. This value might be null, empty, A (for an assigned management point), L (for a local management point), or AL (for both). This is an optional parameter.  

 `ActiveMessageThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The number of messages that can be processed concurrently in a parallel endpoint.  

 `CoClass`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 `ClassID` or `ProgID` of the COM class that implements the endpoint. This is a required field.  

 `Concurrency`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Concurrency level of the endpoint.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Display name of the endpoint for when it is displayed in a user interface. This is an optional field.  

 `ManualStart`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Flag indicating whether the delivery of messages should be started manually. If this flag is set, the service will not dispatch messages to the endpoint until it is explicitly started by using the **StartEndpoint** system command.  

 `MessageTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional. Message timeout, in minutes.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Realkey]  

 Name of the endpoint that is used for addressing. This is a required field and must be unique for the computer.  

 `NotificationQueries`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of notification queries (optional parameter).  

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

 `ReleaseTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional. Release timeout, in minutes.  

 `ThreadType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Thread type on which the endpoint should be invoked.  

 `Visibility`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Flag indicating that the endpoint is public. Public endpoints can receive messages from remote computers. Possible values are:  

 internal -  No remote messages.  

 signed  - Remote messages must be signed by a management point in mixed or native mode. Used on some client endpoints that receive replies from a management point.  

 clientsigned -Remote messages must be signed by a client in native mode. Used on some management point endpoints.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
