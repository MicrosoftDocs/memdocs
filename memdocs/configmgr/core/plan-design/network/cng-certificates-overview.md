---
title: CNG v3 certificates overview
titleSuffix: Configuration Manager
description: Learn about support for Cryptography Next Generation (CNG) v3 certificates for Configuration Manager clients and servers.
ms.date: 07/19/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CNG v3 certificates overview
<!-- 1356191 -->

Configuration Manager supports Cryptography: Next Generation (CNG) certificates. Configuration Manager clients can use a PKI client authentication certificate with the private key generated and stored in a CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware-based private keys, such as a TPM KSP for PKI client authentication certificates.

> [!NOTE]
> When using CNG certificates, Configuration Manager clients only support certificates that use the **RSA** cryptographic algorithm. <!-- 7836017 -->

## Supported scenarios

You can use [Cryptography API: Next Generation (CNG)](/windows/win32/seccng/cng-features) v3 certificate templates for the following scenarios:

- Client registration and communication with an HTTPS management point
- Software distribution and application deployment with an HTTPS distribution point
- OS deployment
- Client messaging SDK (with latest update) and ISV Proxy
- Cloud management gateway (CMG) configuration
- User-targeted available applications in Software Center<!-- MEMDocs#1576 -->

Also use CNG v3 certificates for the following HTTPS-enabled server roles: <!-- 1357314 -->

- Management point
- Distribution point
- Software update point
- State migration point
- Certificate registration point, including the NDES server with the Configuration Manager policy module <!--1357314-->

> [!NOTE]
> CNG is backward compatible with Crypto API (CAPI). CAPI certificates continue to be supported even when CNG support is enabled on the client.

## Unsupported scenarios

The following scenarios currently aren't supported:

- The following server roles aren't operational when installed in HTTPS mode with a CNG v3 certificate bound to the web site in Internet Information Services (IIS):

  - Enrollment point  
  - Enrollment proxy point  

## To use CNG certificates

To use CNG v3 certificates, your certification authority (CA) needs to provide CNG certificate templates for target machines. Template details vary according to the scenario; however, the following properties are required:

- **Compatibility** tab

  - **Certificate Authority** must be Windows Server 2008 or later. (Windows Server 2012 is recommended.)

  - **Certificate recipient** must be Windows Vista/Server 2008 or later. (Windows 8/Windows Server 2012 is recommended.)

- **Cryptography** tab

  - **Provider Category** must be **Key Storage Provider**. (required)

  - **Algorithm name** must be **RSA**. (required) <!-- 7836017 -->

  - **Request must use one of the following providers:** must be **Microsoft Software Key Storage Provider**.

> [!NOTE]
> The requirements for your environment or organization may be different. Contact your PKI expert. The important point to consider is a certificate template must use a Key Storage Provider to take advantage of CNG.

For best results, we recommend building the Subject Name from Active Directory information. Use the DNS Name for **Subject name format** and include the DNS name in the alternate subject name. Otherwise, you must provide this information when the device enrolls into the certificate profile.
