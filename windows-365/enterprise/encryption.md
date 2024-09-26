---
# required metadata
title: Data encryption in Windows 365
titleSuffix:
description: Learn about data encryption in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/26/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: anbiswas
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Data encryption in Windows 365

Windows 365 encrypts data at rest and in transit as explained in this article.

## Encryption of data at rest

To help you protect your organization's data, Windows 365 Enterprise and Business Cloud PC disks are encrypted with [Azure Storage server-side encryption (SSE)](/azure/storage/common/storage-service-encryption).

This storage layer encryption provides the following benefits:

- When data is persisted to the cloud, data at rest on your Microsoft-hosted Cloud PC's disk is automatically encrypted.
- Windows 365 Cloud PC disks are encrypted transparently using 256-bit Advanced Encryption Standard (AES) encryption, a modern block cipher, and is FIPS 140-2 compliant. The encryption at this layer doesn't affect Cloud PC performance.
- The encryption is applied to every Cloud PC in every region at no extra cost.

The following Windows 365 Enterprise and Business objects are automatically encrypted-at-rest with platform-managed keys:

- Disks
- Snapshots
- Images

Windows 365 as a service treats all data stored on Windows 365 disks as customer content. For more information, see [Privacy and personal data in Windows 365](./privacy-personal-data.md).

>[!NOTE]
>BitLocker is not supported as an encryption option for Windows 365 Cloud PCs. For more information, see [using Windows 10 virtual machines in Intune](https://go.microsoft.com/fwlink/?linkid=2188944).

## Encryption of data in transit

Windows 365 uses the Transport Layer Security (TLS) protocol to protect data in transit. TLS provides:

- Strong authentication
- Message privacy and integrity (enabling detection of message tampering, interception, and forgery)
- Interoperability
- Algorithm flexibility
- Ease of deployment and use

TLS 1.2 is used for all connections started from Windows 365 to the Azure Virtual Desktop infrastructure components. These components use the same TLS 1.2 ciphers as [Azure Front Door](/azure/frontdoor/concept-end-to-end-tls#supported-cipher-suites). Additional technical details on the cipher suites are available at [Microsoft 365 technical reference details about encryption](/purview/technical-reference-details-about-encryption#tls-cipher-suites-supported-by-microsoft-365).

<!-- ########################## -->
## Next steps

For more information about the cryptographic modules underlying Azure managed disks, see [Cryptography API: Next Generation](/windows/desktop/seccng/cng-portal).

For more information on network connectivity and encryption of the RDP remoting connection, see [Understanding Azure Virtual Desktop network connectivity](/azure/virtual-desktop/network-connectivity).
