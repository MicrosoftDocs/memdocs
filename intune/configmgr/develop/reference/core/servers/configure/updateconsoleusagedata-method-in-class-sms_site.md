---
title: UpdateConsoleUsageData Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the UpdateConsoleUsageData WMI class method updates console usage data received from console connections.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 189235fc-738b-4b3f-b81a-7d53dfb6c220
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# UpdateConsoleUsageData Method in Class SMS_Site
The `UpdateConsoleUsageData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates console usage data received from console connections.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 UpdateConsoleUsageData (
    SMS_ConsoleUsageData ConsoleUsageData
);

```

#### Parameters
 `ConsoleUsageData`
 Data type: `SMS_ConsoleUsageData`

 Qualifiers: [in]

 Console usage data.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
