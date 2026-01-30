---
title: VerifySignature Method
description: In Configuration Manager, the VerifySignature WMI class method verifies the data signature.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# VerifySignature Method in Class CCM_SoftwareCatalogUtilities
The `VerifySignature` Windows Management Instrumentation (WMI) class method in Configuration Manager that verifies the data signature.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 VerifySignature
{
    [IN]    String Data
    [IN]    String DataSignature
    [IN]    String WebServiceID
    [IN]    Boolean VerifyUserAndTimestamp
    [OUT]   Boolean SignatureVerificationPassed
};
```

## Parameters
 `Data`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Data to verify.

 `DataSignature`
 Data type: `String`

 Qualifiers: [id("1"), in]

 Data signature.

 `WebServiceID`
 Data type: `String`

 Qualifiers: [id("2"), in]

 Web Service identifier.

 `VerifyUserAndTimestamp`
 Data type: `Boolean`

 Qualifiers: [id("3"), in]

 `true` to verify the user and timestamp.

 `SignatureVerificationPassed`
 Data type: `Boolean`

 Qualifiers: [id("4"), out]

 `true` if the data signature is valid.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
