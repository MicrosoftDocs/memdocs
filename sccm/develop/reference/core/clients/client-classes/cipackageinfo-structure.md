---
title: "CIPackageInfo Structure"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 560625bf-5cd2-4cb0-8df8-d17951afabe7
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
