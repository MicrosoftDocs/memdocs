---
title: "IDCMSDK::GetAssignedBaselines"
titleSuffix: Configuration Manager
description: "In Configuration Manager, the IDCMSDK::GetAssignedBaselines method enumerates assigned baseline configuration items."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 89d3dda9-be5d-43fc-a20d-9267531a4ddd
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# IDCMSDK::GetAssignedBaselines Method
The `IDCMSDK::GetAssignedBaselines` method, in Configuration Manager, enumerates assigned baseline configuration items.

## Syntax

```
[IDL]
HRESULT GetAssignedBaselines(
     IEnumUnknown**  ppEnum,
     ULONG*  pulNumCIs,
     struct CIDetectInfo**  ppInfo
);
```

#### Parameters
 `ppEnum`
 Data type: `IEnumUnknown`

 Qualifiers: [out]

 Pointer to a pointer to an enumeration object containing an [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md) for each baseline configuration item currently assigned and downloaded to the client.

 `pulNumCIs`
 Data type: `ULONG`

 Qualifiers: [out]

 Pointer to the number of baseline configuration items. On successful return from the method, this parameter also indicates the number of other configuration items currently assigned to the client.

 `ppInfo`
 Data type: `struct`

 Qualifiers: [out, size_is(,*pulNumCIs)]

 Pointer to a pointer to a [CIDetectInfo Structure](../../../../../develop/reference/core/clients/client-classes/cidetectinfo-structure.md) containing information for each baseline configuration item that is assigned but not downloaded.

## Return Values
 An `HRESULT` code. Possible values include, but are not limited to, the following:

 S_OK
 The method succeeded. All other values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
 [CIDetectInfo Structure](../../../../../develop/reference/core/clients/client-classes/cidetectinfo-structure.md)
