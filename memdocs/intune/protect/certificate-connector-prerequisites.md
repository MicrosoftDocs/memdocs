---
# required metadata

title: Prerequisites for use of the Certificate Connector for Microsoft Intune - Azure | Microsoft Docs
description: Review the software and network prerequisites for use of the Certificate Connector for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/21/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Prerequisites for the Certificate Connector for Microsoft Intune

Before you install and configure the Certificate Connector for Microsoft Intune, review the prerequisites and infrastructure requirements, which can vary depending on the features you’ll configure a connector instance to support.

## General prerequisites

Requirements for the computer where you install the connector software:

- Windows Server 2012 R2 or later
- .NET 4.7.2
- The server must meet the same network requirements as managed devices.
- To support automatic updates of the connector software, the server must have access to the **Azure update service**:
  - Port: **443**
  - Endpoint: **autoupdate.msappproxy.net**

## PKCS

Requirements for PKCS certificate templates:

- Certificate templates you’ll use for PKCS requests must be configured with permissions that allow the certificate connector service account to auto enroll the certificate.
- The certificate templates must be added to the Certification Authroity (CA).

> [!NOTE]
> Any instance of the connector that supports PKCS can be used to retrieve pending PKCS requests from the Intune Service queue. It's not possible to define which connector handles each request. </br></br>
> Therefore, each connector that supports PKCS must have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.

## Revocation Prerequisites

- The Certification Authority must be configured to allow the [connector service account](#certificate-connector-service-account) to revoke certificates.

## SCEP

The connector requires the following:

- IIS 7 or higher
- .NET Framework 4.7

On the Windows Server, configure the following Server Roles and Features:

- **Server Roles**:
  - Active Directory Certificate Services
    - Network Device Enrollment Service - For the connector SCEP when you use a Microsoft CA, [install and configure](../protect/certificates-scep-configure.md#set-up-ndes) the **Network Device Enrollment Service** (NDES) server role. When you configure NDES, you’ll need to assign a user account for use by the [NDES application pool](#ndes-application-pool-user). NDES also has it's own requirements.
  - Web Server (IIS)
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

- **Features**:
  - .NET Framework 4.7 Features
    - .NET Framework 4.7
    - ASP.NET 4.7
    - WCF Services
      - HTTP Activation

Requirements for SCEP certificate templates:

- Certificate templates you’ll use for SCEP requests must be configured with permissions that allow the Certificate Connector service account to auto enroll the certificate.
- The certificate templates must be added to the CA.

## Accounts

Prepare the following accounts before you install the certificate connector software.

### Installation account

You can use any user account that has local administrative permissions on the Windows Server to install the connector software. You can use this same account to configure the Windows Server with the NDES Windows server role should your use of the connector require it.

### Certificate connector service account

The Certificate Connector requires an account to use as a service account. This account is used by the connector to access the Windows Server, communicate with Intune, and access the Certification Authority to service PKI requests.

The connector service account must have the following permissions:

- [**Logon as Service**](/system-center/scsm/enable-service-log-on-sm?view=sc-sm-2019&preserve-view=true)
- **Issue and Manage Certificates** permissions on the Certification Authority (required only for revocation scenarios).
- **Read** and **Enroll** permissions on any certificate template that you’ll use to issue certificates.
- Permissions to the **Key Storage Provider** (KSP) that’s used by PFX Import. See [Import PFX Certificates to Intune](../protect/certificates-imported-pfx-configure.md#import-pfx-certificates).

The following options are supported for use as the certificate connector service account:

- **SYSTEM**
- **Managed Service Account** – See [Create a group managed service account (gMSA)](/azure/active-directory-domain-services/create-gmsa) in the Azure Active Directory documentation.
- **Domain user**

For more information, see [Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md).

### NDES application pool user

To use SCEP with a Microsoft CA, you’ll need to add NDES to the server that hosts the connector before installing the connector. When you configure NDES, you’ll need to specify an account for use as the application pool user. This account can be a local or domain user account and must have the following permissions:

- **Read** and **Enroll** permissions on each SCEP certificate template you’ll use to issue certificates.
- Member of the **IIS_IUSRS** group.

For guidance on configuring the NDES server role for the Certificate Connector for Microsoft Intune, see [Set up NDES](../protect/certificates-scep-configure#set-up-ndes) in **Configure infrastructure to support SCEP with Intune**.

## Next steps

[Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md)
