---
title: "CNG certificates overview"
titleSuffix: "Configuration Manager"
description: "An overview of CNG certificates in Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe

---

# CNG certificates overview
<!-- 1356191 --> 

Confiuration Manager has limited support for Cryptography: Next Generation (CNG) certificates. Configuration Manager clients can use PKI client authentication certificate with private key in CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware based private key, such as TPM KSP for PKI client authentication certificates.

## Supported scenarios
You can use [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) certificate templates for the following scenarios:

- Client registration and communication with an HTTPS management point.   
- Software distribution and application deployment with an HTTPS distribution point.   
- Operating system deployment.  
- Client messaging SDK (with latest update) and ISV Proxy.   
- Cloud Management Gateway configuration.  

> [!NOTE]
> CNG is backward compatible with Crypto API (CAPI). CAPI certificates will continue to be supported even when CNG support is enabled on the client.

## Unsupported scenarios

The following scenarios are not currently supported:

- Application Catalog Web service, Application Catalog website, Enrollment point, and Enrollment proxy point roles will not be operational when installed in HTTPS mode with a CNG certificate bound to the web site in Internet Information Services (IIS). Software Center will not display applications and packages as available that are deployed to user or user group collections.

- State Migration Point will not be operational when installed in HTTPS mode with a CNG certificate bound to the web site in IIS.

- Using CNG certificates to create a Cloud Distribution Point.

- NDES Policy Module to Certificate Registration Point (CRP) communication will fail if the NDES Policy Module is using a CNG certificate for client authentication certificate.

- Task sequence media creation will fail to create bootable media if a CNG certificate is specified.

## To use CNG certificates

To use CNG certificates, your certification authority (CA) needs to provide CNG certificate templates for target machines.  Template details vary according to the scenario; however, the following properties are required:

- **Compatibility** tab

    - **Certificate Authority** must be Windows Server 2008 or later. (Windows Server 2012 is recommended.)

    - **Certificate recipient** must be Windows Vista/Server 2008 or later. (Windows 8/Windows Server 2012 is recommended.)

- **Cryptography** tab

    - **Provider Category** must be **Key Storage Provider**.  (Required)

> [!NOTE]
> The requirements for your environment or organization may be different. Contact your PKI expert. The important point to consider is a certificate template must use a Key Storage Provider to be able to take advantage of CNG.

For best results, we recommend building the Subject Name from Active Directory information.  Use the DNS Name for **Subject name format** and include the DNS name in the alternate subject name.  Otherwise, you must provide this information when the device enrolls into the certificate profile.