---
title: Migrate from MBAM
titleSuffix: Configuration Manager
description: Understand the considerations when migrating from Microsoft BitLocker Administration and Monitoring (MBAM) to BitLocker management in Configuration Manager.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Migrate from MBAM

*Applies to: Configuration Manager (current branch)*

If you currently use Microsoft BitLocker Administration and Monitoring (MBAM), you can seamlessly migrate management to Configuration Manager. When you deploy BitLocker management policies in Configuration Manager, clients automatically rotate their keys and upload them to the Configuration Manager recovery service.

> [!IMPORTANT]
> When you migrate from stand-alone MBAM to Configuration Manager BitLocker management, if you require existing functionality of stand-alone MBAM, don't reuse stand-alone MBAM servers or components with Configuration Manager BitLocker management. If you reuse these servers, stand-alone MBAM will stop working when Configuration Manager BitLocker management installs its components on those servers. Don't run the MBAMWebSiteInstaller.ps1 script to set up the BitLocker portals on stand-alone MBAM servers. When you set up Configuration Manager BitLocker management, use separate servers.

## Group policy

If a group policy setting exists for standalone MBAM, it will override the equivalent setting attempted by Configuration Manager. Standalone MBAM uses domain group policy, while Configuration Manager sets local policies for BitLocker management. Domain policies will override the local Configuration Manager BitLocker management policies. If the standalone MBAM domain group policy doesn't match the Configuration Manager policy, Configuration Manager BitLocker management will fail. For example, if a domain group policy sets the standalone MBAM server for key recovery services, Configuration Manager BitLocker management can't set the same setting for its recovery service. This behavior causes clients to not report their recovery keys to the Configuration Manager BitLocker management recovery service.

Don't set a group policy for a setting that Configuration Manager BitLocker management already specifies. Only set group policies for settings that don't currently exist in Configuration Manager BitLocker management. Configuration Manager has feature parity with standalone MBAM. In most instances there should be no reason to set domain group policies to configure BitLocker policies. To prevent conflicts and problems, avoid use of group policies for BitLocker. Configure all settings through Configuration Manager BitLocker management policies.

## TPM password hash

- Previous MBAM clients don't upload the TPM password hash to Configuration Manager. The client only uploads the TPM password hash once.

- If you need to migrate this information to the Configuration Manager recovery service, clear the TPM on the device. After it restarts, it uploads the new TPM password hash to the recovery service.

> [!NOTE]
> Uploading of the TPM password hash mainly pertains to versions of Windows before Windows 10. Windows 10 or later by default doesn't save the TPM password hash, so these devices don't normally upload it. For more information, see [About the TPM owner password](/windows/security/information-protection/tpm/change-the-tpm-owner-password#about-the-tpm-owner-password).

## Re-encryption

Configuration Manager doesn't re-encrypt drives that are already protected with BitLocker Drive Encryption. If you deploy a BitLocker management policy that doesn't match the drive's current protection, it reports as non-compliant. The drive is still protected.

For example, you used MBAM to encrypt the drive with the AES-XTS 128 encryption algorithm, but the Configuration Manager policy requires AES-XTS 256. The drive is non-compliant with the policy, even though the drive is encrypted.

To work around this behavior, first disable BitLocker on the device. Then deploy a new policy with the new settings.

## Next steps

[About the BitLocker recovery service](recovery-service.md)

[Set up BitLocker reports and portals](setup-websites.md)
