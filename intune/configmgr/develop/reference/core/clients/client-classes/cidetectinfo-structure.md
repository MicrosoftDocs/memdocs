---
title: CIDetectInfo Structure
description: Learn how the CIDetectInfo structure contains identity information for baseline configuration item detection.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# CIDetectInfo Structure
In Configuration Manager, the `CIDetectInfo` structure contains identity information for baseline configuration item detection.

## Syntax

```
struct CIDetectInfo
{
      LPWSTR szCIID;
      LPWSTR szVersion;
};
```

## Members
 szCIID
 ID of the configuration item.

 szVersion
 Version of the configuration item.

## See Also
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)
