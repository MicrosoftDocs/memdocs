---
title: AddLicense Method
description: The AddLicense Windows Management Instrumentation (WMI) class method adds license information to an application deployment type.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# AddLicense Method in Class SMS_DeploymentTypeLicenseAssociation
The `AddLicense` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds license information to an application deployment type.

## Syntax

```
sint32 AddLicense (
     [in] string LicenseID,
     [in] string LicenseBlob,
     [in] string ModelName
);

```

#### Parameters
 `LicenseID`
 Data type: `String`

 Qualifiers: [in]

 The ID of the license.

 `LicenseBlob`
 Data type: `String`

 Qualifiers: [in]

 The license blob.

 `ModelName`
 Data type: `String`

 Qualifiers: [in]

 The model name of the deployment type.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_DeploymentTypeLicenseAssociation Server WMI Class](../../../develop/reference/apps/sms_deploymenttypelicenseassociation-server-wmi-class.md)
