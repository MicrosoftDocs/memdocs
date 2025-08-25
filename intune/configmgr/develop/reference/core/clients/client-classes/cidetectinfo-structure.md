---
title: CIDetectInfo Structure
description: Learn how the CIDetectInfo structure contains identity information for baseline configuration item detection.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c719e7cf-481b-44ee-92db-60de1b4e5581
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
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
