---
# required metadata

title: C certificate connectors for Microsoft Intune - Azure | Microsoft Docs
description: Learn about certificate connectors for Simple Certificate Enrollment Protocol (SCEP) or Public Key Cryptography Standards (PKCS) certificates and certificate profiles with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/28/2020
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

# Certificate connectors for Microsoft Intune

To support the use of certificates for authentication and the signing and encryption of email using S/MIME, Intune requires the use of a certificate connector. A certificate connector is software you install on an on-premises server. The connector enables cloud-managed devices to provision certificates from on-premises infrastructure, like an issuing Certificate Authority.

This article describes the available connectors, their lifecycle, prerequisites for use, and how to keep them up to date.  

## Available connectors

There are two certificate connectors for Intune. Each has its own uses and requirements.

### PFX Certificate Connector for Microsoft Intune

The **PFX Certificate Connector** supports certificate deployment for PCKS #12 certificate requests and handles requests for PFX files imported to Intune for S/MIME email encryption for a specific user.

> [!TIP]
> Prior to the August update for this connector, PKCS #12 certificate requests were handled by the *Intune Certificate Connector*. With the August update, the functionality for all PKCS certificate requests was consolidated in the *PFX Certificate Connector*, which supports auto-update of the connector to new versions, and requires use of .NET Framework version 4.7.2.

**The PFX Certificate Connector**:

