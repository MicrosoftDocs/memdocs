---
title: "Create PFX certificate profiles | Microsoft Docs"
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
# How to create PFX certificate profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Certificate profiles work with Active Directory Certificate Services and the Network Device Enrollment Service role to provision authentication certificates for managed devices so that users can seamlessly access company resources. For example, you can create and deploy certificate profiles to provide the necessary certificates for users to initiate VPN and wireless connections.

[Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md) provides general information about creating and configuring certificate profiles. This topic highlights some specific information about certificate profiles related to PFX certificates.

-  Configuration Manager supports deploying certificates to different certificate stores, depending on the requirements, the device type, and  the operating system. The following devices are supported when they are enrolled with Intune:

 -   iOS  

- For other prerequisites, see [Certificate profile prerequisites](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## PFX certificate profiles
System Center Configuration Manager allows you to import, then provision personal information exchange (.pfx) files to user devices. PFX files can be used to generate user-specific certificates to support encrypted data exchange.

> [!TIP]  
>  A step-by-step walkthrough describing this process is available in [How to Create and Deploy PFX Certificate Profiles in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## Create and deploy a Personal Information Exchange (PFX) certificate profile  

### Get started

1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Certificate Profiles**.  

3.  On the **Home** tab, in the **Create** group, click **Create Certificate Profile**.

4.  On the **General** page of the **Create Certificate Profile** Wizard, specify the following information:  

    -   **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    -   **Description**: Provide a description that gives an overview of the certificate profile and other relevant information that helps to identify it in the System Center Configuration Manager console. You can use a maximum of 256 characters.  

    -   **Specify the type of certificate profile that you want to create**: For PFX certificates, choose one of the following:  

        -   **Personal Information Exchange PKCS #12 (PFX) settings - Import**: Imports a PFX certificate.  

        -   **Personal Information Exchange - PKCS #12 (PFX) settings - Create**: Creates a PFX certificate.
       

### Import a PFX certificate

To import a PFX certificate, you'll need the Configuration Manager SDK. Any certificates you import for a user will be deployed to any devices that the user enrolls.

1. On the **PFX Certificate** page of the **Create Certificate Profile Wizard**, specify where the certificate will be stored on devices to which you deploy it:
	- 	**Install to Trusted Platform Module (TPM) if present**  
    -   **Install to Trusted Platform Module (TPM), otherwise fail** 
    -   **Install to Windows Hello for Business otherwise fail** 
    -   **Install to Software Key Storage Provider** 
2. Click **Next**. 
3. On the **Supported Platforms** page of the wizard, choose the device platforms on which this certificate will be installed, then click **Next**.
4. Using the SDK for Windows 8.1 available from the Download Center ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), deploy a Create PFX Script. The Create PFX Script added in Configuration Manager 2012 SP2 adds an SMS_ClientPfxCertificate class to the SDK. This class includes the following methods:  

    -   ImportForUser  

    -   DeleteForUser  

     Sample script:  

```  
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

The following script variables must be modified for your script:  

   -   blob\ = The PFX base64-encrypted blob  
   -   $Password = The password for the PFX file  
   -   $ProfileName = The name of the PFX profile  
   -   ComputerName = Name of host computer   

### Create a PFX certificate

To create a PFX certificate:

1.  First, choose the certificate authority (CA).  Starting with version 1706, you may choose between Microsoft or Entrust as a certificate authority.

2.  Click **Next**. 

3.  On the **Supported Platforms** page, choose the device platforms on which this certificate will be installed, and then click **Next**.

4.  On the **Configure Certificate Authorities** page, choose the **Primary Site** and the **Certificate registration point**.   These must be previously defined [certificate registration points](/sccm/protect/deploy-use/introduction-to-certificate-profiles).   

### Finish up

1.  Click **Next**, review the **Summary** page, and then close the wizard.  
2.  The certificate profile containing the PFX file is now available from the **Certificate Profiles** workspace. 
3.  To deploy the profile, in the **Assets and Compliance** workspace open **Compliance Settings** > **Company Resource Access** > **Certificate Profiles**, right-click the certificate you want, then click **Deploy**. 



## See also
[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) walks you through the Create Certificate Profile Wizard.

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) provides information about deploying certificate profiles.