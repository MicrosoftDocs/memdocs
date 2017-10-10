---
title: "CCM_SoftwareCatalogUtilities Class"
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
ms.assetid: 30c0e8cd-bcf7-456f-9d1a-00358d7a75easearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_SoftwareCatalogUtilities Client WMI Class
The `CCM_SoftwareCatalogUtilities` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides a set of utility methods to assist in processing software updates.  

> [!IMPORTANT]
>  The software update client side SDK will only return set of updates which are deployed to client from Configuration Manager site server, and are applicable, and are yet to be installed on the client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_SoftwareCatalogUtilities :    
{  
};  
```  

## Methods  
 The following table lists the methods in the `CCM_SoftwareCatalogUtilities` class.  

-   [ApplyPolicyEx Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/applypolicyex-method-in-class-ccm_softwarecatalogutilities.md)  

-   [GetClientVersion Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/getclientversion-method-in-class-ccm_softwarecatalogutilities.md)  

-   [GetDeviceId Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/getdeviceid-method-in-class-ccm_softwarecatalogutilities.md)  

-   [GetPolicyState Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/getpolicystate-method-in-class-ccm_softwarecatalogutilities.md)  

-   [GetPortalUrlValue Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/getportalurlvalue-method-in-class-ccm_softwarecatalogutilities.md)  

-   [VerifySignature Method in Class CCM_SoftwareCatalogUtilities](../../../../../develop/reference/core/clients/sdk/verifysignature-method-in-class-ccm_softwarecatalogutilities.md)  

## Properties  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