- Supports multiple instances of this connector for each Intune tenant. Each instance of the connector must install on a Windows Server and have access to the private key used to encrypt the passwords of the uploaded PFX files.
- Can install on the same server that hosts an instance of the *Microsoft Intune Connector*.
- Supports [automatic updates](#automatic-updates) to new versions. To automatically install new versions, the computer that hosts the connector must contact **autoupdate.msappproxy.net** on port **443**. If the connector fails to automatically update, you can manually update the connector.
- Supports certificate revocation (requires the connector run version **6.2008.60.607** or later)
- Has the same network requirements as [managed devices](../fundamentals/intune-endpoints.md#access-for-managed-devices)

  For more information, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).

**The Windows server where the connector installs**:

- Must run Windows Server 2012 R2 or later.
- Run the .NET 4.7.2 Framework.  

**To install the PFX Certificate connector**:

For guidance installation of this connector, see [Download, install, and configure the PFX Certificate Connector for Microsoft Intune](certificates-imported-pfx-configure.md).

### Microsoft Intune Connector

The **Microsoft Intune Connector** is sometimes referred to as the *Microsoft Intune Certificate Connector*. This connector supports certificate deployment when you use *Simple Certificate Enrollment Protocol* (SCEP) and have an Active Directory Certificate Services Certification Authority (CA). This type of CA is also referred to as a *Microsoft CA*.

When you use SCEP with a Microsoft CA, you must also configure the **Network Device Enrollment Service** (NDES). For that reason, this connector is often referred to as the *NDES Certificate Connector*.

If  you use a [third-party Certification Authority](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), you don’t need to use this connector and NDES isn’t required.

**The Microsoft Intune Connector**:

- Installs on a Windows server, which can also host an instance of the *PFX Certificate Connector*.
- Supports up to 100 instances of this connector per tenant, with each instance on a separate Windows server. When you use multiple connectors:
  - All instances of the *Microsoft Intune Connector* in your environment should be at the same version.
  - Your infrastructure supports redundancy and load balancing, as any available connector instance can process your certificate requests.
- Requires a [manual update](#manual-update) to install the new version of the connector. Manual update requires you to uninstall the current connector, and then install the new version of the connector. Additional actions shouldn't be required.
- Supports *Federal Information Processing Standard* (FIPS) mode. FIPS isn't required. When FIPS is enabled, you can issue and revoke certificates.
- Has the same network requirements as [managed devices](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  For more information, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).

**The Windows server where the connector installs**:

- Must run Windows Server 2012 R2 or later.
- Run the .NET 4.5 Framework. When this connector installs on the same server as the *PFX Certificate Connector*, you must use .NET 4.7.2 Framework, which is required by the PFX connector.
- Can't be the same server that hosts your issuing Certificate Authority (CA).
- When used for SCEP with a Microsoft CA, requires access to a server that runs NDES. NDES runs on a Windows server, and can run on the same server as this connector.

**When NDES is required**:

- Internet Explorer Enhanced Security Configuration [must be disabled on the server that hosts NDES](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) and the server that hosts the *Microsoft Intune Connector*.
- The connector requires additional configurations to communicate with NDES. You'll find procedures for installing and configuring NDES with the procedures for installing the *Microsoft Intune Connector*.

  For more information about NDES, see [Network Device Enrollment Service Guidance](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**To install the Microsoft Intune Connector**:

For guidance on installation of this connector, see [Configure infrastructure to support SCEP with Intune](certificates-scep-configure.md).

## Connector Lifecycle

Periodically, updated versions of certificate connectors are released. Announcements for new connector releases appear in the (What’s New](../fundamentals/whats-new.md) article for Intune and in the [What's new for Connectors](#whats-new-for-connectors) section near the end of this article.

When a new version releases, support for the previous version is deprecated with a limited grace period for its continued use. After the grace period expires, support for that deprecated version ends, and it can stop functioning at any time. The grace period is six months.

Plan to update a connector to the latest version at the first opportunity. Each connector has a different update path:

- **PFX Certificate Connector for Microsoft Intune** - Supports automatic updates.
- **Microsoft Intune Connector** - Requires manual update.

### Automatic update

When supported by the connector type and your environment, Intune can automatically update the connector to the latest version shortly after that connector version is released.  

To update automatically, the server that hosts the connector must access the **Azure update service**:

- Port: **443**
- Endpoint: **autoupdate.msappproxy.net**

When firewalls, infrastructure, or network configurations limit access for automatic update, resolve the blocking issues or manually update the connector to the new version.

### Manual update

The process to manually update a certificate connector is the same for reinstalling a connector.

You can manually update a certificate connector even when it supports automatic updates. For example, you can manually update the connector when your network configuration blocks an automatic update.  

### To reinstall a certificate connector

1. On the Windows server that hosts the connector, use **Windows Apps and Features** to uninstall the connector.

2. To install the new version, use the procedure to install a new version of the connector. Be sure to check for any new or updated prerequisites when installing a newer version of a connector:
   - SCEP: [Configure infrastructure to support SCEP with Intune](certificates-scep-configure.md)
   - PKCS: [Download, install, and configure the PFX Certificate Connector for Microsoft Intune](certificates-imported-pfx-configure.md)

## Connector status and version

In the Microsoft Endpoint Manager admin center, you can select a certificate connector to view information about its status and confirm its version:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

3. Select a connector to view its status.

When viewing the connector status:

- Deprecated connectors will show with a **Warning**. After the six-month grace period, the warning changes to an Error.
- Connectors that are beyond the grace period show an Error. These connectors are no longer supported and can stop working at any time.

## What's new for Connectors

Updates for the two certificate connectors are released periodically. When we update a connector, you can read about the changes here.

### PFX Certificate Connector release history

The *PFX Certificate Connector for Microsoft Intune* [supports automatic updates](#automatic-update).

#### August 26, 2020

**Version 6.2008.60.607** - Changes in this release:

- Requires .NET Framework version 4.7.2
- Replaces the use of the *Microsoft Intune Connector* for use with PKCS certificate profiles. The *PFX Certificate Connector* is now the only connector required to use PCKS #12 or Imported PFX certificates.
- Adds support for using PKCS certificate profiles with all supported platforms except Windows 8.1.
- Adds support for certificate revocation for Outlook S/MIME.

#### November 18, 2019

**Version: 6.1911.11.602** - Changes in this release:

- Added S/MIME support for PFX Import.  

#### May 17, 2019

**Version 6.1905.0.404** - Changes in this release:

- Fixed an issue where existing PFX certificates continue to be reprocessed which causes the connector to stop processing new requests. 

#### May 6, 2019

**Version 6.1905.0.402** - Changes in this release:

- The polling interval for the connector is reduced from 5 minutes to 30 seconds.

#### April 2, 2019

**Version 6.1904.0.401** - Changes in this release:

- This connector now supports automatic update.
- Fixed an issue where the connector might fail to enroll to Intune after signing in to the connector with a global administrator account.

### Microsoft Intune Connector release history

#### April 2, 2019

**Version 6.1904.1.0** - Changes in this release:  

- Fixed an issue where the connector might fail to enroll to Intune after signing in to the connector with a global administrator account.
- Includes reliability fixes to certificate revocation.
- Includes performance fixes to increase how quickly PKCS certificate requests are processed.

## Next steps

Create SCEP, PKCS, or PKCS imported certificate profiles for each platform you want to use. To continue, see the following articles:

- [Configure infrastructure to support SCEP certificates with Intune](certificates-scep-configure.md)  
- [Configure and manage PKCS certificates with Intune](certficates-pfx-configure.md)  
- [Create a PKCS imported certificate profile](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
