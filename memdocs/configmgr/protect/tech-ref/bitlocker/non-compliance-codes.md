---
title: Non-compliance codes
titleSuffix: Configuration Manager
description: A technical reference for the possible codes from a Configuration Manager client that's not compliant with BitLocker policy
ms.date: 11/29/2019
ms.service: configuration-manager
ms.subservice: protect
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Non-compliance codes

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

WMI on the client provides the following non-compliance codes. It also describes the reasons why a particular device reports as non-compliant.

There are various methods to view WMI. For example, use the following PowerShell command:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> If the device is compliant, this command doesn't return anything.
>
> You can also check the `Compliant` attribute of this class, which is `1` if the device is compliant.

|Non-compliance code|Reason for non-compliance|
|--- |--- |
|0|Cipher strength not AES 256.|
|1|BitLocker policy requires this volume to be encrypted, but it isn't.|
|2|BitLocker policy requires this volume to *not* be encrypted, but it is.|
|3|BitLocker policy requires this volume use a TPM protector, but it doesn't.|
|4|BitLocker policy requires this volume use a TPM+PIN protector, but it doesn't.|
|5|BitLocker policy doesn't allow non-TPM machines to report as compliant.|
|6|Volume has a TPM protector, but the TPM isn't visible.|
|7|BitLocker policy requires this volume use a password protector, but it doesn't have one.|
|8|BitLocker policy requires this volume *not* use a password protector, but it has one.|
|9|BitLocker policy requires this volume use an auto-unlock protector, but it doesn't have one.|
|10|BitLocker policy requires this volume *not* use an auto-unlock protector, but it has one.|
|11|BitLocker detects a policy conflict, which prevents it from reporting this volume as compliant.|
|12|A system volume is needed to encrypt the OS volume, but it isn't present.|
|13|Protection is suspended for the volume.|
|14|Auto-unlock protector is unsafe unless the OS volume is encrypted.|
|15|Policy requires minimum cypher strength is XTS-AES-128 bit, actual cypher strength is weaker.|
|16|Policy requires minimum cypher strength is XTS-AES-256 bit, actual cypher strength is weaker.|
