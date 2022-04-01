---
# required metadata

title: Certificate connectors for Microsoft Intune
description: Learn about certificate connectors for Simple Certificate Enrollment Protocol (SCEP) or Public Key Cryptography Standards (PKCS) certificates and certificate profiles with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/28/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

ROBOTS: NOINDEX


#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Certificate connectors for Microsoft Intune

<!-- The details in this article are for deprecated functionality. These two connectors are no longer supported and this article will be retired at a future date. -->

> [!IMPORTANT]
> Beginning on July 29, 2021, the **Certificate Connector for Microsoft Intune** replaces the use of *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*. The new connector includes the functionality of both previous connectors. Support for the previous connectors that are described in this article, ended on 9/22/2021 with the release of version 6.2109.51.0 of the Certificate Connector for Microsoft.
>
> If you need to install a new certificate connector, or reinstall a connector, install the newer Certificate Connector for Microsoft Intune. For more information, see [Certificate Connector for Microsoft Intune](../protect/certificate-connector-overview.md).

To support the use of certificates for authentication and the signing and encryption of email using S/MIME, Intune requires the use of a certificate connector. A certificate connector is software you install on an on-premises server. The connector enables cloud-managed devices to provision certificates from on-premises infrastructure, like an issuing Certificate Authority.

## Available connectors

There are two certificate connectors for Intune. Each has its own uses and requirements.

### PFX Certificate Connector for Microsoft Intune

The **PFX Certificate Connector** supports certificate deployment for PKCS #12 certificate requests and handles requests for PFX files imported to Intune for S/MIME email encryption for a specific user.

> [!TIP]
> Prior to the August update for this connector (version 6.2008.60.607), PKCS #12 certificate requests were handled by the *Intune Certificate Connector*. With the August update, the functionality for all PKCS certificate requests was consolidated in the *PFX Certificate Connector*, which supports auto-update of the connector to new versions, and requires use of .NET Framework version 4.7.2.
>
> This connector also supports the following three platforms, that aren’t supported through the Microsoft Intune Connector:
>
> - Android Enterprise – Fully Managed
> - Android Enterprise – Dedicated
> - Android Enterprise – Corporate-Owned Work Profile  
>
> The functionality of the Microsoft Intune Connector isn't deprecated and you can continue use it with PKCS certificate profiles for some platforms. However, if you do not use SCEP or otherwise require use of NDES, you can switch to the PFX Certificate Connector and remove NDES from your servers.

**The PFX Certificate Connector**:

- Supports multiple instances of this connector for each Intune tenant. Each instance of the connector must install on a Windows Server and have access to the private key used to encrypt the passwords of the uploaded PFX files.
  > [!NOTE]
  > All connectors need to have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.
  >
  > Any instance of this connector can retrieve pending PKCS requests from the Intune Service queue, as such it's not possible to define which connector handles each request.
  >
  > The same applies to certificate revocation.
  >
- Can install on the same server that hosts an instance of the *Microsoft Intune Connector*.
- Supports up to 100 instances of this connector per tenant, with each instance on a separate Windows server. When you use multiple connectors:
  - All instances of the *PFX Certificate Connector* in your environment should be at the same version.
  - Your infrastructure supports redundancy and load balancing, as any available connector instance can process your certificate requests.
