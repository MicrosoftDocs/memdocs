---
title: "CIPackageInfo Structure"
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
ms.assetid: 560625bf-5cd2-4cb0-8df8-d17951afabe7searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CIPackageInfo Structure
In System Center Configuration Manager, the `CIPackageInfo` structure contains package information for a configuration item.  

## Syntax  

```  
struct CIPackageInfo  
{  
      LPWSTR szTypeName;  
      LPWSTR szPackageName;  
      LPWSTR szPackageVersion;  
      LPWSTR szNamespace;  
};  
```  

## Members  
 szTypeName  
 Name of the configuration item.  

 szPackageName  
 Name of the package.  

 szPackageVersion  
 Version of the package.  

 szNamespace  
 Namespace used by the package software.  

## See Also  
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)   
 [ICIINFO::GetDependantPackages Method](../../../../../develop/reference/core/clients/client-classes/iciinfo--getdependantpackages-method.md)
