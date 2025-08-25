---
title: "ICIINFO::GetDependantPackages"
titleSuffix: Configuration Manager
description: The ICIINFO::GetDependantPackages method, in Configuration Manager, gets the dependent package information for the configuration item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 71274da9-00db-4854-b3e5-83a73da1c7e9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# ICIINFO::GetDependantPackages Method
The `ICIINFO::GetDependantPackages` method, in Configuration Manager, gets the dependent package information for the configuration item.

## Syntax

```
[IDL]
HRESULT GetDependantPackages(
     ULONG* pulNumDependants,
     struct CIPackageInfo** ppInfo
);
```

#### Parameters
 `pulNumDependants`
 Data type: `ULONG`

 Qualifiers: [out]

 Pointer to the number of dependent packages.

 `ppInfo`
 Data type: `CIPackageInfo`

 Qualifiers: [out]

 Pointer to a pointer to one [CIPackageInfo Structure](../../../../../develop/reference/core/clients/client-classes/cipackageinfo-structure.md) for each dependent package.

## Return Values
 An `HRESULT` code. Possible values include, but are not limited to, the following:

 S_OK
 The method succeeded. All other return values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
 [CIPackageInfo Structure](../../../../../develop/reference/core/clients/client-classes/cipackageinfo-structure.md)
