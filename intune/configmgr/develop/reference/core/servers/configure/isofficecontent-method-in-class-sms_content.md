---
title: IsOfficeContent Method
description: Learn about the IsOfficeContent class method. In Configuration Manager, this method specifies whether content is Microsoft 365 content.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# IsOfficeContent Method in Class SMS_Content
The `IsOfficeContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, specifies whether content is Microsoft 365 content.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
Boolean IsOfficeContent (
    UInt32 ContentId
);

```

#### Parameters
 `ContentId`
 Data type: `UInt32`

 Qualifiers: [in]

 Content ID.

## Return Values
 `True` if content is Microsoft 365 content; otherwise, `False`.

## Requirements

### Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See also

[SMS_Content server WMI class](sms_content-server-wmi-class.md)
