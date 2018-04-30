---
title: "CCM_Service_SystemTaskConfiguration Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d7864ef9-16f6-4c98-afe6-7d4a21275263
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_Service_SystemTaskConfiguration Client WMI Class
> [!IMPORTANT]
>  This class supports the Configuration Manager 2007 infrastructure and is not intended to be used directly from your code.  

 In System Center Configuration Manager, the `CCM_Service_SystemTaskConfiguration` class is a client Windows Management Instrumentation (WMI) class that supports system task configuration for the CCMEXEC service.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Service_SystemTaskConfiguration : CCM_Policy  
{  
      String CoClass;  
      String DisplayName;  
      String Event;  
      String Name;  
      UInt32 Order;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      String ThreadType;  
};  
```  

## Methods  
 The `CCM_Service_SystemTaskConfiguration` class does not define any methods.  

## Properties  
 `CoClass`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Class ID or program ID of the COM class that implements the system task.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Display name of the system task.  

 `Event`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Event on which the system task should be invoked.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Realkey]  

 Name of the system task, which must be unique on the computer.  

 `Order`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Order value of the task. Tasks with lower order values run before tasks with higher values. Tasks with the same order value run simultaneously (no ordering between them is guaranteed).This value defaults to 0 if a value is not specified.  

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

 `ThreadType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Thread type on which the endpoint should be invoked.  

## Remarks  
 There is an instance of this class for each system task on the computer.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
