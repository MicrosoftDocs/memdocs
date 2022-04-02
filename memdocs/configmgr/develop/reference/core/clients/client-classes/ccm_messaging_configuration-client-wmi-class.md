---
title: "CCM_Messaging_Configuration Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the CCM_Messaging_Configuration class is a client WMI class that supports messaging-related settings that are exposed to administrators."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cc2afe45-3c53-4f4e-a353-c75552a3410c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Messaging_Configuration Client WMI Class
In Configuration Manager, the `CCM_Messaging_Configuration` class is a client Windows Management Instrumentation (WMI) class that supports messaging-related settings that are exposed to administrators.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Messaging_Configuration : CCM_Policy  
{  
      UInt8 DummyKey;  
      String MessageRetrySpec;  
      UInt32 MessageSizeThreshold;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
};  
```  

## Methods  
 The `CCM_Messaging_Configuration` class does not define any methods.  

## Properties  
 `DummyKey`  
 Data type: `UInt8`  

 Access type: Read/Write  

 Qualifiers: [RealKey]  

 Dummy key.  

 `MessageRetrySpec`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional field that specifies a list of retry intervals, in minutes. The messaging system uses this when an outgoing message has to be retried. The format of this field is a semicolon-delimited list of integers, such as 1;5;30;60. In the previous example, if a message cannot be delivered due to a transient error, it is retried after 1 minute, then 5 minutes, then 30 minutes, and finally 60 minutes; until the message times out or is successfully delivered. All subsequent retries use the last value in the list (60 minutes in this example). If this field is omitted or incorrectly formatted, the service falls back to using internally hard coded defaults.  

 `MessageSizeThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Maximum allowed size of messages, in kilobytes. If a message exceeds this threshold and BITS is enabled and the message is transferred using BITS, otherwise the message is transferred using HTTP.  

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

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
