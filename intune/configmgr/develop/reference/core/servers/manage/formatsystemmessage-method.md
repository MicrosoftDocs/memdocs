---
title: FormatSystemMessage Method
description: Learn how the FormatSystemMessage method, in Configuration Manager, formats a system error message by using the error code and optional insertion strings.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# FormatSystemMessage Method
The `FormatSystemMessage` method, in Configuration Manager, formats a system error message by using the error code and optional insertion strings.

## Syntax

```
[VBScript]
SMSFormatMessageCtl.FormatSystemMessage
```

#### Parameters
 `MessageID`
 Data type: `int`

 Error message ID.

 `InsertionStrings`
 Data type: `object`

 Optional list of insertion strings.

## Return Value
 A string.

## Requirements
 FormatMessageCtl.dll.

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMSFormatMessageCtl Class](../../../../../develop/reference/core/servers/manage/smsformatmessagectl-class.md)
