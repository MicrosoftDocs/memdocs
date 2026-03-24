---
description: "Learn how to use the ICIIINFO::GetVersion method to get the version of the configuration item in Configuration Manager."
title: "ICIINFO::GetVersion"
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# ICIINFO::GetVersion Method
The `ICIINFO::GetVersion` method, in Configuration Manager, gets the version of the configuration item.

## Syntax

```
[IDL]
HRESULT GetVersion(
     LPWSTR* ppszVersion
);
```

#### Parameters
 `ppszVersion`
 Data type: `LPWSTR`

 Qualifiers: [out]

 Pointer to the version of the configuration item.

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
