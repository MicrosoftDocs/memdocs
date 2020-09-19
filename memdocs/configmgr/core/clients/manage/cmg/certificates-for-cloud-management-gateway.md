---
title: Certificates for CMG
titleSuffix: Configuration Manager
description: Learn about the different digital certificates to use with the cloud management gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/18/2020
ms.topic: reference
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
---

# Certificates for the cloud management gateway

*Applies to: Configuration Manager (current branch)*

Depending upon the scenario you use to manage clients on the internet with the cloud management gateway (CMG), you need one or more of the following digital certificates:  

- [CMG server authentication certificate](server-auth-cert.md)

- [Client authentication certificate](#bkmk_clientauth)
  - [CMG connection point](#bkmk_cmgcp)
  - [Client trusted root certificate to CMG](#bkmk_clientroot)  

- [Enable management point for HTTPS](#bkmk_mphttps)  

For more information about the different scenarios, see [Overview of CMG](overview.md).

## General information

<!--SCCMDocs issue #779-->
Certificates for the CMG support the following configurations:  

- 2048-bit or 4096-bit key length

- Key storage providers for certificate private keys. For more information, see [CNG certificates overview](../../../plan-design/network/cng-certificates-overview.md).  

- When you configure Windows with the following policy: **System cryptography: Use FIPS-compliant algorithms for encryption, hashing, and signing**  

- **TLS 1.2**. For more information, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="bkmk_serverauth"></a> CMG server authentication certificate

*This certificate is required in all scenarios.*

For more information, see [CMG server authentication certificate](server-auth-cert.md).

## <a name="bkmk_clientauth"></a> Client authentication certificate

Client authentication certificate requirements:

- This certificate is required for internet-based clients running Windows 8.1, and Windows 10 devices not joined to Azure Active Directory (Azure AD).
- It may be required on the CMG connection point. For more information, see [CMG connection point](#bkmk_cmgcp).
- It isn't required for Windows 10 clients joined to Azure AD.
- If your site is version 2002 or later, devices can use a token issued by the site. For more information, see [Token-based authentication for CMG](../../deploy/deploy-clients-cmg-token.md).

The clients use this certificate to authenticate with the CMG. Windows 10 devices that are hybrid or cloud domain-joined don't require this certificate because they use Azure AD to authenticate.

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue client authentication certificates. For more information, see [Deploying the client certificate for Windows computers](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

> [!NOTE]
> Microsoft recommends joining devices to Azure AD. Internet-based devices can use Azure AD to authenticate with Configuration Manager. It also enables both device and user scenarios whether the device is on the internet or connected to the internal network. For more information, see [Install and register the client using Azure AD identity](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Starting in version 2002,<!--5686290--> Configuration Manager extends its support for internet-based devices that don't often connect to the internal network, aren't able to join Azure AD, and don't have a method to install a PKI-issued certificate. For more information, see [Token-based authentication for CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="bkmk_cmgcp"></a> CMG connection point

To securely forward client requests, the CMG connection point requires a secure connection with the management point. Depending upon how you configure your devices and management points determines the CMG connection point configuration.

- The management point is HTTPS

  - Clients have a client authentication certificate: The CMG connection point requires a client authentication certificate that corresponds to the server authentication certificate on the HTTPS management point.

  - Clients use Azure AD authentication or a Configuration Manager token: This certificate isn't required.

- If you configure the management point for Enhanced HTTP: This certificate isn't required.

For more information, see [Enable management point for HTTPS](#bkmk_mphttps).

### <a name="bkmk_clientroot"></a> Client trusted root certificate to CMG

*This certificate is required when using client authentication certificates. When all clients use Azure AD for authentication, this certificate isn't required.*

You supply this certificate when creating the CMG in the Configuration Manager console.

The CMG must trust the client authentication certificates. To accomplish this trust, provide the trusted root certificate chain. Make sure to add all certificates in the trust chain. For example, if the client authentication certificate is issued by an intermediate CA, add both the intermediate and root CA certificates.

> [!NOTE]  
> When you create a CMG, you don't have to provide a trusted root certificate on the Settings page. This certificate isn't required when using Azure AD for client authentication. If you're using PKI client authentication certificates, then you still need to add a trusted root certificate to the CMG.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->

#### Export the client certificate's trusted root

After issuing a client authentication certificate to a computer, use this process on that computer to export the trusted root.

1. Open the Start menu. Type "run" to open the Run window. Open `mmc`.  

2. From the File menu, choose **Add/Remove Snap-in...**.  

3. In the Add or Remove Snap-ins dialog box, select **Certificates**, then select **Add**.  

    1. In the Certificates snap-in dialog box, select **Computer account**, then select **Next**.  

    1. In the Select Computer dialog box, select **Local computer**, then select **Finish**.  

    1. In the Add or Remove Snap-ins dialog box, select **OK**.  

4. Expand **Certificates**, expand **Personal**, and select **Certificates**.  

5. Select a certificate whose Intended Purpose is **Client Authentication**.  

    1. From the Action menu, select **Open**.  

    1. Go to the **Certification Path** tab.  

    1. Select the next certificate up the chain, and select **View Certificate**.  

6. On this new Certificate dialog box, go to the **Details** tab. Select **Copy to File...**.  

7. Complete the Certificate Export Wizard using the default certificate format, **DER encoded binary X.509 (.CER)**. Make note of the name and location of the exported certificate.  

8. Export all of the certificates in the certification path of the original client authentication certificate. Make note of which exported certificates are intermediate CAs, and which ones are trusted root CAs.  

## <a name="bkmk_mphttps"></a> Enable management point for HTTPS

Provision this certificate outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue a web server certificate. For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md) and [Deploy the web server certificate for site systems that run IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

When using the site option to **Use Configuration Manager-generated certificates for HTTP site systems**, the management point can be HTTP. For more information, see [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md).

> [!TIP]
> If you aren't using Enhanced HTTP, and your environment has multiple management points, you don't have to HTTPS-enable them all for CMG. Configure the CMG-enabled management points as **Internet only**. Then your on-premises clients don't try to use them.<!-- SCCMDocs#1676 -->

### Enhanced HTTP certificate for management points

When you enable Enhanced HTTP, the site server generates a self-signed certificate named **SMS Role SSL Certificate**, issued by the root SMS Issuing certificate. The management point adds this certificate to the IIS Default Web site bound to port 443.

### Management point client connection mode summary

These tables summarize whether the management point requires HTTP or HTTPS, depending upon the type of client and site version.

#### For internet-based clients communicating with the CMG

Configure an on-premises management point to allow connections from the CMG with the following client connection mode:

| Type of client   | Management point |
|------------------|------------------|
| Workgroup        | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| AD domain-joined | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| Azure AD-joined  | E-HTTP, HTTPS |
| Hybrid-joined    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Note 1**: This configuration requires the client has a [client authentication certificate](#bkmk_clientauth), and only supports device-centric scenarios.  

#### For on-premises clients communicating with the on-premises management point

Configure an on-premises management point with the following client connection mode:

| Type of client   | Management point |
|------------------|------------------|
| Workgroup        | HTTP, HTTPS |
| AD domain-joined | HTTP, HTTPS |
| Azure AD-joined  | HTTPS       |
| Hybrid-joined    | HTTP, HTTPS |

> [!NOTE]  
> AD domain-joined clients support both device- and user-centric scenarios communicating with an HTTP or HTTPS management point.  
>
> Azure AD-joined and hybrid-joined clients can communicate via HTTP for device-centric scenarios, but need E-HTTP or HTTPS to enable user-centric scenarios. Otherwise they behave the same as workgroup clients.  

#### Legend of terms

- *Workgroup*: The device isn't joined to a domain or Azure AD, but has a [client authentication certificate](#bkmk_clientauth).
- *AD domain-joined*: You join the device to an on-premises Active Directory domain.
- *Azure AD-joined*: Also known as cloud domain-joined, you join the device to an Azure AD tenant. For more information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join).
- *Hybrid-joined*: You join the device to your on-premises Active Directory and register it with your Azure AD. For more information, see [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid).
- *HTTP*: On the management point properties, you set the client connections to **HTTP**.
- *HTTPS*: On the management point properties, you set the client connections to **HTTPS**.
- *E-HTTP*: On the site properties, **Communication Security** tab, you set the site system settings to **HTTPS or HTTP**, and you enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**. You configure the management point for HTTP, the HTTP management point is ready for both HTTP and HTTPS communication (token auth scenarios).
