---
title:  Tenant attached CMPivot overview 
titleSuffix: Configuration Manager
description: CMPivot overview for Microsoft Endpoint Manager tenant attached devices.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart 
manager: dougeby
---

# Tenant attach: CMPivot overview

*Applies to: Configuration Manager (technical preview branch)*

> [!Important]
> This article applies to the technical preview branch for Configuration Manager. For more information see, [Configuration Manager technical preview version 2005](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot).

CMPivot allows you to quickly assess the state of a device in your environment and take action. When you enter a query, CMPivot will run a query in real time on the currently connected device. The data returned can then be filtered, grouped, and refined to answer business questions, troubleshoot issues in your environment, or respond to security threats. For more information about using CMPivot, see [Use CMPivot](../core/servers/manage/cmpivot.md).

## <a name="bkmk_refine"></a> Refine CMPivot queries

When using CMPivot from the Microsoft Endpoint Manager admin console, ensure your queries are tuned for performance. If you request a query with a data set that is too large, you may receive `Error: The query result is too large, retry with additional filters`. Refine your query to be more specific if you see this error. The following operators are commonly used to refine queries:

- Use `count` if you only need the number of items returned.
- Use `project` if you only need specific columns.
- Use `take` to return up to the specified number of rows.
- Use `top` to return the first N records sorted by specified columns.

> [!Important]
> When using CMPivot to query a device, if there isn't a response within 10 minutes, the query will timeout. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## Next steps

For more sample scripts, see [Microsoft Endpoint Manager tenant attach: CMPivot script samples](cmpivot-samples-attached.md).
