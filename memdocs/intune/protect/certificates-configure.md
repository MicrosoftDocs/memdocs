---
# required metadata

title: Learn about the types of certificate that are supported by Microsoft Intune
description: Learn about Microsoft Intune's support for Simple Certificate Enrollment Protocol (SCEP), Public Key Cryptography Standards (PKCS) certificates.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/03/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Use certificates for authentication in Microsoft Intune

Use certificates with Intune to authenticate your users to applications and corporate resources through VPN, Wi-Fi, or email profiles. When you use certificates to authenticate these connections, your end users won't need to enter usernames and passwords, which can make their access seamless. Certificates are also used for signing and encryption of email using S/MIME.

## Introduction to certificates with Intune

Certificates provide authenticated access without delay through the following two phases:

- Authentication phase: The user’s authenticity is checked to confirm the user is who they claim to be.
- Authorization phase: The user is subjected to conditions for which a determination is made on whether the user should be given access.

Typical use scenarios for certificates include:

- Network authentication (for example, 802.1x) with device or user certs
- Authenticating with VPN servers using device or user certs
- Signing e-mail based on user certs

Intune supports Simple Certificate Enrollment Protocol (SCEP), Public Key Cryptography Standards (PKCS), and imported PKCS certificates as methods to provision certificates on devices. The different provisioning methods have different requirements, and results. For example:

- SCEP provisions certificates that are unique to each request for the certificate.
- PKCS provisions each device with a unique certificate.
- With Imported PKCS, you can deploy the same certificate that you’ve exported from a source, like an email server, to multiple recipients. This shared certificate is useful to ensure all your users or devices can then decrypt emails that were encrypted by that certificate.

To provision a user or device with a specific type of certificate, Intune uses a certificate profile.

In addition to the three certificate types and provisioning methods, you’ll need a trusted root certificate from a trusted Certification Authority (CA). The CA can be an on-premises Microsoft Certification Authority, or a [third-party Certification Authority](certificate-authority-add-scep-overview.md). The trusted root certificate establishes a trust from the device to your root or intermediate (issuing) CA from which the other certificates are issued. To deploy this certificate, you use the *trusted certificate* profile, and deploy it to the same devices and users that will receive the certificate profiles for SCEP, PKCS, and imported PKCS.

> [!TIP]  
> Intune also supports use of [Derived credentials](derived-credentials.md) for environments that require use of smartcards.

### What’s required to use certificates

- **A Certification Authority**. Your CA is the source of trust that the certificates reference for authentication. You can use a Microsoft CA or a third-party CA.
- **On-premises infrastructure**. The infrastructure you’ll require depends on the certificate types you’ll use:
  - [SCEP](certificates-scep-configure.md)
  - [PKCS](certificates-pfx-configure.md)
  - [Imported PKCS](certificates-imported-pfx-configure.md)
- **A trusted root certificate**. Before you deploy SCEP or PKCS certificate profiles, deploy the trusted root certificate from your CA using a *trusted certificate* profile. This profile helps establish the trust from the device back to the CA and is required by the other certificate profiles.

With a trusted root certificate deployed, you’ll then be ready to deploy certificate profiles to provision users and devices with certificates for authentication.

### Which certificate profile to use

The following comparisons aren’t comprehensive but intended to help distinguish the use of the different certificate profile types.

| Profile type               | Details       |
|----------------------------|---------------|
| Trusted certificate        | Use to deploy the public key (certificate) from a root CA or intermediary CA to users and devices to establish a trust back to the source CA. Other certificate profiles require the trusted certificate profile and its root certificate.    |
| SCEP certificate           | Deploys a template for a certificate request to users and devices. Each certificate that’s provisioned using SCEP is unique and tied to the user or device that requests the certificate. <br><br>With SCEP, you can deploy certificates to devices that lack a user affinity, including use of SCEP to provision a certificate on KIOSK or user-less device.   |
| PKCS certificate           | Deploys a template for a certificate request that specifies a certificate type of either user or device. <br><br> - Requests for a certificate type of user always require user affinity.  When deployed to a user, each of the user’s devices receives a unique certificate. When deployed to a device with a user, that user is associated with the certificate for that device. When deployed to a userless device, no certificate is provisioned. <br> - Templates with a certificate type of device don’t require user affinity to provision a certificate. Deployment to a device provisions the device. Deployment to a user provisions the device the user is signed into with a certificate.   |
| PKCS imported certificate  | Deploys a single certificate to multiple devices and users, which supports scenarios like S/MIME signing and encryption. For example, by deploying the same certificate to each device, each device can decrypt email received from that same email server. <br><br>Other certificate deployment methods are insufficient for this scenario, as SCEP creates a unique certificate for each request, and PKCS associates a different certificate for each user, with different users receiving different certificates.    |

## Intune supported certificates and usage

