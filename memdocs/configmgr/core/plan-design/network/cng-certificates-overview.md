---
title: CNG certificates overview
titleSuffix: Configuration Manager
description: Learn about support for Cryptography Next Generation (CNG) certificates for Configuration Manager clients and servers.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby


---

# CNG certificates overview
<!-- 1356191 --> 

Configuration Manager has limited support for Cryptography: Next Generation (CNG) certificates. Configuration Manager clients can use PKI client authentication certificate with private key in CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware-based private key, such as TPM KSP for PKI client authentication certificates.

## Supported scenarios
You can use [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) certificate templates for the following scenarios:

- Client registration and communication with an HTTPS management point   
- Software distribution and application deployment with an HTTPS distribution point   
- Operating system deployment  
- Client messaging SDK (with latest update) and ISV Proxy   
- Cloud Management Gateway configuration  

Starting with version 1802, use CNG certificates for the following HTTPS-enabled server roles: <!-- 1357314 -->   
- Management point
- Distribution point
- Software update point
- State migration point     

Starting with version 1806, use CNG certificates for the following HTTPS-enabled server roles:

- Certificate registration point, including the NDES server with the Configuration Manager policy module <!--1357314-->

> [!NOTE]
> CNG is backward compatible with Crypto API (CAPI). CAPI certificates continue to be supported even when CNG support is enabled on the client.

## Unsupported scenarios

The following scenarios are currently not supported:

- The following server roles are not operational when installed in HTTPS mode with a CNG certificate bound to the web site in Internet Information Services (IIS): 
    - Application catalog web service
    - Application catalog website
    - Enrollment point  
    - Enrollment proxy point  

- Software Center does not display applications and packages as available that are deployed to user or user group collections.

- Using CNG certificates to create a Cloud Distribution Point.

- If the NDES policy module is using a CNG certificate for client authentication, communication to the certificate registration point fails. 
    - This is supported starting in Configuration Manager version 1806.

- If you specify a CNG certificate when creating task sequence media, the wizard fails to create bootable media.
    - This is supported starting in Configuration Manager version 1806.

## To use CNG certificates

To use CNG certificates, your certification authority (CA) needs to provide CNG certificate templates for target machines. Template details vary according to the scenario; however, the following properties are required:

- **Compatibility** tab

    - **Certificate Authority** must be Windows Server 2008 or later. (Windows Server 2012 is recommended.)

    - **Certificate recipient** must be Windows Vista/Server 2008 or later. (Windows 8/Windows Server 2012 is recommended.)

- **Cryptography** tab

    - **Provider Category** must be **Key Storage Provider**. (required)
    - **Request must use one of the following providers:** must be **Microsoft Software Key Storage Provider**. 

> [!NOTE]
> The requirements for your environment or organization may be different. Contact your PKI expert. The important point to consider is a certificate template must use a Key Storage Provider to take advantage of CNG.

For best results, we recommend building the Subject Name from Active Directory information. Use the DNS Name for **Subject name format** and include the DNS name in the alternate subject name. Otherwise, you must provide this information when the device enrolls into the certificate profile.
