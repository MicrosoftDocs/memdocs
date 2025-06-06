---
title: GetCIDocumentBody Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the GetCIDocumentBody WMI class method gets the configuration item document body.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cd77676f-e824-47fe-bf6a-a78bc37a8d72
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# GetCIDocumentBody Method in Class SMS_Application
The `GetCIDocumentBody` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the configuration item document body.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 GetCIDocumentBody (
     string DocumentID,
     string Document
);
```

#### Parameters
 `DocumentID`
 Data type: `String`

 Qualifiers: [in]

 ID of the document.

 `Document`
 Data type: `String`

 Qualifiers: [out]

 Body of the document.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)
