---
title: Import PFX certificate profiles
titleSuffix: Configuration Manager
description: Learn how to import PFX files in Configuration Manager to generate user-specific certificates that support encrypted data exchange.
ms.date: 11/29/2019
ms.service: configuration-manager
ms.subservice: protect
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Import PFX certificate profiles

*Applies to: Configuration Manager (current branch)*

Learn how to create a certificate profile by importing credentials from external certificates. This article highlights specific information about personal information exchange (PFX) certificate profiles. For more information about how to create and configure these profiles, see [Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager supports different kinds of certificate stores for different devices and OS versions. For example, Windows 10 and Windows 10 Mobile. For more information, see [Certificate profile prerequisites](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Use Configuration Manager to import certificate credentials and then provision PFX files to devices. You can use these files to generate user-specific certificates to support encrypted data exchange.

> [!TIP]  
> For a step-by-step walk-through of this process, see the blog post [How to Create and Deploy PFX Certificate Profiles in Configuration Manager](/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager).  

## Create a profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then select **Certificate Profiles**.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Certificate Profile**.

1. On the **General** page of the **Create Certificate Profile Wizard**, specify the following information:  

    - **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    - **Description**: Provide a description that gives an overview of the certificate profile that helps to identify it in the Configuration Manager console. You can use a maximum of 256 characters.  

1. Select **Personal Information Exchange - PKCS #12 (PFX) settings - Import**. This option imports information from an existing certificate to create a certificate profile.

    > [!NOTE]
    > The **Create** option requests a certificate on behalf of a user from a connected on-premises certificate authority (CA). This process then securely delivers the certificate to clients as PFX files. For more information, see [Create PFX certificate profiles using a certificate authority](create-pfx-certificate-profiles.md).

1. On the **PFX Certificate** page of the **Create Certificate Profile Wizard**, specify the device key storage provider (KSP):

    - **Install to Trusted Platform Module (TPM) if present**  
    - **Install to Trusted Platform Module (TPM) otherwise fail**
    - **Install to Windows Hello for Business otherwise fail**
    - **Install to Software Key Storage Provider**

1. On the **Supported Platforms** page, choose the supported device platforms.

1. Complete the wizard.

## Deploy the profile

After you create and provision a certificate profile, it's now available in the **Certificate Profiles** node. For more information on how to deploy it, see [Deploy resource access profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## Assign primary users

Assign the target users as primary users on the Windows 10 devices where you need to install the PFX certificates. For more information, see [user device affinity](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## Provision a create PFX script

To import a PFX certificate, use the following Configuration Manager PowerShell cmdlets to provision a Create PFX script:

- [Get-CMClientCertificatePfx](/powershell/module/configurationmanager/get-cmclientcertificatepfx)
- [Import-CMClientCertificatePfx](/powershell/module/configurationmanager/import-cmclientcertificatepfx)
- [Remove-CMClientCertificatePfx](/powershell/module/configurationmanager/remove-cmclientcertificatepfx)

### Example script

To provision a PFX file to a certificate profile for a user, open PowerShell on a computer with the Configuration Manager console. Change the variables with values from your environment.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## See also

[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md)

[Create PFX certificate profiles using a certificate authority](create-pfx-certificate-profiles.md)

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)