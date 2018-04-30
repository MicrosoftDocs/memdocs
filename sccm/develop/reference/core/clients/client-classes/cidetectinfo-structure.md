---
title: "CIDetectInfo Structure"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c719e7cf-481b-44ee-92db-60de1b4e5581
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CIDetectInfo Structure
In System Center Configuration Manager, the `CIDetectInfo` structure contains identity information for baseline configuration item detection.  

## Syntax  

```  
struct CIDetectInfo  
{  
      LPWSTR szCIID;  
      LPWSTR szVersion;  
};  
```  

## Members  
 szCIID  
 ID of the configuration item.  

 szVersion  
 Version of the configuration item.  

## See Also  
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)