- Supports [automatic updates](#automatic-update) to new versions. To automatically install new versions, the computer that hosts the connector must contact **autoupdate.msappproxy.net** on port **443**. If the connector fails to automatically update, you can manually update the connector.
- Supports certificate revocation (requires the connector run version **6.2008.60.607** or later)
- Has the same network requirements as [managed devices](../fundamentals/intune-endpoints.md#access-for-managed-devices)

  For more information, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).

**The Windows server where the connector installs**:

- Must run Windows Server 2012 R2 or later.
- Run the .NET 4.7.2 Framework.  

**To install the PFX Certificate connector**:

For guidance installation of this connector, see [Download, install, and configure the PFX Certificate Connector](certificates-pfx-configure.md).

### Microsoft Intune Connector

The **Microsoft Intune Connector** is sometimes referred to as the *Microsoft Intune Certificate Connector*. This connector supports certificate deployment when you use *Simple Certificate Enrollment Protocol* (SCEP) and have an Active Directory Certificate Services Certification Authority (CA). This type of CA is also referred to as a *Microsoft CA*.

When you use SCEP with a Microsoft CA, you must also configure the **Network Device Enrollment Service** (NDES). For that reason, this connector is often referred to as the *NDES Certificate Connector*.

If  you use a [third-party Certification Authority](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), you don’t need to use this connector and NDES isn’t required.

**The Microsoft Intune Connector**:

- Supports issuing SCEP certificates
- Can be used to issue PKCS certificates to most device platforms, but not all. This connector doesn't support issuing of PKCS certificates to:
  - Android Enterprise – Fully Managed
  - Android Enterprise – Dedicated
  - Android Enterprise – Corporate-Owned Work Profile

  To support those platforms, use the *PFX Certificate Connector*, which supports issuing PKCS certificates to all device platforms. If you don’t use SCEP, you can then uninstall this connector, and use only the PFX Certificate Connector.
  > [!NOTE]
  > With PKCS, all connectors need to have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.
  >
  > Any instance of this connector can retrieve pending PKCS requests from the Intune Service queue, as such it's not possible to define which connector handles each request.
  >
  > The same applies to certificate revocation.
  >

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

> [!IMPORTANT]
> Beginning on July 29, 2021, the [**Certificate Connector for Microsoft Intune**](../protect/certificate-connector-overview.md) replaces the use of *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*. The new connector includes the functionality of both previous connectors.

Periodically, updated versions of certificate connectors are released. Announcements for new connector releases appear in the [What’s New](../fundamentals/whats-new.md) article for Intune and in the [What's new for Connectors](#whats-new-for-connectors) section near the end of this article.

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
   - PKCS: [Download, install, and configure the PFX Certificate Connector for Microsoft Intune](certificates-pfx-configure.md)

## Connector status <!-- and version -->

In the Microsoft Endpoint Manager admin center, you can select a certificate connector to view information about its status: <!-- and confirm its version: -->

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

3. Select a connector to view its status.

When viewing the connector status:

- Deprecated connectors will show with a **Warning**. After the six-month grace period, the warning changes to an Error.
- Connectors that are beyond the grace period show an Error. These connectors are no longer supported and can stop working at any time.

## Logging

*The following logging details are available beginning with connector version 6.2101.13.0.*

Logs for the PFX Certificate Connector are available as Event logs on the server where the connector is installed:

- **Event Viewer** > **Application and Service Logs** > **Microsoft** > **Intune** > **Certificate Connectors**

The following logs are available and default to 50 MB, with automatic archiving enabled:

- **Admin Log** - This log contains one log event per request to the connector. Events include either a *success* with information about the request, or an *error* with information about the request and the error.
- **Operational Log** - This log displays additional information than is found in the Admin log, and can be of use in debugging issues. This log also displays a ongoing operations for the PFX Certificate connector instead of single events.

### Event IDs

All events have one of the following IDs:

- **0001-0999** - Not associated with any specific scenario
- **1000-1999** - PKCS
- **2000-2999** - PKCS Import
- **3000-3999** - Revoke

### Task Categories

All events are tagged with a Task Category to aid in filtering.  Task categories contain but are not limited to the following list:

**PKCS**  
- **Admin**  
  - *PkcsRequestSuccess* - Successfully fulfilled and uploaded a PKCS Request to Intune.
  - *PkcsRequestFailure* - Failed to fulfill or upload a PKCS Request to Intune.
- **Operational**
  - *PkcsDownloadSuccess* - Successfully downloaded PKCS requests from Intune
  - *PkcsDownloadFailure* - A failure occurred when downloading PKCS requests from Intune
  - *PkcsDownloadedRequest* - Details of a single downloaded request from Intune
  - *PkcsIssuedSuccess* - Issued a certificate for a request
  - *PkcsIssuedFailedAttempt* - A failure occurred while issuing a certificate for a request
  - *PkcsIssuedFailure* - Failed to issue a certificate for a Request
  - *PkcsUploadSuccess* - Details of successful request that was uploaded to Intune
  - *PkcsUploadFailure* - A failure occurred when uploading requests to  Intune
  - *PkcsUploadedRequest* - Details of an uploaded request to Intune

**PKCS Import**  
- **Admin**  
  - *PkcsImportRequestSuccess* - Successfully downloaded PKCS Import requests from Intune
  - *PkcsImportRequestFailure* - A failure occurred when downloading PKCS Import requests from Intune
- **Operational**
  - *PkcsImportDownloadSuccess* - Successfully downloaded PKCS Import requests from Intune
  - *PkcsImportDownloadFailure* - A failure occurred when downloading PKCS Import requests from Intune
  - *PkcsImportDownloadedRequest* - Details of a single downloaded request from Intune
  - *PkcsImportReencryptSuccess* - Re-encrypted an imported certificate
  - *PkcsImportReencryptFailedAttempt* - A failure occurred while re-encrypting an imported certificate
  - *PkcsImportReencryptFailure* - Failed to re-encrypt an imported certificate
  - *PkcsImportUploadFailure* - A failure occurred when uploading requests to Intune
  - *PkcsImportUploadedRequest* - Details of an uploaded request to Intune

**Revocation**
- **Admin**
  - *RevokeRequestSuccess* - Successfully downloaded Revocation requests from Intune
  - *RevokeRequestFailure* - A failure occurred when downloading Revocation requests from Intune
- **Operational**
  - *RevokeDownloadSuccess* - Successfully downloaded Revocation requests from Intune
  - *RevokeDownloadFailure* - A failure occurred when downloading Revocation requests from Intune
  - *RevokeDownloadedRequest* - Details of a single downloaded request from Intune
  - *RevokeSuccess* - Successfully revoked certificate
  - *RevokeFailure* - A failure occurred while revoking a certificate
  - *RevokeFailedAttempt* - Failed to revoke a certificate
  - *RevokeUploadSuccess* - Details of successful request that was uploaded to Intune
  - *RevokeUploadFailure* - A failure occurred when uploading requests to Intune
  - *RevokeUploadedRequest* - Details of an uploaded request to Intune

## What's new for Connectors

Updates for the two certificate connectors are released periodically. When we update a connector, you can read about the changes here.

> [!IMPORTANT]
> On June 1, 2022, Intune certificate connectors earlier than version 6.2101.13.0 will no longer allow you to issue certificates to users and devices. See the note at the to start of this article for detail on moving to the new **Certificate Connector for Microsoft**.

### PFX Certificate Connector release history

The *PFX Certificate Connector for Microsoft Intune* [supports automatic updates](#automatic-update).

#### March 10, 2021

Version **6.2101.16.0**. - Changes in this release:

- Improvements to to the PFX Create flow to prevent duplication of Certificate Request files on on-premises servers that host the connector.

#### February 24, 2021

Version **6.2101.13.0**. This new connector version adds [improvements for logging](#logging) to the PFX Connector:

- New location for Event Logs, with logs broken down into Admin, Operational & Debug
- Admin & Operational logs default to 50 MB - with auto archiving enabled.
- EventIDs for PKCS Import, PKCS Create and Revocation.

#### January 26, 2021

**Version 6.2009.2.0** - Changes in this release:

- Improves upgrade of the Connector to persist accounts that run Connector Services.

#### January 15, 2021

**Version 6.2009.1.9** - Changes in this release:

- Improvements to the renewal of the connector certificate.

#### October 2, 2020

**Version 6.2008.60.612** - Changes in this release:

- Fixed an issue with PKCS certificate delivery to Android Enterprise Fully Managed devices. The issue required the cryptography Key Storage Provider (KSP) be a legacy provider. You can now use a Cryptographic Next Generation (CNG) Key Storage Provider as well.
- Changes to *CA Account* tab of the PFX Certificate Connector: The Username and password (credentials) that you specify are now used to issue certificates and to revoke certificates. Previously these credentials were used only for certificate revocation.

<!-- Rolling Archive for PFX Certificate Connector release history
 that are five or more releases old:

#### August 26, 2020

**Version 6.2008.60.607** - Changes in this release:

- Requires .NET Framework version 4.7.2
- Replaces the use of the *Microsoft Intune Connector* for use with PKCS certificate profiles. The *PFX Certificate Connector* is now the only connector required to use PKCS #12 or Imported PFX certificates.
- Adds support for using PKCS certificate profiles with all supported platforms except Windows 8.1.
- Adds support for certificate revocation for Outlook S/MIME.

#### November 18, 2019

**Version: 6.1911.11.602** - Changes in this release:

- Added S/MIME support for PFX Import.  
- 
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

End of PFX Certificate Connector release history archive -->

### Microsoft Intune Connector release history

#### April 2, 2019

**Version 6.1904.1.0** - Changes in this release:  

- Fixed an issue where the connector might fail to enroll to Intune after signing in to the connector with a global administrator account.
- Includes reliability fixes to certificate revocation.
- Includes performance fixes to increase how quickly PKCS certificate requests are processed.

## Next steps

Create SCEP, PKCS, or PKCS imported certificate profiles for each platform you want to use. To continue, see the following articles:

- [Configure infrastructure to support SCEP certificates with Intune](certificates-scep-configure.md)  
- [Configure and manage PKCS certificates with Intune](certificates-pfx-configure.md)  
- [Create a PKCS imported certificate profile](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
- [Troubleshoot issues for the Microsoft Intune Connector ](/troubleshoot/mem/intune/troubleshoot-certificate-connector-events)