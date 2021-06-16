---
# required metadata

title: Overview of Certificate Connector for Microsoft Intune - Azure | Microsoft Docs
description: Learn about the unified Certificate Connector for Microsoft Intune, which supports SCEP, PKCS, imported PKCS, and certificate revocation. 
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


# Certificate Connector for Microsoft Intune

For Microsoft Intune to support use of certificates for authentication and the signing and encryption of email using S/MIME, you can use the Certificate Connector for Microsoft Intune. The certificate connector is software you install on an on-premises server to help deliver and manage certificates for your Intune-managed devices.

This article introduces the Certificate Connector for Microsoft Intune, its lifecycle, and how to keep it up to date.

> [!TIP]
> Beginning on June 21, 2021, the **Certificate Connector for Microsoft** Intune replaces the use of *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*. The new connector includes the functionality of both previous connectors. Although the [previous connectors remain in support](../protect/certificate-connectors.md), they are no longer available for download.  If you need to install a new connector, or reinstall a connector, install the newer Certificate Connector for Microsoft Intune.

## Connector overview

To use the certificate connector, you’ll first download software from within the Microsoft Endpoint Manager admin center, which you’ll then install on a Windows Server.

During the installation, you can install one or more connector features, including support for:

- Private and public key pair (PKCS) certificates
- PKCS imported certificates
- Simple Certificate Enrollment Protocol (SCEP)
- Certificate revocation

You'll also assign a service account to run the connector. This account is used for all interactions with your Certification Authority, and for certificate issuance, revocation, and renewal. Supported options for the service account include the connector servers SYSTEM account, a Domain account, or a Managed service account from Azure Active Directory (Azure AD).

After the connector installs, you can run configuration of the connector again at any time to update it or change the features you’ve installed. After it's installed and configured, the connector can automatically install future updates to keep your connectors current to the most recent release.

## Capabilities of the certificate connector

The Certificate Connector for Microsoft Intune supports:

- PCKS #12 certificate requests.

- PKCS imported certificates (PFX file) for S/MIME email encryption for a specific user.

- Issuing Simple Certificate Enrollment Protocol (SCEP) certificates. When you use an Active Directory Certificate Services Certification Authority (CA), also called a *Microsoft CA*, you must also configure the Network Device Enrollment Service (NDES) on the server that hosts the connector.

  Use of SCEP with a third-party Certification Authority, doesn’t require use of the Certificate Connector for Microsoft Intune.

- Certificate revocation.

- Automatic updates](#automatic-update) to new versions. When servers that host the certificate connector can access the internet, they automatically install new updates to stay current. When a connector fails to automatically update, you can manually update the connector.

- Installation of up to 100 instances of the connector per Intune tenant, with each instance on a separate Windows Server. When you use multiple connectors:
  - Each instance of the connector must have access to the private key used to encrypt the passwords of each uploaded PFX file.
  - Each instance of the connector should be at the same version. Because the connector supports automatic updates to the newest version, updates can be managed for you by Intune.  
  - Your infrastructure supports redundancy and load balancing, as any available connector instance that supports the same connector features can process your certificate requests.

    >[!NOTE]
    > Any instance of the connector that supports PKCS can be used to retrieve pending PKCS requests from the Intune Service queue. It's not possible to define which connector handles each request. </br></br>
    > Therefore, each connector that supports PKCS must have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.

- *Federal Information Processing Standard* (FIPS) mode. FIPS isn't required. When FIPS is enabled, you can issue and revoke certificates.

- Installation of multiple instances of the connector in a single Intune tenant. You can configure a proxy to allow the connector to communicate with Intune.

- The same network requirements as [managed devices](../fundamentals/intune-endpoints.md#access-for-managed-devices). For more information, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).



## Connector architecture

***Pending details***



## Connector lifecycle

Periodically, updates  to the certificate connector are released. Announcements for new connector releases appear in the [What’s New](../fundamentals/whats-new.md) article for Intune and in the [What's new for the Certificate Connector](#whats-new-for-the-certificate-connector) section near the end of this article.

When a new version releases, support for the previous version is deprecated with a limited grace period for its continued use. After the grace period expires, support for that deprecated version ends, and it can stop functioning at any time. The grace period is six months.

If you don’t allow the connector to automatically update, plan to manually update it to the latest version at the first opportunity.

### Automatic update

Intune can automatically update the connector to the latest version shortly after that connector version is released.

To update automatically, the server that hosts the connector must access the **Azure update service**:

- Port: **443**
- Endpoint: **autoupdate.msappproxy.net**

When firewalls, infrastructure, or network configurations limit access for automatic update, resolve the blocking issues or manually update the connector to the new version.

### Manual update

The process to manually update a certificate connector is the same for reinstalling a connector.

You can manually update a certificate connector even when it supports automatic updates. For example, you can manually update the connector when your network configuration blocks an automatic update.

### Reinstall a certificate connector

1. On the Windows Server that hosts the connector, use **Windows Apps and Features** to uninstall the connector.

2. To install the new version, use the procedure to install a new version of the connector. Be sure to check for any new or updated [prerequisites](../protect/certificate-connector-prerequisites.md) when installing a newer version of a connector.

## Connector status

In the Microsoft Endpoint Manager admin center, you can select a certificate connector to view information about its status:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

3. Select a connector to view its status.

When viewing the connector status:

- Deprecated connectors show a **Warning**. After the six-month grace period, the warning changes to an Error.
- Connectors that are beyond the grace period show an Error. These connectors are no longer supported and can stop working at any time.

## Logging

Logs for the Certificate Connector for Microsoft Intune are available as Event logs on the server where the connector is installed:

- **Event Viewer** > **Application and Service Logs** > **Microsoft** > **Intune** > **Certificate Connectors**

The following logs are available and default to 50 MB, and have automatic archiving enabled:

- **Admin Log** - This log contains one log event per request to the connector. Events include either a *success* with information about the request, or an *error* with information about the request and the error.
- **Operational Log** - This log displays additional information to that found in the Admin log, and can be of use in debugging issues. This log also displays ongoing operations instead of single events.

### Event IDs

All events have one of the following IDs:

- **0001-0999** - Not associated with any specific scenario
- **1000-1999** - PKCS
- **2000-2999** - PKCS Import
- **3000-3999** - Revoke
- **4000-4999** - SCEP

### Task Categories

All events are tagged with a Task Category to aid in filtering.  Task categories contain but aren't limited to the following list:

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

**SCEP**
- **Admin**
  - *Details pending*
- **Operational**
  - *Details pending*
 
## What's new for the Certificate Connector

Updates for the Certificate Connector for Microsoft Intune are released periodically. When we update the connector, you can read about the changes here.

### June 21, 2021

The Certificate Connector for Microsoft Intune is released. This connector is a unified connector in that it includes the capabilities of both the *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*, which it replaces.  With this release, the previous connectors remain supported, but are no longer developed nor available for download. Plan to replace existing installations of the individual with installations of this new unified connector. 

## Next steps

[Review prerequisites for the Certificate Connector for Microsoft Intune](../protect/certificate-connector-prerequisites.md)
