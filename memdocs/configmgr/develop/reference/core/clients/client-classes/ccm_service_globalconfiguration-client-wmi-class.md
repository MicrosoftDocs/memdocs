---
title: "CCM_Service_GlobalConfiguration Class"
description: Learn how the CCM_Service_GlobalConfiguration class is a client Windows Management Instrumentation (WMI) class that supports global configuration for the CCMEXEC service.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 62d6b768-bf45-4bca-b36c-eeec8fcc3caf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Service_GlobalConfiguration Client WMI Class
In Configuration Manager, the `CCM_Service_GlobalConfiguration` class is a client Windows Management Instrumentation (WMI) class that supports global configuration for the CCMEXEC service. There is only one instance of this class on a computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Service_GlobalConfiguration : CCM_Policy  
{  
      UInt8 Dummy;  
      UInt32 EndpointActiveMessageThreshold;  
      UInt32 EndpointMessageTimeout;  
      UInt32 EndpointReleaseTimeout;  
      UInt32 OutgoingMessageTimeout;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      String ServiceRootDir;  
};  
```  

## Methods  
 The `CCM_Service_GlobalConfiguration` class does not define any methods.  

## Properties  
 `Dummy`  
 Data type: `UInt8`  

 Access type: Read/Write  

 Qualifiers: [Realkey]  

 Dummy key.  

 `EndpointActiveMessageThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Default maximum number of outstanding messages that endpoints are allowed. A message is outstanding if it has been dispatched to the endpoint, but the endpoint has not called **SetComplete** on the associated context. For serial endpoints, the AMT is always 1. This can be overridden on a per-endpoint basis.  

 `EndpointMessageTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Default timeout, in minutes, assigned to all messages that arrive for endpoints. If the value is NULL or 0, no default timeout is assigned. This can be overridden on a per-endpoint basis.  

 `EndpointReleaseTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Endpoint defaults. The default idle time, in minutes, that endpoints are allowed before they are released by the service. An endpoint is idle when no messages are being dispatched to it. If the value is NULL or 0, endpoints are not released until the service shuts down. This can be overridden on a per-endpoint basis in the endpoint's configuration.  

 `OutgoingMessageTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Service defaults. The default timeout, in minutes, that all messages sent from the computer are assigned. If the value is NULL or 0, no default timeout is assigned. This can be overridden on a per-message basis by using the **Timeout** property of the message.  

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

 `ServiceRootDir`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Root directory that the service uses internally for temporary files. The System and Administrators account must have full access to this directory (the latter is to allow the debugging of CCMEXEC as an application). The service creates this directory if it does not exist.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
