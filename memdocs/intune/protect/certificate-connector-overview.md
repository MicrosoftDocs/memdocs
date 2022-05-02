---
# required metadata

title: Overview of Certificate Connector for Microsoft Intune - Azure | Microsoft Docs
description: Learn about the unified Certificate Connector for Microsoft Intune, which supports SCEP, PKCS, imported PKCS, and certificate revocation. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2022
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
> Beginning on July 29, 2021, the **Certificate Connector for Microsoft Intune** replaces the use of *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*. The new connector includes the functionality of both previous connectors. With the release of version 6.2109.51.0 of the Certificate Connector for Microsoft, the previous connectors are no longer supported.

## Connector overview

To use the certificate connector, you’ll first download software from within the Microsoft Endpoint Manager admin center, which you’ll then install on a Windows Server.

During the installation, you can install one or more connector features, including support for:

- Private and public key pair (PKCS) certificates
- PKCS imported certificates
- Simple Certificate Enrollment Protocol (SCEP)
- Certificate revocation

You'll also assign a service account to run the connector. This account is used for all interactions with your Certification Authority, and for certificate issuance, revocation, and renewal. Supported options for the service account include the connector servers SYSTEM account or a Domain account.

After the connector installs, you can run configuration of the connector again at any time to update it or change the features you’ve installed. After it's installed and configured, the connector can automatically install future updates to keep your connectors current to the most recent release.

Intune supports installing of multiple instances of the connector in a tenant, and each instance can support different features. If you use multiple connectors that support different features, certificate requests are always routed to a relevant connector. For example, if you install two connectors that support PKCS, and install two more that support both PKCS and SCEP, certificate tasks for PKCS can be managed by any of the four connectors, but tasks for SCEP are only directed to the two connectors that support SCEP.
  
Each instance of the certificate connector has the same network requirements as devices that are managed by Intune. For more information, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), and [Intune network configuration requirements and bandwidth](../fundamentals/network-bandwidth-use.md).

## Capabilities of the certificate connector

The Certificate Connector for Microsoft Intune supports:

- PKCS #12 certificate requests.

- PKCS imported certificates (PFX file) for S/MIME email encryption for a specific user.

- Issuing Simple Certificate Enrollment Protocol (SCEP) certificates. When you use an Active Directory Certificate Services Certification Authority (CA), also called a *Microsoft CA*, you must also configure the Network Device Enrollment Service (NDES) on the server that hosts the connector.

  Use of SCEP with a third-party Certification Authority, doesn’t require use of the Certificate Connector for Microsoft Intune.

- Certificate revocation.

