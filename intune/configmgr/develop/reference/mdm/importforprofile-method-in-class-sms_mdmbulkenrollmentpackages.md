---
title: ImportForProfile Method
description: The ImportForProfile Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports an On-Premises Mobile Device Management (MDM) bulk enrollment package for a profile.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: fdbb743a-c476-474e-a129-e789180c1bf5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# ImportForProfile Method in Class SMS_MDMBulkEnrollmentPackages
The `ImportForProfile` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports an On-Premises Mobile Device Management (MDM)  bulk enrollment package for a profile.

## Syntax

```
sint32 ImportForProfile(
     String ProfileGUID,
     String CertificateGUID,
     String PackageName,
     String Certificate
);

```

#### Parameters
 `ProfileGUID`
 Data type: `String`

 Qualifiers: [in]

 The GUID of the profile.

 `CertificateGUID`
 Data type: `String`

 Qualifiers: [in]

 The GUID of the certificate.

 `PackageName`
 Data type: `String`

 Qualifiers: [in]

 Package name.

 `Certificate`
 Data type: `String`

 Qualifiers: [in]

 The root certificate.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_MDMBulkEnrollmentPackages Server WMI Class](../../../develop/reference/mdm/sms_mdmbulkenrollmentpackages-server-wmi-class.md)
