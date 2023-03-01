---
title: Create PFX certificate profiles
titleSuffix: Configuration Manager
description: Learn how to use PFX files in Configuration Manager to generate user-specific certificates that support encrypted data exchange.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create PFX certificate profiles using a certificate authority

*Applies to: Configuration Manager (current branch)*

Learn how to create a certificate profile that uses a certification authority for credentials. This article highlights specific information about personal information exchange (PFX) certificate profiles. For more information about how to create and configure these profiles, see [Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager allows you to create a PFX certificate profile using credentials issued by a certificate authority. You can choose Microsoft or Entrust as your certificate authority. When deployed to user devices, PFX files generate user-specific certificates to support encrypted data exchange.

To import certificate credentials from existing certificate files, see [Import PFX certificate profiles](import-pfx-certificate-profiles.md).

## Prerequisites

Before you start creating a certificate profile, make sure the necessary prerequisites are ready. For more information, see [Prerequisites for certificate profiles](../../protect/plan-design/prerequisites-for-certificate-profiles.md). For example, for PFX certificate profiles, you need a [certificate registration point](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) site system role.

## Create a profile  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then select **Certificate Profiles**.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Certificate Profile**.

1. On the **General** page of the **Create Certificate Profile Wizard**, specify the following information:  

    - **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    - **Description**: Provide a description that gives an overview of the certificate profile that helps to identify it in the Configuration Manager console. You can use a maximum of 256 characters.  

1. Select **Personal Information Exchange - PKCS #12 (PFX) settings - Create**. This option requests a certificate on behalf of a user from a connected on-premises certificate authority (CA). Choose your certificate authority: **Microsoft** or **Entrust**.

    > [!NOTE]
    > The **Import** option gets information from an existing certificate to create a certificate profile. For more information, see [Import PFX certificate profiles](import-pfx-certificate-profiles.md).

1. On the **Supported Platforms** page, select the OS versions that this certificate profile supports. For more information on supported OS versions for your version of Configuration Manager, see [Supported OS versions for clients and devices](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. On the **Certificate Authorities** page, choose the certificate registration point (CRP) to process the PFX certificates:

    1. **Primary Site**: Choose the server containing the CRP role for the CA.
    1. **Certification authorities**: Select the relevant CA.

    For more information, see [Certificate infrastructure](../../protect/deploy-use/certificate-infrastructure.md).

The settings on the **PFX Certificate** page vary depending on the selected CA on the **General** page:

- [Microsoft CA](#bkmk_microsoft)
- [Entrust CA](#bkmk_entrust)

### <a name="bkmk_microsoft"></a> Configure **PFX Certificate** settings for Microsoft CA

1. For the **Certificate template name**, choose the certificate template.

1. To use the certificate profile for S/MIME signing or encryption, enable **Certificate usage**.

    When you enable this option, it delivers all PFX certificates associated with the target user to all of their devices. If you don't enable this option, each device receives a unique certificate.  

1. Set **Subject name format** to either **Common name** or **Fully-distinguished name**. If you're unsure which one to use, contact your CA administrator.

1. For the **Subject alternative name**, enable **Email address** and **User principle name (UPN)** as appropriate for your CA.

1. **Renewal threshold**: Determines when certificates are automatically renewed, based on the percentage of time remaining before expiration.

1. Set the **Certificate validity period** to the lifetime of the certificate.

1. When the certificate registration point specifies Active Directory credentials, enable **Active Directory publishing**.

1. If you selected one or more Windows 10 supported platforms:

    1. Set the **Windows certificate store** to **User**. (The **Local Computer** option doesn't deploy certificates, don't choose it.)

    1. Select one of the following **Key Storage Provider (KSP)**:

        - **Install to Trusted Platform Module (TPM) if present**  
        - **Install to Trusted Platform Module (TPM) otherwise fail**
        - **Install to Windows Hello for Business otherwise fail**
        - **Install to Software Key Storage Provider**

1. Complete the wizard.

### <a name="bkmk_entrust"></a> Configure **PFX Certificate** settings for Entrust CA

1. For the **Digital ID Configuration**, choose the configuration profile. The Entrust administrator creates the digital ID configuration options.

1. To use the certificate profile for S/MIME signing or encryption, enable **Certificate usage**.

    When you enable this option, it delivers all PFX certificates associated with the target user to all of their devices. If you don't enable this option, each device receives a unique certificate.  

1. To map Entrust **Subject name format** tokens to Configuration Manager fields, select **Format**.

    The **Certificate Name Formatting** dialog lists the Entrust Digital ID configuration variables. For each Entrust variable, choose the appropriate Configuration Manager fields.

1. To map Entrust **Subject Alternative Name** tokens to supported LDAP variables, select **Format**.

    The **Certificate Name Formatting** dialog lists the Entrust Digital ID configuration variables. For each Entrust variable, choose the appropriate LDAP variable.

1. **Renewal threshold**: Determines when certificates are automatically renewed, based on the percentage of time remaining before expiration.

1. Set the **Certificate validity period** to the lifetime of the certificate.

1. When the certificate registration point specifies Active Directory credentials, enable **Active Directory publishing**.

1. If you selected one or more Windows 10 supported platforms:

    1. Set the **Windows certificate store** to **User**. (The **Local Computer** option doesn't deploy certificates, don't choose it.)

    1. Select one of the following **Key Storage Provider (KSP)**:

        - **Install to Trusted Platform Module (TPM) if present**  
        - **Install to Trusted Platform Module (TPM) otherwise fail**
        - **Install to Windows Hello for Business otherwise fail**
        - **Install to Software Key Storage Provider**

1. Complete the wizard.

## Deploy the profile

After you create a certificate profile, it's now available in the **Certificate Profiles** node. For more information on how to deploy it, see [Deploy resource access profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## See also

[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md)

[Import PFX certificate profiles](import-pfx-certificate-profiles.md)

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
