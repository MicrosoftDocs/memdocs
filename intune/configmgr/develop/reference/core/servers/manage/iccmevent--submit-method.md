---
title: "ICCMEvent::Submit Method"
description: In Configuration Manager, the ICCMEvent::Submit method submits an event to Windows Management Instrumentation.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# ICCMEvent::Submit Method
In Configuration Manager, the `ICcmEvent::Submit` method submits an event to Windows Management Instrumentation (WMI).

## Syntax

```
[C++]
HRESULT ICcmEvent::Submit();
```

#### Parameters
 None.

## Return Values
 An `HRESULT` code. Possible values include, but are not limited to, the following:

 S_OK
 The method succeeded.

## Requirements
 Smscore.dll.

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