| Type              | Authentication | S/MIME Signing | S/MIME encryption  |
|--|--|--|--|
| Public Key Cryptography Standards (PKCS) imported certificate |  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)|
| PKCS#12 (or PFX)    | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) |  |
| Simple Certificate Enrollment Protocol (SCEP)  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | |

To deploy these certificates, you'll create and assign certificate profiles to devices.

Each individual certificate profile you create supports a single platform. For example, if you use PKCS certificates, you'll create PKCS certificate profile for Android and a separate PKCS certificate profile for iOS/iPadOS. If you also use SCEP certificates for those two platforms, you'll create a SCEP certificate profile for Android, and another for iOS/iPadOS.

### General considerations when you use a Microsoft Certification Authority

When you use a Microsoft Certification Authority (CA):

- To use SCEP certificate profiles:
  - [setup a Network Device Enrollment Service (NDES) server](certificates-scep-configure.md#set-up-ndes) for use with Intune.
  - [Install the Certificate Connector for Microsoft Intune](certificate-connector-install.md).

- To use PKCS certificate profiles:
  - [Install the Certificate Connector for Microsoft Intune](certificate-connector-install.md).
  
- To use PKCS imported certificates:
  - [Install the Certificate Connector for Microsoft Intune](certificate-connector-install.md).
  - Export certificates from the certification authority and then import them to Microsoft Intune. See [the PFXImport PowerShell project](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Deploy certificates by using the following mechanisms:
  - [Trusted certificate profiles](certificates-trusted-root.md) to deploy the Trusted Root CA certificate from your root or intermediate (issuing) CA to devices
  - SCEP certificate profiles
  - PKCS certificate profiles
  - PKCS imported certificate profiles

### General considerations when you use a third-party Certification Authority

When you use a third-party (non-Microsoft) Certification Authority (CA):

- To use SCEP certificate profiles:
  - Configure integration with a third-party CA from [one of our supported partners](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). Setup includes following the instructions from the third-party CA to complete integration of their CA with Intune.
  - [Create an application in Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) that delegates rights to Intune to do SCEP certificate challenge validation.

- PKCS imported certificates require you to [Install the Certificate Connector for Microsoft Intune](certificate-connector-install.md).

- Deploy certificates by using the following mechanisms:
  - [Trusted certificate profiles](certificates-trusted-root.md#create-trusted-certificate-profiles) to deploy the Trusted Root CA certificate from your root or intermediate (issuing) CA to devices
  - SCEP certificate profiles
  - PKCS certificate profiles *(only supported with the [Digicert PKI Platform](certificates-digicert-configure.md))*
  - PKCS imported certificate profiles

## Supported platforms and certificate profiles

| Platform              | Trusted certificate profile | PKCS certificate profile | SCEP certificate profile | PKCS imported certificate profile  |
|--|--|--|--|---|
| Android device administrator | ![Supported](./media/certificates-configure/green-check.png) <br>*(see **Note 1**)*| ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)|  ![Supported](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - Fully Managed (Device Owner)   | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png) |  ![Supported](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Dedicated (Device Owner)   | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png)|
| Android Enterprise <br> - Corporate-Owned Work Profile   | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - Personally-Owned Work Profile    | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) |
| macOS                 | ![Supported](./media/certificates-configure/green-check.png) |  ![Supported](./media/certificates-configure/green-check.png) |![Supported](./media/certificates-configure/green-check.png)|![Supported](./media/certificates-configure/green-check.png)|
| Windows 8.1 and later |![Supported](./media/certificates-configure/green-check.png)  |  |![Supported](./media/certificates-configure/green-check.png) |   |
| Windows 10/11  | ![Supported](./media/certificates-configure/green-check.png) <br>*(see **Note 2**)*| ![Supported](./media/certificates-configure/green-check.png) <br>*(see **Note 2**)*| ![Supported](./media/certificates-configure/green-check.png) <br>*(see **Note 2**)*| ![Supported](./media/certificates-configure/green-check.png) |

- ***Note 1*** - Beginning with Android 11, trusted certificate profiles can no longer install the trusted root certificate on devices that are enrolled as *Android device administrator*. This limitation doesn't apply to Samsung Knox. For more information, see [Trusted certificate profiles for Android device administrator](certificates-trusted-root.md#trusted-certificate-profiles-for-android-device-administrator).
- ***Note 2*** - This profile is supported for [Windows Enterprise multi-session remote desktops](../fundamentals/azure-virtual-desktop-multi-session.md).

## Next steps

More resources
- [Use S/MIME to sign and encrypt emails](certificates-s-mime-encryption-sign.md)  
- [Use third-party certification authority](certificate-authority-add-scep-overview.md)  

Create certificate profiles:  
- [Configure a trusted certificate profile](certificates-trusted-root.md)
- [Configure infrastructure to support SCEP certificates with Intune](certificates-scep-configure.md)  
- [Configure and manage PKCS certificates with Intune](certificates-pfx-configure.md)  
- [Create a PKCS imported certificate profile](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

Learn about the [Certificate Connector for Microsoft Intune](certificate-connector-install.md)
