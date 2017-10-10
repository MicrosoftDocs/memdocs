---
title: "SMS_CH_SummaryHistory Class"
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
ms.assetid: 91fa4d66-d2cb-4fac-abeb-2b95508bbc2asearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CH_SummaryHistory Server WMI Class
The `SMS_CH_SummaryHistory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the client summary history.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CH_SummaryHistory : SMS_BaseClass  
{  
    UInt32 ClientsActive;  
    UInt32 ClientsActiveHealthyOrActiveNoResults;  
    UInt32 ClientsHealthy;  
    UInt32 ClientsInactive;  
    UInt32 ClientsRemediationSuccess;  
    UInt32 ClientsRemediationTotal;  
    UInt32 ClientsTotal;  
    UInt32 ClientsUnhealthy;  
    String CollectionID;  
    DateTime Date;  
    String SiteCode;  
};  
```  

## Methods  
 The `SMS_CH_SummaryHistory` class does not define any methods.  

## Properties  
 `ClientsActiveHealthyOrActiveNoResults`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of active, healthy clients and active clients with no results.  

 `ClientsActive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of active clients.  

 `ClientsHealthy`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of healthy clients.  

 `ClientsInactive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of inactive clients.  

 `ClientsRemediationSuccess`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of successfully remediated clients.  

 `ClientsRemediationTotal`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of remediated clients (successful and unsuccessful).  

 `ClientsTotal`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of clients.  

 `ClientsUnhealthy`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of unhealthy clients.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated ID containing eight characters that identifies the collection.  

 `Date`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The summary date.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Three-letter site code of the site.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Client Status Server WMI Classes](../../../../../develop/reference/core/clients/status/client-status-server-wmi-classes.md)
