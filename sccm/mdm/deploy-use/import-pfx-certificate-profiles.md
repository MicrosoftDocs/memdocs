---
title: "Create PFX certificate profiles by importing certificate details"
titleSuffix: "Configuration Manager"
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
# How to create PFX certificate profiles by importing certificate details

*Applies to: System Center Configuration Manager (Current Branch)*


Here, you learn how to create a certificate profile by importing credentials from external certificates.  

[Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md) provide general information about creating and configuring certificate profiles. This topic highlights some specific information about certificate profiles related to PFX certificates.

-  Configuration Manager a variety of certificate stores appropriate for different devices and operating systems.  These include:

 -   iOS and MacOS/OSX
 -   Android and Android for Work
 -   Windows 10, including Windows 10 mobile.

To learn more, see [Certificate profile prerequisites](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## PFX certificate profiles
System Center Configuration Manager allows you to import certificate credentials and then provision personal information exchange (.pfx) files to user devices. PFX files can be used to generate user-specific certificates to support encrypted data exchange.

> [!TIP]  
>  A step-by-step walkthrough describing this process is available in [How to Create and Deploy PFX Certificate Profiles in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## Create, import, and deploy a Personal Information Exchange (PFX) certificate profile  

### Get started

1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Certificate Profiles**.  

3.  On the **Home** tab, in the **Create** group, click **Create Certificate Profile**.

4.  On the **General** page of the **Create Certificate Profile** Wizard, specify the following information:  

    -   **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    -   **Description**: Provide a description that gives an overview of the certificate profile and other relevant information that helps to identify it in the System Center Configuration Manager console. You can use a maximum of 256 characters.  

    -   **Specify the type of certificate profile that you want to create**: For PFX certificates, choose one of the following options:  

        -   **Personal Information Exchange PKCS #12 (PFX) settings - Import**: Creates a certificate profile by programmatically importing information from existing certificates.  

        -   **Personal Information Exchange - PKCS #12 (PFX) settings - Create**: Creates a PFX certificate profile using credentials provided by a certificate authority.  To learn more, see [How to create PFX certificate profiles using a certificate authority](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### Create a PFX certificate profile for the imported credentials

To import a PFX certificate, you use the Configuration Manager SDK to deploy a Create PFX script. 

Imported certificates are later deployed to enrolled devices.

1. On the **PFX Certificate** page of the **Create Certificate Profile Wizard**, specify where the device key storage provider:
	- 	**Install to Trusted Platform Module (TPM) if present**  
    -   **Install to Trusted Platform Module (TPM), otherwise fail** 
    -   **Install to Windows Hello for Business otherwise fail** 
    -   **Install to Software Key Storage Provider** 
2. Click **Next**. 
3. On the **Supported Platforms** page of the wizard, choose the supported device platforms and then click **Next**.

### Finish the profile

1.  Click **Next**, review the **Summary** page, and then close the wizard.  
2.  The certificate profile containing the PFX file is now available from the **Certificate Profiles** workspace. 
3.  To deploy the profile, in the **Assets and Compliance** workspace open **Compliance Settings** > **Company Resource Access** > **Certificate Profiles**, right-click the certificate you want, then click **Deploy**. 

### Deploy a Create PFX Script

Use the [Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525) to deploy a Create PFX Script. 

The Create PFX Script added in Configuration Manager 2012 SP2 adds an SMS_ClientPfxCertificate class to the SDK. This class includes the following methods:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

The following example imports credentials into a PFX certificate profile.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

To use this example, update the following script variables:  

   -   **blob**\ - The PFX base64-encrypted blob  
   -   **$Password** - The password for the PFX file  
   -   **$ProfileName** - The name of the PFX profile  
   -   **ComputerName** - Name of host computer   

## See also
[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md) walks you through the Create Certificate Profile Wizard.

[How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) describes show to deploy certificate profiles.