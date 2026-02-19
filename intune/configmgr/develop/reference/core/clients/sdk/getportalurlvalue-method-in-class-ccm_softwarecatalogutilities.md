---
title: GetPortalUrlValue Method
description: Learn how the GetPortalUrlValue Windows Management Instrumentation (WMI) class method in Configuration Manager that returns the portal url for a client.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetPortalUrlValue Method in Class CCM_SoftwareCatalogUtilities
The `GetPortalUrlValue` Windows Management Instrumentation (WMI) class method in Configuration Manager that returns the portal url for a client.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetPortalUrlValue
{
    [OUT]   String PortalUrl
};
```

## Parameters
 `PortalUrl`
 Data type: `String`

 Qualifiers: [id("0"), out]

 Portal url.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
