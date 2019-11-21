---
title: Client event logs
titleSuffix: Configuration Manager
description: A technical reference for the possible BitLocker (MBAM) client entries in the Windows event log
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Client event logs

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

On a Configuration Manager client to which you deploy a BitLocker management policy, use the Windows Event Viewer to view BitLocker client event logs. Go to **Applications and Services Logs**, **Microsoft**, **Windows**, **MBAM** for both [Admin](#admin) and [Operational](#operational) event logs.

For more information on using these logs, see [BitLocker event logs](/configmgr/protect/tech-ref/bitlocker/about-event-logs).

## Admin

|Event ID|Task category|Message|
|--- |--- |--- |
|2|VolumeEnactmentFailed|An error occurred while applying MBAM policies.|
|4|TransferStatusDataFailed|An error occurred while sending encryption status data.|
|8|SystemVolumeNotFound|The system volume is missing. SystemVolume is needed to encrypt the operating system drive.|
|9|TPMNotFound|The TPM hardware is missing. TPM is needed to encrypt the operating system drive with any TPM protector.|
|10|MachineHWExempted|The computer is exempted from Encryption. Machine's hardware status: Exempted|
|11|MachineHWUnknown|The computer is exempted from encryption. Machine's hardware status: Unknown|
|12|HWCheckFailed|Hardware exemption check failed.|
|13|UserIsExempted|The user is exempt from encryption.|
|14|UserIsWaiting|The user requested an exemption.|
|15|UserExemptionCheckFailed|User exemption check failed.|
|16|UserPostponed|The user postponed the encryption process.|
|17|TPMInitializationFailed|TPM initialization failed. The user rejected the BIOS changes.|
|18|CoreServiceDown|Unable to connect to the MBAM Recovery and Hardware service.|
|20|PolicyMismatch|The MBAM policy is in conflict or corrupt.|
|21|ConflictingOSVolumePolicies|Detected OS volume encryption policies conflict. Check BitLocker and MBAM policies related to OS drive protectors.|
|22|ConflictingFDDVolumePolicies|Detected Fixed Data Drive volume encryption policies conflict. Check BitLocker and MBAM policies related to FDD drive protectors.|
|27|EncryptionFailedNoDra|An error occurred while encrypting. A Data Recovery Agent (DRA) protector is required in FIPS mode for pre-Windows 8.1 machines.|
|34|TpmLockOutResetFailed|Failed to reset TPM lockout.|
|36|TpmOwnerAuthRetrievalFailed|Failed to retrieve TPM OwnerAuth from MBAM services.|
|37|WmiProviderDllSearchPathUpdateFailed|Failed to update the DLL search path for WMI provider.|
|38|TimedOutWaitingForWmiProvider|Agent Stopping - Timed-out waiting for MBAM WMI Provider Instance.|

## Operational

|Event ID|Task category|Message|
|--- |--- |--- |
|1|VolumeEnactmentSuccessful|The MBAM policies were applied successfully.|
|3|TransferStatusDataSuccessful|The encryption status data was sent successfully.|
|19|CoreServiceUp|Successfully connected to the MBAM Recovery and Hardware service.|
|28|TpmOwnerAuthEscrowed|The TPM OwnerAuth has been escrowed.|
|29|RecoveryKeyEscrowed|The BitLocker recovery key for the volume has been escrowed.|
|30|RecoveryKeyReset|The BitLocker recovery key for the volume has been updated.|
|31|EnforcePolicyDateSet|The enforce policy date...has been set for the volume|
|32|EnforcePolicyDateCleared|The enforce policy date...has been cleared for the volume.|
|33|TpmLockOutResetSucceeded|Successfully reset TPM lockout.|
|35|TpmOwnerAuthRetrievalSucceeded|Successfully retrieved TPM OwnerAuth from MBAM services.|
|39|RemovableDriveMounted|Removable drive was mounted.|
|40|RemovableDriveDismounted|Removable drive was unmounted.|
|41|FailedToEnactEndpointUnreachable|Failure to connect to the MBAM Recovery and Hardware service prevented MBAM policies from being applied successfully to the volume.|
|42|FailedToEnactLockedVolume|Locked volume state prevented MBAM policies from being applied successfully to the volume.|
|43|TransferStatusDataFailedEndpointUnreachable|Failure to connect to the MBAM Compliance and Status service prevented the transfer of encryption status data.|
