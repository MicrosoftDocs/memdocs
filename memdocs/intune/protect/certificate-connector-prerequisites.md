---
# required metadata

title: Prerequisites for the Certificate Connector for Microsoft Intune
description: Review the software and network prerequisites for use of the Certificate Connector for Microsoft Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/09/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- certificates
- sub-certificates
---

# Prerequisites for the Certificate Connector for Microsoft Intune

Review the prerequisites and infrastructure requirements for the Certificate Connector for Microsoft Intune. Some prerequisites and infrastructure requirements can vary depending on the features you configure a connector instance to support.

## General prerequisites

Requirements for the computer where you install the connector software:

- Windows Server 2012 R2 or later.

  > [!NOTE]
  > The Server installation must include the Desktop Experience and support use of a browser. For more information, see [Install Server with Desktop Experience](/windows-server/get-started/getting-started-with-server-with-desktop-experience) in the Windows Server 2016 documentation.

- .NET 4.7.2

- Transport Layer Security (TLS) 1.2. For more information, see [Enable support for TLS 1.2 in your environment](/troubleshoot/azure/active-directory/enable-support-tls-environment) in the Microsoft Entra documentation.

- The server must meet the same network requirements as managed devices. See [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/intune-endpoints.md).

- To support automatic updates of the connector software, the server must have access to the **Azure update service**:
  - Port: **443**
  - Endpoint: **autoupdate.msappproxy.net**

- The **Enhanced Security Configuration** must be deactivated.

## PKCS

Requirements for private and public key pair (PKCS) certificate templates:

- Certificate templates that you use for PKCS requests must be configured with permissions that allow the certificate connector service account to enroll the certificate.
- The certificate templates must be added to the Certification Authority (CA).

> [!NOTE]
> Any instance of the connector that supports PKCS can be used to retrieve pending PKCS requests from the Intune Service queue, process Imported certificates, and handle revocation requests. It's not possible to define which connector handles each request. </br></br>
> Therefore, each connector that supports PKCS must have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.

## PKCS imported certificates

To support PKCS imported certificates, the server that hosts the connector requires additional configurations, such as configuring a Key storage provider access to allow the Connector Service User to retrieve keys.

For information about support for PKCS imported certificates, see [Configure and use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md).

## Revocation Prerequisites

- The Certification Authority must be configured to allow the [connector service account](#certificate-connector-service-account) to revoke certificates.

## SCEP

To support Simple Certificate Enrollment Protocol (SCEP) certificates, the Windows Server that hosts the connector must meet the following prerequisites in addition to the [general prerequisites](#general-prerequisites):

- IIS 7 or higher
- Network Device Enrollment Service (NDES) service, which is part of the Active Directory Certification Services role. The connector isn't supported on the same server as your issuing Certification Authority (CA). For more information, see [Configure infrastructure to support SCEP with Intune](../protect/certificates-scep-configure.md).

On the Windows Server, select to add the following Server Roles and Features:

- **Server Roles**:
  - Active Directory Certificate Services
  - Web Server (IIS)

- **Features**:
  - .NET Framework 4.7 Features
    - .NET Framework 4.7
    - ASP.NET 4.7
    - WCF Services
      - HTTP Activation

- **AD CS > Role Services**:
  - Network Device Enrollment Service - For the connector SCEP when you use a Microsoft CA, [install, and configure](../protect/certificates-scep-configure.md#set-up-ndes) the **Network Device Enrollment Service** (NDES) server role. When you configure NDES, you need to assign a user account for use by the [NDES application pool](#ndes-application-pool-user). NDES also has its own requirements.

- **Web Server Role (IIS) > Role Services**:
  - Security
    - Request Filtering
  - Application Development
    - .NET Extensibility 4.7
    - ASP.NET 4.7
  - Management Tools
    - IIS Management Console
    - IIS 6 Management Compatibility
      - IIS 6 Metabase Compatibility
      - IIS 6 WMI Compatibility

  In addition, NDES requires the following.NET Framework 3.5 Features:
  - .NET Framework 3.5
  - HTTP Activation

Requirements for SCEP certificate templates:

- Certificate templates you use for SCEP requests must be configured with permissions that allow the Certificate Connector service account to auto enroll the certificate.
- The certificate templates must be added to the CA.

## Accounts

Prepare the following accounts before you install the certificate connector software.

### Installation account

You can use any user account that has local administrative permissions on the Windows Server to install the connector software. You can use this same account to configure the Windows Server with the NDES Windows server role should you use SCEP and a Microsoft CA.

### Certificate connector service account

The certificate connector requires an account to use as a service account. This account is used by the connector to access the Windows Server, communicate with Intune, and access the Certification Authority to service PKI requests.

The connector service account must have the following permissions:

- [**Logon as Service**](/system-center/scsm/enable-service-log-on-sm?view=sc-sm-2019&preserve-view=true)
- **Issue and Manage Certificates** permissions on the Certification Authority (required only for revocation scenarios).
- **Read** and **Enroll** permissions on any certificate template that you use to issue certificates.
- Permissions to the **Key Storage Provider** (KSP) that’s used by PFX Import. See [Import PFX Certificates to Intune](../protect/certificates-imported-pfx-configure.md#import-pfx-certificates).

The following options are supported for use as the certificate connector service account:

- **SYSTEM**
- **Domain user** - Use any domain user account that is an administrator on the Windows Server.

For more information, see [Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md).

### NDES application pool user

To use SCEP with a Microsoft CA, you need to add NDES to the server that hosts the connector before installing the connector. When you configure NDES, you need to specify an account for use as the application pool user, which can also be referred to as the NDES service account. This account can be a local or domain user account and must have the following permissions:

- **Read** and **Enroll** permissions on each SCEP certificate template you use to issue certificates.
- Member of the **IIS_IUSRS** group.

For guidance on configuring the NDES server role for the Certificate Connector for Microsoft Intune, see [Set up NDES](../protect/certificates-scep-configure.md#set-up-ndes) in **Configure infrastructure to support SCEP with Intune**.

### Microsoft Entra user

When configuring the connector, you need to use a user account that: is either a Global Admin or Intune Admin and has an Intune license assigned.

## Next steps

[Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md)
