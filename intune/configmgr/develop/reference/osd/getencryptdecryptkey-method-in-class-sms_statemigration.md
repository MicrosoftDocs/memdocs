---
title: GetEncryptDecryptKey Method
description: The GetEncryptDecryptKey WMI class method retrieves the symmetric key that is used to encrypt and decrypt the user state during state migration.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetEncryptDecryptKey Method in Class SMS_StateMigration
The `GetEncryptDecryptKey` Windows Management Instrumentation (WMI) class method, in Configuration Manager, retrieves the symmetric key that is used to encrypt and decrypt the user state during state migration.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 GetEncryptDecryptKey(
   String Key
);
```

#### Parameters
 `Key`
 Data type: `String`

 Qualifiers: [out]

 The encryption key required to restore user state.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)
 [AddAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md)
