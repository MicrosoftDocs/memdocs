---
title: "ITSEnvClass::GetVariables"
description: In Configuration Manager, the GetVariables method gets the variables for the operating system deployment task sequence environment.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# ITSEnvClass::GetVariables Method
In Configuration Manager, the `GetVariables` method gets the variables for the operating system deployment task sequence environment.

## Syntax

```
[IDL]
HRESULT GetVariables(
     VARIANT* variables
);
```

#### Parameters
 `variables`
 Data type: `VARIANT`

 Qualifiers: [out, retval]

 Pointer to the environment variables.

## Return Values
 An `HRESULT` code. Possible values include, but are not limited to, the following value.

 S_OK
 The method succeeded.

## See Also
 [ITSEnvClass Interface](../../../../../develop/reference/core/clients/client-classes/itsenvclass-interface.md)
