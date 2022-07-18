---
description: Learn how to use CCM_ServiceBITSConfiguration class which supports BITS-related settings used by CCMEXEC for uploading and downloading message payloads.
title: "CCM_Service_BITSConfiguration Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f7b19c4c-da0a-45ff-b07e-a0922afeb682
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Service_BITSConfiguration Client WMI Class
In Configuration Manager, the `CCM_Service_BITSConfiguration` class is a client Windows Management Instrumentation (WMI) class that supports Background Intelligent Transfer Service (BITS)-related settings used by CCMEXEC for uploading and downloading message payloads. The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Service_BITSConfiguration : CCM_Policy  
{  
      UInt8 DummyKey;  
      UInt32 MinimumRetryDelay;  
      UInt32 NoProgressTimeout;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
};  
```  

## Methods  
 The `CCM_Service_BITSConfiguration` class does not define any methods.  

## Properties  
 `DummyKey`  
 Data type: `UInt8`  

 Access type: Read/Write  

 Qualifiers: None  

 This value is used as the WMI key for a singleton policy and has no other effect.  

 `MinimumRetryDelay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Retry delay to pass to BITS when uploading or downloading message payloads (in minutes). If the value is 0 or `null`, BITS defaults are used.  

 `NoProgressTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 No-progress timeout to pass to BITS when uploading or downloading message payloads (in minutes). If the value is `null` or 0, BITS defaults are used.  

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

 Qualifiers: Key  

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

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)   
 [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md)
