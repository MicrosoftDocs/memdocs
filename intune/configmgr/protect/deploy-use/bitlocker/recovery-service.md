---
title: BitLocker recovery service
titleSuffix: Configuration Manager
description: Learn about the BitLocker recovery service in Configuration Manager.
ms.date: 12/01/2021
ms.service: configuration-manager
ms.subservice: protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# About the BitLocker recovery service

*Applies to: Configuration Manager (current branch)*

[!INCLUDE [11108795 note about recovery service](includes/11108795-bitlocker-recovery-service.md)]

The BitLocker recovery service is a server component that receives BitLocker recovery data from Configuration Manager clients. The site deploys the recovery service when you create a BitLocker management policy. Configuration Manager automatically installs the recovery service on each management point with an HTTPS-enabled website.

Configuration Manager stores the recovery information in the site database. Without a BitLocker management encryption certificate, Configuration Manager stores the key recovery information in plain text. For more information, see [Encrypt recovery data in the database](encrypt-recovery-data.md).

Starting in version 2010, you can manage BitLocker policies and escrow recovery keys over a cloud management gateway (CMG). When domain-joined clients communicate via the CMG, they don't use the legacy recovery service, but the message processing engine component of the management point. Microsoft Entra hybrid joined devices also use the message processing engine.

Starting in version 2103, all supported clients use the message processing engine component of the management point as the recovery service. This change reduces dependencies on legacy MBAM components, and enables support for [enhanced HTTP](../../../core/plan-design/hierarchy/enhanced-http.md).<!-- 9503186 -->

> [!NOTE]
> For version 2010, the message processing engine channel only escrows keys for OS and fixed drive volumes. It doesn't support recovery keys for removable drives or the TPM password hash.
>
> Starting in version 2103, BitLocker management policies over a CMG support the following capabilities:<!--8845996-->
>
> - Recovery keys for removable drives
> - TPM password hash, otherwise known as TPM owner authorization

## Rotate keys

When you recover a key with the self-service or helpdesk portals, since it's disclosed, Configuration Manager requires the client to rotate the key. Rotating the key means that the client generates a new key for BitLocker recovery. It then escrows the new key to the [recovery service](recovery-service.md).<!-- 12571609 -->

> [!NOTE]
> When you migrate from MBAM, when the device receives a BitLocker management policy from Configuration Manager, it first rotates its key. It then sends the new key to the Configuration Manager recovery service.

## Next steps

[Migrate from MBAM](migration-considerations.md)

[Set up BitLocker reports and portals](setup-websites.md)
