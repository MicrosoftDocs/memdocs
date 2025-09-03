---
description: The IDCMSDK::EvaluateBaseline method, in Configuration Manager, runs the discover operation for the specified baseline configuration item.
title: "IDCMSDK::EvaluateBaseline"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e66ba88a-2b78-4b36-b932-ac15d144291e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# IDCMSDK::EvaluateBaseline Method
The `IDCMSDK::EvaluateBaseline` method, in Configuration Manager, runs the discover operation for the specified baseline configuration item.

## Syntax

```
[IDL]
HRESULT EvaluateBaseline(
     const struct CIDetectInfo* pInfo,
     IDCMAgentCallback*  pCallback,
     BOOL  bForce,
     JobId*  pJobId
);
```

#### Parameters
 `pInfo`
 Data type: `struct`

 Qualifiers: [in]

 Pointer to a [CIDetectInfo Structure](../../../../../develop/reference/core/clients/client-classes/cidetectinfo-structure.md) containing information about the baseline configuration item.

 `pCallback`
 Data type: `IDCMAgentCallback`

 Qualifiers: [in]

 Pointer to an [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md) object that is used to notify the agent of the progress, completion, or failure of the operation.

 `bForce`
 Data type: `BOOL`

 Qualifiers: [in]

 `true` if the method is to force the evaluation scan of the baseline configuration item. This value requires administrator privileges.

 A setting of `false` for this parameter allows the scan to run, but it doesn't run if the last evaluation of the baseline met the Desired Configuration Management TimeToLive threshold.

 `pJobId`
 Data type: `JobId`

 Qualifiers: [out]

 Pointer to the ID of the new Desired Configuration Management Agent job for the baseline configuration item.

## Return Values
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:

 S_OK
 The method succeeded. All other return values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
 [CIDetectInfo Structure](../../../../../develop/reference/core/clients/client-classes/cidetectinfo-structure.md)
