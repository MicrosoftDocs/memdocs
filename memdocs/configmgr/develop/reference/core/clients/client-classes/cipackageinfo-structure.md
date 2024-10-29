---
title: CIPackageInfo Structure
titleSuffix: Configuration Manager
description: In Configuration Manager, the CIPackageInfo structure contains package information for a configuration item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 560625bf-5cd2-4cb0-8df8-d17951afabe7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CIPackageInfo Structure
In Configuration Manager, the `CIPackageInfo` structure contains package information for a configuration item.  

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
