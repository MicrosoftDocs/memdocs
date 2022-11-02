---
title: Create SCEP certificate profiles
titleSuffix: Configuration Manager
description: Learn how to use certificate profiles to provision managed devices with the certificates they need
ms.date: 03/29/2022
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create certificate profiles

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in version 2203, this company resource access feature is no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](../plan-design/resource-access-deprecation-faq.yml).

Use certificate profiles in Configuration Manager to provision managed devices with the certificates they need to access company resources. Before creating certificate profiles, set up the certificate infrastructure as described in [Set up certificate infrastructure](certificate-infrastructure.md).  

This article describes how to create trusted root and Simple Certificate Enrollment Protocol (SCEP) certificate profiles. If you want to create PFX certificate profiles, see [Create PFX certificate profiles](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

To create a certificate profile:

1. Start the Create Certificate Profile Wizard.
1. Provide general information about the certificate.
1. Configure a trusted certificate authority (CA) certificate.  
1. Configure SCEP certificate information.  
1. Specify supported platforms for the certificate profile.

## Start the wizard  

To start the Create Certificate Profile:

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then select the **Certificate Profiles** node.  

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Certificate Profile**.  

## General

On the **General** page of the Create Certificate Profile Wizard, specify the following information:  

- **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

- **Description**: Provide a description that gives an overview of the certificate profile. Also include other relevant information that helps to identify it in the Configuration Manager console. You can use a maximum of 256 characters.  

- Specify the type of certificate profile that you want to create:

  - **Trusted CA certificate**: Select this type to deploy a trusted root certification authority (CA) or intermediate CA certificate to form a certificate chain of trust when the user or device must authenticate another device. For example, the device might be a Remote Authentication Dial-In User Service (RADIUS) server or a virtual private network (VPN) server.
  
    Also configure a trusted CA certificate profile before you can create a SCEP certificate profile. In this case, the trusted CA certificate must be for the CA that issues the certificate to the user or device.  

  - **Simple Certificate Enrollment Protocol (SCEP) settings**: Select this type to request a certificate for a user or device with the Simple Certificate Enrollment Protocol and the Network Device Enrollment Service (NDES) role service.

  - **Personal Information Exchange PKCS #12 (PFX) settings - Import**: Select this option to import a PFX certificate. For more information, see [Import PFX certificate profiles](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Personal Information Exchange PKCS #12 (PFX) settings - Create**: Select this option to process PFX certificates using a certificate authority. For more information, see [Create PFX certificate profiles](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## Trusted CA certificate  

> [!IMPORTANT]  
> Before you create a SCEP certificate profile, configure at least one trusted CA certificate profile.
>
> After the certificate is deployed, if you change any of these values, a new certificate is requested:
>
> - Key Storage Provider
> - Certificate template name
> - Certificate type
> - Subject name format
> - Subject alternative name
> - Certificate validity period
> - Key usage
> - Key size
> - Extended key usage
> - Root CA certificate

1. On the **Trusted CA Certificate** page of the Create Certificate Profile Wizard, specify the following information:  

    - **Certificate file**: Select **Import**, and then browse to the certificate file.  

    - **Destination store**: For devices that have more than one certificate store, select where to store the certificate. For devices that have only one store, this setting is ignored.  

2. Use the **Certificate thumbprint** value to verify that you've imported the correct certificate.  

## SCEP certificates

### 1. SCEP Servers

On the **SCEP Servers** page of the Create Certificate Profile Wizard, specify the URLs for the NDES Servers that will issue certificates via SCEP. You can automatically assign an NDES URL based on the configuration of the certificate registration point, or add URLs manually.  

### 2. SCEP Enrollment

Complete the **SCEP Enrollment** page of the Create Certificate Profile Wizard.

- **Retries**: Specify the number of times that the device automatically retries the certificate request to the NDES server. This setting supports the scenario where a CA manager must approve a certificate request before it's accepted. This setting is typically used for high-security environments or if you have a stand-alone issuing CA rather than an enterprise CA. You might also use this setting for testing purposes so that you can inspect the certificate request options before the issuing CA processes the certificate request. Use this setting with the **Retry delay (minutes)** setting.  

- **Retry delay (minutes)**: Specify the interval, in minutes, between each enrollment attempt when you use CA manager approval before the issuing CA processes the certificate request. If you use manager approval for testing purposes, specify a low value. Then you're not waiting a long time for the device to retry the certificate request after you approve the request.

    If you use manager approval on a production network, specify a higher value. This behavior allows sufficient time for the CA administrator to approve or deny pending approvals.  

- **Renewal threshold (%)**: Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.  

- **Key Storage Provider (KSP)**: Specify where the key to the certificate is stored. Choose from one of the following values:  

  - **Install to Trusted Platform Module (TPM) if present**: Installs the key to the TPM. If the TPM isn't present, the key is installed to the storage provider for the software key.  

  - **Install to Trusted Platform Module (TPM) otherwise fail**: Installs the key to the TPM. If the TPM module isn't present, the installation fails.  

  - **Install to Windows Hello for Business otherwise fail**: This option is available for Windows 10 or later devices. It allows you to store the certificate in the Windows Hello for Business store, which is protected by multi-factor authentication. For more information, see [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > This option doesn't support Smart card logon for the Enhanced key usage on the Certificate Properties page.

  - **Install to Software Key Storage Provider**: Installs the key to the storage provider for the software key.  

- **Devices for certificate enrollment**: If you deploy the certificate profile to a user collection, allow certificate enrollment only on the user's primary device, or on any device to which the user signs in.

    If you deploy the certificate profile to a device collection, allow certificate enrollment for only the primary user of the device, or for all users that sign in to the device.  

### 3. Certificate Properties

On the **Certificate Properties** page of the Create Certificate Profile Wizard, specify the following information:  

- **Certificate template name**: Select the name of a certificate template that you configured in NDES and added to an issuing CA. To successfully browse to certificate templates, your user account needs **Read** permission to the certificate template. If you can't **Browse** for the certificate, type its name.  

  > [!IMPORTANT]
  > If the certificate template name contains non-ASCII characters, the certificate isn't deployed. (One example of these characters is from the Chinese alphabet.) To make sure that the certificate is deployed, first create a copy of the certificate template on the CA. Then rename the copy by using ASCII characters.  

  - If you *browse* to select the name of the certificate template, some fields on the page automatically populate from the certificate template. In some cases, you can't change these values unless you choose a different certificate template.  

  - If you *type* the name of the certificate template, make sure that the name exactly matches one of the certificate templates. It must match the names that are listed in the registry of the NDES server. Make sure that you specify the name of the certificate template, and not the display name of the certificate template.  

    To find the names of certificate templates, browse to the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP`. It lists the certificate templates as the values for **EncryptionTemplate**, **GeneralPurposeTemplate**, and **SignatureTemplate**. By default, the value for all three certificate templates is **IPSECIntermediateOffline**, which maps to the template display name of **IPSec (Offline request)**.  

    > [!WARNING]  
    > When you type the name of the certificate template, Configuration Manager can't verify the contents of the certificate template. You may be able to select options that the certificate template doesn't support, which may result in a failed certificate request. When this behavior happens, you'll see an error message for w3wp.exe in the CPR.log file that the template name in the certificate signing request (CSR) and the challenge don't match.  
    >
    > When you type the name of the certificate template that's specified for the **GeneralPurposeTemplate** value, select the **Key encipherment** and the **Digital signature** options for this certificate profile. If you want to enable only the **Key encipherment** option in this certificate profile, specify the certificate template name for the **EncryptionTemplate** key. Similarly, if you want to enable only the **Digital signature** option in this certificate profile, specify the certificate template name for the **SignatureTemplate** key.  

- **Certificate type**: Select whether you'll deploy the certificate to a device or a user.  

- **Subject name format**: Select how Configuration Manager automatically creates the subject name in the certificate request. If the certificate is for a user, you can also include the user's email address in the subject name.

    > [!NOTE]  
    > If you select **IMEI number** or **Serial number**, you can differentiate between different devices that are owned by the same user. For example, those devices could share a common name, but not an IMEI number or serial number. If the device doesn't report an IMEI or serial number, the certificate is issued with the common name.

- **Subject alternative name**: Specify how Configuration Manager automatically creates the values for the subject alternative name (SAN) in the certificate request. For example, if you selected a user certificate type, you can include the user principal name (UPN) in the subject alternative name. If the client certificate will authenticate to a Network Policy Server, set the subject alternative name to the UPN.  

- **Certificate validity period**: If you set a custom validity period on the issuing CA, specify the amount of remaining time before the certificate expires.

    > [!TIP]
    > Set a custom validity period with the following command line:
    > `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > For more information about this command, see [Certificate infrastructure](certificate-infrastructure.md).  

    You can specify a value that's lower than the validity period in the specified certificate template, but not higher. For example, if the certificate validity period in the certificate template is two years, you can specify a value of one year, but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA's certificate.  

- **Key usage**: Specify key usage options for the certificate. Choose from the following options:  

  - **Key encipherment**: Allow key exchange only when the key is encrypted.  

  - **Digital signature**: Allow key exchange only when a digital signature helps protect the key.  

  If you browsed for a certificate template, you can't change these settings, unless you select a different certificate template.  

  Configure the selected certificate template with one or both of the two key usage options above. If not, you'll see the following message in the certificate registration point log file, **Crp.log**: **Key usage in CSR and challenge do not match**  

- **Key size (bits)**: Select the size of the key in bits.  

- **Extended key usage**: Add values for the certificate's intended purpose. In most cases, the certificate requires **Client Authentication** so that the user or device can authenticate to a server. You can add any other key usages as required.  

- **Hash algorithm**: Select one of the available hash algorithm types to use with this certificate. Select the strongest level of security that the connecting devices support.  

  > [!NOTE]  
  > **SHA-2** supports SHA-256, SHA-384, and SHA-512. **SHA-3** supports only SHA-3.  

- **Root CA certificate**: Choose a root CA certificate profile that you previously configured and deployed to the user or device. This CA certificate must be the root certificate for the CA that will issue the certificate that you're configuring in this certificate profile.  

  > [!IMPORTANT]  
  > If you specify a root CA certificate that's not deployed to the user or device, Configuration Manager won't initiate the certificate request that you're configuring in this certificate profile.  

## Supported platforms  

On the **Supported Platforms** page of the Create Certificate Profile Wizard, select the OS versions where you want to install the certificate profile. Choose **Select all** to install the certificate profile to all available operating systems.

## Next steps

The new certificate profile appears in the **Certificate Profiles** node in the **Assets and Compliance** workspace. It's ready for you to deploy to users or devices. For more information, see [How to deploy profiles](deploy-wifi-vpn-email-cert-profiles.md).