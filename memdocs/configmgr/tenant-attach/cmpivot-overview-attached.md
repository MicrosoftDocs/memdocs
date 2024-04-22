---
title: Tenant attached CMPivot usage overview
titleSuffix: Configuration Manager
description: CMPivot usage overview for Microsoft Intune tenant attached devices.
ms.date: 01/25/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Tenant attach: CMPivot usage overview

*Applies to: Configuration Manager (current branch)*

CMPivot allows you to quickly assess the state of a device in your environment and take action. When you enter a query, CMPivot will run a query in real time on the currently connected device. The data returned can then be filtered, grouped, and refined to answer business questions, troubleshoot issues in your environment, or respond to security threats. For more information about using CMPivot, see [Use CMPivot](../core/servers/manage/cmpivot.md).

## <a name="bkmk_refine"></a> Refine CMPivot queries

When using CMPivot from the Microsoft Intune admin center, ensure your queries are tuned for performance. If you request a query with a data set that is too large, you may receive `Error: The query result is too large, retry with additional filters`. Refine your query to be more specific if you see this error. The following operators are commonly used to refine queries:

- Use `count` if you only need the number of items returned.
- Use `project` if you only need specific columns.
- Use `take` to return up to the specified number of rows.
- Use `top` to return the first N records sorted by specified columns.

> [!Important]
> When using CMPivot to query a device, if there isn't a response within 10 minutes, the query will timeout. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Intune and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## Next steps

For more information, see [Launch CMPivot from the admin center](cmpivot-start.md)
For more sample scripts, see [Microsoft Intune tenant attach: CMPivot script samples](cmpivot-samples-attached.md).
