---
description: Learn how to generate client configuration requests (CCRs) for the query in Configuration Manager using CreateCCRs.
title: CreateCCRs method in class SMS_Query
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7ad37be0-497c-4647-9c22-9097ea13bfc4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# CreateCCRs Method in Class SMS_Query
The `CreateCCRs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, generates client configuration requests (CCRs) for the query.

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.

## Syntax

```
SInt32 CreateCCRs(
   Boolean PushOnlyAssignedClients,
   SInt32 ClientType,
   Boolean Forced,
   Boolean ForceReinstall,
   Boolean PushEvenIfDC,
   Boolean InformationOnly,
   Boolean SpecifySiteCode,
   String PushSiteCode
);
```

#### Parameters
 `PushOnlyAssignedClients`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `true` to push installation only to assigned clients.

 `ClientType`
 Data type: `SInt32`

 Qualifiers: [in, optional]

 Type of client.

 `Forced`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `true` to force installation. The value defaults to `false`, if not specified. This is used to force reinstallation, even if the client is already installed. If `Forced` is set to `true`, the operating system value will be ignored.

 `ForceReinstall`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `true` to force reinstallation. The value defaults to `false`, if not specified.

 `PushEvenIfDC`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `true` to push installation on a domain component.

 `InformationOnly`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `true` if the CCRs are for information only. This parameter is only used to gather information from the client.

 `SpecifySiteCode`
 Data type: `Boolean`

 Qualifiers: [in, optional]

 `SpecifySiteCode` is used to control whether the `PushSiteCode` parameter is used. The `PushSiteCode` value will not be used unless `SpecificySiteCode` is set to `true`.

 `PushSiteCode`
 Data type: `String`

 Qualifiers: [in, optional]

 `PushSiteCode` defines which site will initiate the actual push. The specified site will push its client files to the client and do the actual installation.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Query Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_query-server-wmi-class.md)
