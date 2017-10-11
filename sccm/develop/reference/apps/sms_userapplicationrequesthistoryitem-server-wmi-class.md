---
title: "SMS_UserApplicationRequestHistoryItem Class"
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
ms.assetid: 4d140550-c95a-4367-8d24-b0704de33c0asearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UserApplicationRequestHistoryItem Server WMI Class
The `SMS_UserApplicationRequestHistoryItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an update to an instance of `SMS_UserApplicationRequest`.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserApplicationRequestHistoryItem :    
{  
    String Comments;  
    String ModifiedBy;  
    DateTime ModifiedDate;  
    UInt32 State;  
};  
```  

## Methods  
 The `SMS_UserApplicationRequestHistoryItem` class does not define any methods.  

## Properties  
 `Comments`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Comments entered to explain why the change occurred. These could be user’s comment explaining why they are requesting the application or approver comments explaining why the application was approved or denied.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The user who made the change to the request.  

 `ModifiedDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The date when the change to the request was made.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The state of the request after the change was made. Possible values are:  

|||  
|-|-|  
|1|Requested|  
|2|Canceled|  
|3|Denied|  
|4|Approved|  

## Remarks  

## Requirements  
 Each time a request is updated, an instance of this class is created to track the history of the request.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserApplicationRequest Server WMI Class](../../../develop/reference/apps/sms_userapplicationrequest-server-wmi-class.md)
