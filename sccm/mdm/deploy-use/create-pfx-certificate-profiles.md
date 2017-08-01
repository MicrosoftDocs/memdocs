---
title: "Create PFX certificate profiles using a certificate authority | Microsoft Docs"
description: "Learn how to use PFX files in System Center Configuration Manager to generate user-specific certificates that support encrypted data exchange."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe

---
# How to create PFX certificate profiles using a certificate authority

*Applies to: System Center Configuration Manager (Current Branch)*

Here, you learn how to create a certificate profile that uses a certification authority for credentials.

[Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md) provides general information about creating and configuring certificate profiles. This topic highlights some specific information about certificate profiles related to PFX certificates.

## PFX certificate profiles
System Center Configuration Manager allows you to create a PFX certificate profile using credentials issued by a certificate authority.  As of version 1706, you may choose Microsoft or Entrust as your certificate authority.  When deployed to user devices, personal information exchange (.pfx) files generate user-specific certificates to support encrypted data exchange.

To import certificate credentials from existing certificate files, see [How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## Create and deploy a Personal Information Exchange (PFX) certificate profile  

### Get started

1.  In the System Center Configuration Manager console, choose **Assets and Compliance**.  
2.  In the **Assets and Compliance** workspace, choose **Compliance Settings** &gt; **Company Resource Access** &gt; **Certificate Profiles**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Certificate Profile**.

4.  On the **General** page of the **Create Certificate Profile** Wizard, specify the following information:  

    -   **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    -   **Description**: Provide a description that gives an overview of the certificate profile and other relevant information that helps to identify it in the System Center Configuration Manager console. You can use a maximum of 256 characters.  

    -   In **Specify the type of certificate profile that you want to create**, choose **Personal Information Exchange - PKCS #12 (PFX) settings - Create** and then choose your certificate authority from the drop-down list.  Beginning with version 1706, you may choose **Microsoft** or **Entrust**.

### Select supported platforms

The Supported Platforms page identifies the operating systems and devices the certificate profile supports.  

Certificate profiles may support multiple operating systems and devices, however, certain operating system or device combinations may require different settings.  In these cases, it's best to create separate profiles for each unique set of settings.  

As of version 1706, the following options are available:

- Windows 10
    - All Windows 10 (64-bit)
    - All Windows 10 (32-bit)
    - All Windows 10 Holographic Enterprise and higher
    - All Windows 10 Holographic and higher
    - All Windows 10 Team and higher
    - All Windows 10 Mobile and higher
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> MacOS/OSX devices are not currently supported.  

When no other options are selected, the **Select All** checkbox selects all available options.  When one or more options are selected, **Select All** clears existing selections. 

1.  Select one or more platforms supported by the certificate profile.

1.  Choose **Next** to continue.  


### Configure certification authorities

Here, you choose the certificate registration point (CRP) to process the PFX certificates.  

1.  From the **Primary Site** list, choose the server containing the CRP role for the CA.
1.  From the list of **Certification authorities**, choose the relevant CA by placing a checkmark in the left column.
1.  When ready to continue, choose **Next**.

To learn more, see [Certificate infrastructure](../../protect/deploy-use/certificate-infrastructure.md).


### Configure certificate settings for Microsoft CA

To configure certificate settings when using Microsoft as the CA:

1.  From the **Certificate template name** drop-down, choose the certificate template.

1.  Enable the **Certificate usage** checkbox to use the certificate profile for S/MIME signing or encryption.

    When you check this option while using Microsoft as the CA, all PFX certificates associated with the target user are delivered to all devices enrolled by the user.  When this checkbox is unchecked, each device receives a unique certificate.  

1.  Set **Subject name format** to either **Common name** or **Fully-distinguished name**.  If unsure which to use, contact your certificate authority administrator.

1.  For **Subject alternative name**, enable the **Email address** and **User principle name (UPN)** as appropriate for your CA.

1.  **Renewal threshold** determines when certificates are automatically renewed, based on the percentage of time remaining before expiration.

1.  Set the **Certificate validity period** to the lifetime of the certificate.  The period is specified by setting a number (1-100) and period (years, months, or days).

1.  The **Active Directory publishing** is enabled when the certificate registration point specifies Active Directory credentials.  Enable the option to publish the certificate profile to Active Directory.

1.  If you selected one or more Windows 10 platforms when specifying supported platforms:

    1.  Set **Windows certificate store** to **User**.  (The **Local Computer** option does not support certificate authorities.)
    1.  Select the **Key Storage Provider (KSP)** from one of the following options:

        - **Install to Trusted Platform Module (TPM) if present**  
        - **Install to Trusted Platform Module (TPM), otherwise fail** 
        - **Install to Windows Hello for Business otherwise fail** 
        - **Install to Software Key Storage Provider** 

1.  When finished, choose **Next** or **Summary**.

### Configure certificate settings for Entrust CA

To configure certificate settings when using Entrust as the CA:

1.  From the **Digital ID Configuration** drop-down, choose the configuration profile.  The digital ID configuration options are created by the Entrust administrator.

1.  When checked, the **Certificate usage** uses the certificate profile for S/MIME signing or encryption.

    When using Entrust as the CA, all PFX certificates associated with the target user are delivered to all devices enrolled by the user.    When this option is *not* checked, each device receives a unique certificate.  (Behavior changes for different CAs; to learn more, see the corresponding section.)

1.  Use the **Format** button to map Entrust **Subject name format** tokens to ConfigMgr fields.  

    The **Certificate Name Formatting** dialog lists the Entrust Digital ID configuration variables.  For each Entrust variable, choose the appropriate LDAP variable from the associated drop-down list.

1.  Use the **Format** button to map Entrust **Subject Alternative Name** tokens to supported LDAP variables.  

    The **Certificate Name Formatting** dialog lists the Entrust Digital ID configuration variables.  For each Entrust variable, choose the appropriate LDAP variable from the associated drop-down list.

1.  **Renewal threshold** determines when certificates are automatically renewed, based on the percentage of time remaining before expiration.

1.  Set the **Certificate validity period** to the lifetime of the certificate.  The period is specified by setting a number (1-100) and period (years, months, or days).

1.  The **Active Directory publishing** is enabled when the certificate registration point specifies Active Directory credentials.  Enable the option to publish the certificate profile to Active Directory.

1.  If you selected one or more Windows 10 platforms when specifying supported platforms:

    1.  Set **Windows certificate store** to **User**.  (The **Local Computer** choice does not support certificate authorities.)
    1.  Select the **Key Storage Provider (KSP)** from one of the following options:

        - **Install to Trusted Platform Module (TPM) if present**  
        - **Install to Trusted Platform Module (TPM), otherwise fail** 
        - **Install to Windows Hello for Business otherwise fail** 
        - **Install to Software Key Storage Provider** 

1.  When finished, choose **Next** or **Summary**.


### Finish up

1.  From the Summary page, review your selections and verify your choices.

1.  When ready, choose **Next** to create the profile.  

1.  The certificate profile containing the PFX file is now available from the **Certificate Profiles** workspace. 

1.  To deploy the profile:

    1. Open the **Assets and Compliance** workspace.
    1. Choose **Compliance Settings** > **Company Resource Access** > **Certificate Profiles**
    1. Right-click the desired certificate profile and then choose **Deploy**. 


## See also
[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) walks you through the Create Certificate Profile Wizard.

[How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) describes how to deploy certificate profiles.