- [Automatic updates](#automatic-update) to new versions. When servers that host the certificate connector can access the internet, they automatically install new updates to stay current. When a connector fails to automatically update, you can manually update the connector.

- Installation of up to 100 instances of the connector per Intune tenant, with each instance on a separate Windows Server. When you use multiple connectors:
  - Each instance of the connector must have access to the private key used to encrypt the passwords of each uploaded PFX file.
  - Each instance of the connector should be at the same version. Because the connector supports automatic updates to the newest version, updates can be managed for you by Intune.  
  - Your infrastructure supports redundancy and load balancing, as any available connector instance that supports the same connector features can process your certificate requests.
  - You can configure a proxy to allow the connector to communicate with Intune.

    >[!NOTE]
    > Any instance of the connector that supports PKCS can be used to retrieve pending PKCS requests from the Intune Service queue, process Imported certificates, and handle revocation requests. It's not possible to define which connector handles each request. </br></br>
    > Therefore, each connector that supports PKCS must have the same permissions and be able to connect with all the certification authorities defined later in the PKCS profiles.

## Lifecycle

Periodically, updates  to the certificate connector are released. Announcements for new updates appear in the [What's new for the Certificate Connector](#whats-new-for-the-certificate-connector) section in this article.

Intune supports each connector release for six months after it's released. After the six months have passed, the connector is no longer supported and might not function as expected.

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

1. On the Windows Server that hosts the connector, run the connector installation program to uninstall the connector.

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

In addition to the default log level, you can enable debug logging for each log to obtain additional details.
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

  - **Event ID: 1000** - *PkcsRequestSuccess*  
    Successfully uploaded a PKCS Request to Intune.

  - **Event ID: 1001** - *PkcsRequestFailure*  
    Failed to fulfill or upload a PKCS Request to Intune.

  - **Event ID: 1200** - *PkcsRecryptRequestSuccess*  
    Successfully processed PKCS Reencrypt request.

  - **Event ID: 1201** - *PkcsRecryptRequestFailure*  
    Failed to process PKCS Reencrypt request.

- **Operational**

  - **Event ID: 1002** - *PkcsDownloadSuccess*  
    Successfully downloaded PKCS requests from Intune.

  - **Event ID: 1003** - *PkcsDownloadFailure*  
    Failed to download PKCS requests from Intune.

  - **Event ID: 1020** - *PkcsDownloadedRequest*  
    Successfully downloaded PKCS request from Intune

  - **Event ID: 1032** - *PkcsDigiCertRequest*  
    Successfully downloaded a PKCS request for DigiCert CA from Intune.

  - **Event ID: 1050** - *PkcsIssuedSuccess*  
    Successfully issued a PKCS certificate.

  - **Event ID: 1051** - *PkcsIssuedFailedAttempt*  
    Failed to issue a PKCS certificate, will try again.

  - **Event ID: 1052** - *PkcsIssuedFailure*  
    Failed to issue a PKCS certificate.

  - **Event ID: 1100** - *PkcsUploadSuccess*  
    Successfully uploaded PKCS request results to Intune.

  - **Event ID: 1101** - *PkcsUploadFailure*  
    Failed to upload PKCS request results to Intune.

  - **Event ID: 1102** - *PkcsUploadedRequest*  
    Successfully uploaded PKCS request to Intune.

  - **Event ID: 1202** - *PkcsRecryptDownloadSuccess*  
    Successfully downloaded PKCS Reencrypt requests.

  - **Event ID: 1203** - *PkcsRecryptDownloadFailure*  
    Failed to download PKCS Reencrypt requests.

  - **Event ID: 1220** - *PkcsRecryptDownloadedRequest*  
    Successfully downloaded a PKCS Reencrypt request.

  - **Event ID: 1250** - *PkcsRecryptReencryptSuccess*  
    Successfully re-encrypted PKCS certificate payload.

  - **Event ID: 1251** - *PkcsRecryptDecryptSuccess*  
    Successfully decrypted PKCS certificate payload.

  - **Event ID: 1252** - *PkcsRecryptDecryptFailure*  
    Failed to decrypt PKCS certificate payload.

  - **Event ID: 1253** - *PkcsRecryptReencryptFailure*  
    Failed to re-encrypt PKCS certificate payload.

  - **Event ID: 1300** - *PkcsRecryptUploadSuccess*  
    Successfully uploaded PKCS Reencrypt request results to Intune.

  - **Event ID: 1301** - *PkcsRecryptUploadFailure*  
    Failed to upload PKCS Reencrypt request results to Intune.

  - **Event ID: 1302** - *PkcsRecryptUploadedRequest*  
    Successfully uploaded a PKCS Reencrypt request to Intune.

**PKCS Import**  

- **Admin**  

  - **Event ID: 2000** - *PkcsImportRequestSuccess*  
    Successfully downloaded PKCS Import requests from Intune.

  - **Event ID: 2001** - *PkcsImportRequestFailure*  
    Failed to process a PKCS Import request from Intune.

- **Operational**  

  - **Event ID: 2202** - *PkcsImportDownloadSuccess*  
    Successfully downloaded PKCS Import requests from Intune.

  - **Event ID: 2203** - *PkcsImportDownloadFailure*  
    Failed to download PKCS Import requests from Intune.

  - **Event ID: 2020** - *PkcsImportDownloadedRequest*  
    Successfully downloaded a PKCS Import request from Intune.

  - **Event ID: 2050** - *PkcsImportReencryptSuccess*  
    Successfully re-encrypted a PKCS Import certificate.

  - **Event ID: 2051** - *PkcsImportReencryptFailedAttempt*  
    Failed to re-encrypt a PKCS Import certificate, will try again.

  - **Event ID: 2052** - *PkcsImportReencryptFailure*  
    Failed to re-encrypt an imported certificate.

  - **Event ID: 2100** - *PkcsImportUploadSuccess*  
    Successfully uploaded PKCS Import request results to Intune.

  - **Event ID: 2101** - *PkcsImportUploadFailure*  
    Failed to upoload PKCS request results to Intune.

  - **Event ID: 2102** - *PkcsImportUploadedRequest*  
    Successfully uploaded a PKCS Import request to Intune.

**Revocation**  

- **Admin**  

  - **Event ID: 3000** - *RevokeRequestSuccess*  
    Successfully downloaded Revocation requests from Intune.

  - **Event ID: 3001** - *RevokeRequestFailure*  
    A failure occurred when downloading Revocation requests from Intune.

- **Operational**

  - **Event ID: 3002** - *RevokeDownloadSuccess*  
    Successfully downloaded Revocation requests from Intune.

  - **Event ID: 3003** - *RevokeDownloadFailure*  
    A failure occurred when downloading Revocation requests from Intune.

  - **Event ID: 3020** - *RevokeDownloadedRequest*  
    Details of a single downloaded request from Intune

  - **Event ID:  3032** - *RevokeDigicertRequest*  
    Received revoke request from Intune and forwarding request to Digicert for fulfillment of request.

  - **Event ID: 3050** - *RevokeSuccess*  
    Successfully revoked certificate.

  - **Event ID: 3051** - *RevokeFailure*  
    A failure occurred while revoking a certificate.

  - **Event ID: 3052** - *RevokeFailedAttempt*  
    Failed to revoke a certificate, will try again.

  - **Event ID: 3100** - *RevokeUploadSuccess*  
    Successfully uploaded Revocation request results to Intune.

  - **Event ID: 3101** - *RevokeUploadFailure*  
    Failed to upload Revocation request results to Intune.

  - **Event ID: 3102** - *RevokeUploadedRequest*  
    Successfully uploaded Revocation request to Intune.

**SCEP**

- **Admin**

  - **Event ID: 4000** - *ScrepRequestSuccess*  
    Successfully processed a SCEP request and notified Intune.

  - **Event ID: 4001** - *ScepRequestIssuedFailure*  
    Failed to process a SCEP request and notified Intune.

  - **Event ID: 4002** - *ScepRequestUploadFailure*  
    Successfully processed SCEP request but failed to notify Intune.

- **Operational**

  - **Event ID: 4003** - *ScepRequestReceived*  
    Successfully received a SCEP request from a device.

  - **Event ID: 4004** - *ScepVerifySuccess*  
    Successfully verified a SCEP request with Intune.

  - **Event ID: 4005** - *ScepVerifyFailure*  
    Failed to verify a SCEP request with Intune.

  - **Event ID: 4006** - *ScepIssuedSuccess*  
    Successfully issued certificate for a SCEP request.

  - **Event ID: 4007** - *ScepIssuedFailure*  
    Failed to issue certificate for SCEP request.

  - **Event ID: 4008** - *ScepNotifySuccess*  
    Successfully notified Intune of the result for a SCEP request.

  - **Event ID: 4009** - *ScepNotifyAttemptFailed*  
    Failed to notify Intune of the result of a SCEP request, will try again.

  - **Event ID: 4010** - *ScepNotifySaveToDiskFailed*  
    Failed to write notification to disk and cannot notify Intune of the request status.

## What's new for the Certificate Connector

Updates for the Certificate Connector for Microsoft Intune are released periodically and then [supported for six months](#lifecycle). When we update the connector, you can read about the changes here.

New updates for the connector can take a week or more to become available for each tenant.

> [!IMPORTANT]  
> Starting April 2022, certificate connectors earlier than version **6.2101.13.0** will be deprecated and will show a status of *Error*. This status does not affect functionality. Starting June 2022, such connectors will not be able to issue certificates. This includes both the [PFX Certificate Connector for Microsoft Intune](../protect/certificate-connectors.md#pfx-certificate-connector-release-history) and  [Microsoft Intune Connector](../protect/certificate-connectors.md#microsoft-intune-connector-release-history), which on July 29, 2021 were replaced by the *Certificate Connector for Microsoft Intune* (as detailed in this article).

### March 10, 2022

Version **6.2202.38.0**. This update includes:

- Changes to support TLS 1.2 for auto-update

### February 18, 2022

Version **6.2201.7.0**. This update includes:

- Support changes for account moves
- Explicit disabling for older versions of TLS

### January 6, 2022

Version **6.2112.1.0**. This update includes:

- New configuration logging on startup of services
- New logging for configuration changes during service processing
- Fix for configuration tool to appropriately clear proxy information on removal
- Bug fix affecting reconnections to Intune in scenarios where proxies are in use

### October 11, 2021

Version **6.2110.201.0**. This update includes:

- Bug fix for reading the SCEP application pool during configuration.

### September 23, 2021

Version **6.2109.51.0**. - With the release of this update, support ends for the two previous certificate connectors, *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*.

This update includes:

- Additional logging for Digicert PKCS requests
- Enhancement to cryptography operations made during handling of PKCS requests

### August 16, 2021

Version **6.2108.18.0**. This update includes:

- A fix to correctly display the current connector status in Microsoft Endpoint Manager admin center.
- A fix to correctly report on failures to deliver SCEP certificates.

### July 29, 2021

Version **6.2107.45.0** - The Certificate Connector for Microsoft Intune is released.

This connector is a unified connector in that it includes the capabilities of both the *PFX Certificate Connector for Microsoft Intune* and *Microsoft Intune Connector*, which it replaces.  With this release, the previous connectors remain supported, but are no longer developed nor available for download. Plan to replace existing installations of the individual with installations of this new unified connector.


## Next steps

[Review prerequisites for the Certificate Connector for Microsoft Intune](../protect/certificate-connector-prerequisites.md)
