---
title: StoreEvent Method
description: The StoreEvent Windows Management Instrumentation class method generates store events.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# StoreEvent Method in Class CCM_ClientEvents
The `StoreEvent` Windows Management Instrumentation (WMI) class method generates store events.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```

 uint32 StoreEvent
{
     UInt32 DurationMS,
     String ComponentName,
     String EventName,
     String SessionId
 };

```

## Parameters
 `DurationMS`
 Data type: `UInt32`

 Qualifiers: [in]

 The duration of the event in milliseconds.

 `ComponentName`
 Data type: `String`

 Qualifiers: [in]

 The name of the component.

 `EventName`
 Data type: `String`

 Qualifiers: [in]

 The name of the event.

 `SessionId`
 Data type: `String`

 Qualifiers: [in]

 The ID of the session.

## Requirements

### Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See also

[CCM_ClientEvents Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_clientevents-client-wmi-class.md)
