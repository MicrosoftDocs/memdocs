---
title: Configure CMG client authentication
titleSuffix: Configuration Manager
description: Configure authentication methods for clients to use a cloud management gateway (CMG).
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Configure client authentication for cloud management gateway

*Applies to: Configuration Manager (current branch)*

The next step in the setup of a cloud management gateway (CMG) is to configure how clients authenticate. Because these clients are potentially connecting to the service from the untrusted public internet, they have a higher authentication requirement. There are three options:

- Azure Active Directory (Azure AD)
- PKI certificates
- Configuration Manager site-issued tokens

This article describes how to configure each of these options. For more foundational information, see [Plan for CMG client authentication methods](plan-client-authentication.md).

## Azure AD

If your internet-based devices are running Windows 10 or later, use Azure AD modern authentication with the CMG. This authentication method is the only one that enables user-centric scenarios.

This authentication method requires the following configurations:

- The devices need to be either cloud domain-joined or hybrid Azure AD-joined, and the user also needs an Azure AD identity.

  > [!TIP]
  > To check if a device is cloud-joined, run `dsregcmd.exe /status` in a command prompt. If the device is Azure AD-joined or hybrid-joined, the **AzureAdjoined** field in the results shows **YES**. For more information, see [dsregcmd command - device state](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

- One of the primary requirements for using Azure AD authentication for internet-based clients with a CMG is to integrate the site with Azure AD. You already completed that action in the [prior step](configure-azure-ad.md).

- There are a few other requirements, depending upon your environment:

  - Enable user discovery methods for hybrid identities
  - Enable ASP.NET 4.5 on the management point
  - Configure client settings

For more information on these prerequisites, see [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md).

## PKI certificate

Use these steps if you have a public key infrastructure (PKI) that can issue client authentication certificates to devices.

This certificate may be required on the CMG connection point. For more information, see [CMG connection point](#cmg-connection-point).

### Issue the certificate

Create and issue this certificate from your PKI, which is outside of the context of Configuration Manager. For example, you can use Active Directory Certificate Services and group policy to automatically issue client authentication certificates to domain-joined devices. For more information, see [Example deployment of PKI certificates: Deploy the client certificate](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

The CMG client authentication certificate supports the following configurations:

- 2048-bit or 4096-bit key length

- This certificate supports key storage providers for certificate private keys (v3). For more information, see [CNG v3 certificates overview](../../../plan-design/network/cng-certificates-overview.md).

### Export the client certificate's trusted root

The CMG has to trust the client authentication certificates to establish the HTTPS channel with clients. To accomplish this trust, export the trusted root certificate chain. Then supply these certificates when you create the CMG in the Configuration Manager console.

Make sure to export all certificates in the trust chain. For example, if the client authentication certificate is issued by an intermediate CA, export both the intermediate and root CA certificates.

> [!NOTE]
> Export this certificate when any client uses PKI certificates for authentication. When all clients use either Azure AD or tokens for authentication, this certificate isn't required.

After you issue a client authentication certificate to a computer, use this process on that computer to export the trusted root certificate.

1. Open the Start menu. Type "run" to open the Run window. Open `mmc`.

1. From the File menu, choose **Add/Remove Snap-in...**.

1. In the Add or Remove Snap-ins dialog box, select **Certificates**, then select **Add**.

    1. In the Certificates snap-in dialog box, select **Computer account**, then select **Next**.

    1. In the Select Computer dialog box, select **Local computer**, then select **Finish**.

    1. In the Add or Remove Snap-ins dialog box, select **OK**.

1. Expand **Certificates**, expand **Personal**, and select **Certificates**.

1. Select a certificate whose Intended Purpose is **Client Authentication**.

    1. From the Action menu, select **Open**.

    1. Go to the **Certification Path** tab.

    1. Select the next certificate up the chain, and select **View Certificate**.

1. On this new Certificate dialog box, go to the **Details** tab. Select **Copy to File...**.

1. Complete the Certificate Export Wizard using the default certificate format, **DER encoded binary X.509 (.CER)**. Make note of the name and location of the exported certificate.

1. Export all of the certificates in the certification path of the original client authentication certificate. Make note of which exported certificates are intermediate CAs, and which ones are trusted root CAs.

### CMG connection point

To securely forward client requests, the CMG connection point requires a secure connection with the management point. If you're using PKI client authentication, and the internet-enabled management point is HTTPS, issue a client authentication certificate to the site system server with the CMG connection point role.

> [!NOTE]
> The CMG connection point doesn't require a client authentication certificate in the following scenarios:
>
> - Clients use Azure AD authentication.
> - Clients use Configuration Manager token-based authentication.
> - The site uses Enhanced HTTP.

For more information, see [Enable management point for HTTPS](#enable-management-point-for-https).

## Site token

If you can't join devices to Azure AD or use PKI client authentication certificates, then use Configuration Manager token-based authentication. For more information, or to create a bulk registration token, see [Token-based authentication for cloud management gateway](../../deploy/deploy-clients-cmg-token.md).

## Enable management point for HTTPS

Depending upon how you configure the site, and which client authentication method you choose, you may need to reconfigure your internet-enabled management points. There are two options:

- Configure the site for Enhanced HTTP, and configure the management point for HTTP
- Configure the management point for HTTPS

### Configure the site for Enhanced HTTP

When you use the site option to **Use Configuration Manager-generated certificates for HTTP site systems**, you can configure the management point for HTTP. When you enable Enhanced HTTP, the site server generates a self-signed certificate named **SMS Role SSL Certificate**. This certificate is issued by the root **SMS Issuing** certificate. The management point adds this certificate to the IIS Default Web site bound to port 443.

With this option, internal clients can continue to communicate with the management point using HTTP. Internet-based clients using Azure AD or a client authentication certificate can securely communicate through the CMG with this management point over HTTPS.

For more information, see [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md).

### Configure the management point for HTTPS

To configure a management point for HTTPS, first issue it a web server certificate. Then enable the role for HTTPS.

1. Create and issue a web server certificate from your PKI or a third-party provider, which are outside of the context of Configuration Manager. For example, use Active Directory Certificate Services and group policy to issue a web server certificate to the site system server with the management point role. For more information, see the following articles:

    - [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md)
    - [Example deployment of PKI certificates: Deploy the web server certificate for site systems that run IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)

1. On the properties of the management point role, set the client connections to **HTTPS**.

    > [!TIP]
    > After you set up the CMG, you'll configure other settings for this management point.

If your environment has multiple management points, you don't have to HTTPS-enable them all for CMG. Configure the CMG-enabled management points as **Internet only**. Then your on-premises clients don't try to use them.<!-- SCCMDocs#1676 -->

#### Management point client connection mode summary

These tables summarize whether the management point requires HTTP or HTTPS, depending upon the type of client. They use the following terms:

- *Workgroup*: The device isn't joined to a domain or Azure AD, but has a [client authentication certificate](#pki-certificate).
- *AD domain-joined*: You join the device to an on-premises Active Directory domain.
- *Azure AD-joined*: Also known as cloud domain-joined, you join the device to an Azure AD tenant. For more information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join).
- *Hybrid-joined*: You join the device to your on-premises Active Directory and register it with your Azure AD. For more information, see [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid).
- *HTTP*: On the management point properties, you set the client connections to **HTTP**.
- *HTTPS*: On the management point properties, you set the client connections to **HTTPS**.
- *E-HTTP*: On the site properties, **Communication Security** tab, you set the site system settings to **HTTPS or HTTP**, and you enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**. You configure the management point for HTTP, and the HTTP management point is ready for both HTTP and HTTPS communication.

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

##### For internet-based clients communicating with the CMG

Configure an on-premises management point to allow connections from the CMG with the following client connection mode:

| Internet-based client | Management point |
|------------------|------------------|
| Workgroup <sup>[Note 1](#bkmk_note1)</sup> | E-HTTP, HTTPS |
| AD domain-joined <sup>[Note 1](#bkmk_note1)</sup> | E-HTTP, HTTPS |
| Azure AD-joined  | E-HTTP, HTTPS |
| Hybrid-joined    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Note 1**: This configuration requires the client has a [client authentication certificate](#pki-certificate), and only supports device-centric scenarios.  

##### For on-premises clients communicating with the on-premises management point

Configure an on-premises management point with the following client connection mode:

| On-premises client | Management point |
|------------------|------------------|
| Workgroup        | HTTP, HTTPS |
| AD domain-joined | HTTP, HTTPS |
| Azure AD-joined  | HTTPS       |
| Hybrid-joined    | HTTP, HTTPS |

> [!NOTE]  
> On-premises AD domain-joined clients support both device- and user-centric scenarios communicating with an HTTP or HTTPS management point.
>
> On-premises Azure AD-joined and hybrid-joined clients can communicate via HTTP for device-centric scenarios, but need E-HTTP or HTTPS to enable user-centric scenarios. Otherwise they behave the same as workgroup clients.

## Next steps

You're now ready to create the CMG in Configuration Manager:
  
> [!div class="nextstepaction"]
> [Set up CMG](setup-cloud-management-gateway.md)
