---
# required metadata

title: Sign and encrypt email using S/MIME - Microsoft Intune - Azure | Microsoft Docs
description: Learn how to use email digital certificates in Microsoft Intune to sign and encrypt emails on devices. These certificates are called S/MIME and are configured using device configuration profiles. Signing and encryption certificates use PKCS, or private certificates, and use a connector to import certificates.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# S/MIME overview to sign and encrypt email in Intune

Email certificates, also known as S/MIME certificate, provide extra security to your email communications by using encryption and decryption. Microsoft Intune can use S/MIME certificates to sign and encrypt emails to mobile devices running the following platforms:

- Android
- iOS/iPadOS
- macOS
- Windows 10 and later
- Windows Phone

On iOS/iPadOS devices, you can create an Intune-managed email profile that uses S/MIME and certificates to sign and encrypt incoming and outgoing emails. For other platforms, S/MIME may or may not be supported. If it's supported, install certificates that use S/MIME signing and encryption. Then, an end user enables S/MIME in their email application.

For more information about S/MIME email signing and encryption with Exchange, see [S/MIME for message signing and encryption](https://docs.microsoft.com/Exchange/policy-and-compliance/smime).

This article provides an overview of using S/MIME certificates to sign and encrypt emails on your devices.

## Signing certificates

Certificates used for signing allow the client email app to communicate securely with the email server.

To use signing certificates, create a template on your certificate authority (CA) that focuses on signing. On Microsoft Active Directory Certification Authority, [Configure the server certificate template](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/server-certs/configure-the-server-certificate-template) lists the steps to create certificate templates.

Signing certificates in Intune use PKCS certificates. [Configure and use PKCS certificates](certficates-pfx-configure.md) describes how to deploy and use PKCS certificate in your Intune environment. These steps include:

- Download and install the Microsoft Intune Certificate Connector to support PKCS certificate requests. The connector has the same network requirements as [managed devices](../fundamentals/intune-endpoints.md#access-for-managed-devices).
- Create a trusted root certificate profile for your devices. This step includes using trusted root and intermediate certificates for your certification authority, and then deploying the profile to devices.
- Create a PKCS certificate profile using the certificate template you created. This profile issues signing certificates to devices, and deploys the PKCS certificate profile to devices.

You can also import a signing certificate for a specific user. The signing certificate is deployed across any device that a user enrolls. To import certificates into Intune, use the [PowerShell cmdlets in GitHub](https://github.com/Microsoft/Intune-Resource-Access). To deploy a PKCS certificate imported in  Intune to be used for email signing, follow the steps in [Configure and use PKCS certificates with Intune](certficates-pfx-configure.md). These steps include:

- Download and install the PFX Certificate Connector for Microsoft Intune. This connector delivers imported PKCS certificates to devices.
- Import S/MIME email signing certificates to Intune.
- Create a PKCS imported certificate profile. This profile delivers imported PKCS certificates to the appropriate user's devices.

## Encryption certificates

Certificates used for encryption confirm that an encrypted email can only be decrypted by the intended recipient. S/MIME encryption is an extra layer of security that can be used in email communications.

When sending an encrypted email to another user, the public key of that user's encryption certificate is obtained, and encrypts the email you send. The recipient decrypts the email using the private key on their device. Users can have a history of certificates used to encrypt email. Each of those certificates must be deployed to all of a specific user's devices so their email is successfully decrypted.

It's recommended that email encryption certificates aren't created in Intune. While Intune supports issuing PKCS certificates that support encryption, Intune creates a unique certificate per device. A unique certificate per device isn't ideal for an S/MIME encryption scenario where the encryption certificate should be shared across all the user's devices.

To deploy S/MIME certificates using Intune, you must import all of a user's encryption certificates to Intune. Intune then deploys all of those certificates to each device that a user enrolls. To import certificates into Intune, use the [PowerShell cmdlets in GitHub](https://github.com/Microsoft/Intune-Resource-Access).

To deploy a PKCS certificate imported in Intune used for email encryption, follow the steps in [Configure and use PKCS certificates with Intune](certficates-pfx-configure.md). These steps include:

- Download and install the PFX Certificate Connector for Microsoft Intune. This connector delivers imported PKCS certificates to devices.
- Import S/MIME email encryption certificates to Intune.
- Create a PKCS imported certificate profile. This profile delivers imported PKCS certificates to the appropriate user's devices.

 > [!NOTE]
 > Imported S/MIME encryption certificates are removed by Intune when company data is removed, or when users are unenrolled from management. But, certificates aren't revoked on the certification authority.

## S/MIME email profiles

Once you have created S/MIME signing and encryption certificate profiles, you can [enable S/MIME for iOS/iPadOS native mail](../configuration/email-settings-ios.md).

## Next steps

- [Use SCEP for certificates](certificates-scep-configure.md)
- [Use PKCS certificates](certficates-pfx-configure.md)
- [Use a partner CA](certificate-authority-add-scep-overview.md)
- [Issue PKCS certificates from a Symantec PKI manager web service](certificates-digicert-configure.md)
