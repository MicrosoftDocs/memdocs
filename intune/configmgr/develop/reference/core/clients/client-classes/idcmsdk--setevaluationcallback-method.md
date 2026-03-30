---
title: "IDCMSDK::SetEvaluationCallback"
description: "In Configuration Manager, the IDCMSDK::SetEvaluationCallback method associates a callback object with an existing evaluation job specified by job ID."
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# IDCMSDK::SetEvaluationCallback Method
The `IDCMSDK::SetEvaluationCallback` method, in Configuration Manager, associates a callback object with an existing evaluation job, specified by job ID.

## Syntax

```
[IDL]
HRESULT SetEvaluationCallback(
     JobIdRef  jobId,
     IDCMAgentCallback*  pCallback
);
```

#### Parameters
 `jobId`
 Data type: `JobIdRef`

 Qualifiers: [in]

 ID of the evaluation job to retrieve.

 `pCallback`
 Data type: `IDCMAgentCallback`

 Qualifiers: [in]

 Pointer to an [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md) object. This parameter can be set to `null` if no callback is available.

## Return Values
 An `HRESULT` code. Possible values include, but are not limited to, the following:

 S_OK
 The method succeeded. All other return values indicate failure.

## Remarks
 The typical way to use this method is to pass `null` for the `pCallback` parameter.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
