---
title: "SMS_ClientDeploymentFailureBucket Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8a5608be-1f8a-4aea-a87c-e2b379c98107searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ClientDeploymentFailureBucket Server WMI Class
The  `SMS_ClientDeploymentFailureBucket` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment failure bucket that is used to get the total number of clients with the same failed state message ID.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientDeploymentFailureBucket: SMS_BaseClass  
{  
    UInt32 ClientCount;  
    String CollectionID;  
    UInt32 LastMessageStateID;  
};  

```  

## Methods  
 The  `SMS_ClientDeploymentFailureBucket` class does not define any methods.  

## Properties  
 `ClientCount`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 The total number of clients with the specified LastMessageStateID.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The ID of the collection of which the clients are members.  

 `LastMessageStateID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The ID of the last client deployment state message.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Client Deployment Server WMI Classes](../../../../../develop/reference/core/clients/deploy/client-deployment-server-wmi-classes.md)
