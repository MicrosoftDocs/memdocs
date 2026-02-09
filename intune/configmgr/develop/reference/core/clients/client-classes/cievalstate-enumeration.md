---
title: CIEvalState Enumeration
description: In Configuration Manager, the CIEvalState enumeration is used by the ICIINFO Interface.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# CIEvalState Enumeration
In Configuration Manager, the `CIEvalState` enumeration defines configuration item evaluation states. This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).

## Syntax

```
typedef enum tagCIEvalState
{
  ciIdle = 0,
  ciEvaluating
} CIEvalState;
```

## Elements
 ciIdle
 Configuration item is idle.

 ciEvaluating
 Configuration item is being evaluated.

## See Also
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
