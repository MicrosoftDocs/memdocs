---
title: "SMS_ClientDataSourcesContent Class"
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
ms.assetid: ae23d777-a5a2-48a6-b04f-fa1b8ab9284esearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ClientDataSourcesContent Server WMI Class
The `SMS_ClientDataSourcesContent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client content data sources per boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientDataSourcesContent : SMS_BaseClass  
{  
    UInt64 BranchCacheBytes;  
    UInt64 CloudDistributionPointBytes;  
    UInt64 DistributionPointBytes;  
    UInt32 DpSourceServerCount;  
    UInt64 PeerCacheBytes;  
    UInt32 SpSourceClientCount;  
};  

```  

## Methods  
 The `SMS_ClientDataSourcesContent` class does not define any methods.  

## Properties  
 `BranchCacheBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 Number of bytes from the branch cache.  

 `CloudDistributionPointBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 Number of bytes from cloud distribution points.  

 `DistributionPointBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 Number of bytes from distribution points.  

 `DpSourceServerCount`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Number of distribution points that served content.  

 `PeerCacheBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 Number of bytes from the peer cache.  

 `SpSourceClientCount`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Number of super peers that served content.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

-   Singleton  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Client Deployment Server WMI Classes](../../../../../develop/reference/core/clients/deploy/client-deployment-server-wmi-classes.md)
