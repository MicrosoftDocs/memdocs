---
title: Certificate profile security and privacy
titleSuffix: Configuration Manager
description: Learn about the security guidance for managing certificate profiles for users and devices in Configuration Manager.
ms.date: 03/29/2022
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

# Security and privacy for certificate profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in version 2203, this company resource access feature is no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](resource-access-deprecation-faq.yml).

## Security guidance

Use the following guidance when you manage certificate profiles for users and devices.

### Follow security guidance for the Network Device Enrollment Service (NDES)

Identify and follow any security guidance for NDES. For example, configure the NDES website in Internet Information Services (IIS) to require HTTPS and ignore client certificates.

For more information, see [Network Device Enrollment Service Guidance](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

### Choose the most secure options for certificate profiles

When you configure SCEP certificate profiles, choose the most secure options that devices and your infrastructure can support. Identify, implement, and follow any security guidance that's recommended for your devices and infrastructure.

### Centrally specify user device affinity

Manually specify user device affinity instead of allowing users to identify their primary device. Don't enable usage-based configuration.

If you use the option in a SCEP certificate profile to **Allow certificate enrollment only on the users primary device**, don't consider the information that's collected from users or from the device to be authoritative. If you deploy SCEP certificate profiles with this configuration, and a trusted administrative user doesn't specify user device affinity, unauthorized users might receive elevated privileges and be granted certificates for authentication.

> [!NOTE]
> If you do enable usage-based configuration, this information is collected by using state messages. Configuration Manager doesn't secure state messages. To help mitigate this threat, use SMB signing or IPsec between client computers and the management point.

### Manage certificate template permissions

Don't add **Read** and **Enroll** permissions for users to the certificate templates. Don't configure the certificate registration point to skip the certificate template check.

Configuration Manager supports the extra check if you add the security permissions of **Read** and **Enroll** for users. If authentication isn't possible, you can configure the certificate registration point to skip this check. But neither configuration is recommended.

For more information, see [Planning for certificate template permissions for certificate profiles](../../protect/plan-design/planning-for-certificate-template-permissions.md).

## Privacy information

You can use certificate profiles to deploy root certification authority (CA) and client certificates, and then evaluate whether those devices become compliant after the client applies the profiles. The management point sends compliance information to the site server, and Configuration Manager stores that information in the site database. Compliance information includes certificate properties such as subject name and thumbprint. The client encrypts this information when sent to the management point, but the site database doesn't store it in an encrypted format. Compliance information isn't sent to Microsoft.

Certificate profiles use information that Configuration Manager collects using discovery. For more information, see [Privacy information for discovery](../../core/plan-design/hierarchy/security-and-privacy-for-site-administration.md#BKMK_Privacy_Cliients).

By default, devices don't evaluate certificate profiles. You need to configure the certificate profiles, and then deploy them to users or devices.

> [!NOTE]
> Certificates that are issued to users or devices might allow access to confidential information.
