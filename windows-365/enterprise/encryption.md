---
# required metadata
title: Data encryption in Windows 365
titleSuffix:
description: Learn about data encryption in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 01/05/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: anbiswas
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Data encryption in Windows 365

Windows 365 encrypts data at rest and in transit as explained below.

## Encryption of data at rest

To protect data and help you meet your organizational security and compliance goals, Windows 365 Enterprise and Business disks are encrypted with [Azure Storage server-side encryption (SSE)](/azure/storage/common/storage-service-encryption).

This storage layer encryption provides the following benefits:

- When persisting data to the cloud, data at rest on your Microsoft-hosted Cloud PC disks (OS and data) is automatically encrypted.
- Windows 365 disk data is encrypted transparently using 256-bit Advanced Encryption Standard (AES) encryption, a modern block cipher, and is FIPS 140-2 compliant.
- The encryption doesn't impact Cloud PC performance.
- By default, the encryption is applied to every Cloud PC in every region at no extra cost.
- All Windows 365 Enterprise and Business managed disks, snapshots, images, and data written to existing managed disks are automatically encrypted-at-rest with platform-managed keys. Customer-managed Keys aren't currently supported.

Windows 365 as a service treats all data stored on Windows 365 disks as customer content. For more information on how Windows 365 treats privacy and personal data, see [Privacy and personal data in Windows 365](/windows-365/enterprise/privacy-personal-data).

## Encryption of data in transit

Windows 365 uses the Transport Layer Security (TLS) protocol to protect data in transit. TLS provides:

- Strong authentication
- Message privacy and integrity (enabling detection of message tampering, interception, and forgery)
- Interoperability
- Algorithm flexibility
- Ease of deployment and use

TLS 1.2 is used for all connections initiated from Windows 365 to the Azure Virtual Desktop infrastructure components. These components use the same TLS 1.2 ciphers as [Azure Front Door](/azure/frontdoor/concept-end-to-end-tls#supported-cipher-suites).

<!-- ########################## -->
## Next steps

For more information about the cryptographic modules underlying Azure managed disks, see [Cryptography API: Next Generation](/windows/desktop/seccng/cng-portal).

For more information on network connectivity and encryption in transit, see [Understanding Azure Virtual Desktop network connectivity](/azure/virtual-desktop/network-connectivity).
