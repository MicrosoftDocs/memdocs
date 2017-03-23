---
title: "Create PFX certificate profiles | Microsoft Docs"
description: "Learn how to use PFX files in System Center Configuration Manager to generate user-specific certificates that support encrypted data exchange."
ms.custom: na
ms.date: 03/28/2017
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
author: robstackmsft
ms.author: robstack
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
System Center Configuration Manager allows you to provision personal information exchange (.pfx) files to user devices. PFX files can be used to generate user-specific certificates to support encrypted data exchange. PFX certificates can be created within Configuration Manager or imported.

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

    -   **Specify the type of certificate profile that you want to create**: For PFX certificates, choose one of:  

        -   **Personal Information Exchange PKCS #12 (PFX) settings - Import**: Select this to import a PFX certificate.  
        -   **Personal Information Exchange PKCS #12 (PFX) settings - Create**: Select this option to create a new PFX certificate.

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

### Create a new PFX certificate

When you create and deploy a PFX certificate, the same certificate will be installed on all devices that the user enrolls.

1. On the **Supported Platforms** page of the wizard, choose the device platforms on which this certificate will be installed, then click **Next**.
2. On the **Certification Authorities** page of the wizard, confiugre the following:
	- **Primary Site** - Select the Configuration Manager primary site from which you want to select a certification authority.
	- **Certification authorities** - After you select a primary site, select the certification authority you want from the list, then click **Next**.
3. On the **PFX Certificate** page of the wizard, configure the following values:
	- **Renewal threshold (%)** - Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.
	- **Certificate template name** - Click **Browse** to select the name of a certificate template that has been added to an issuing CA. To successfully browse to certificate templates, the user account that you are using to run the Configuration Manager console must have **Read** permission to the certificate template. Alternatively, type the name of the certificate template. 
	- **Subject name format** - From the list, select how Configuration Manager automatically creates the subject name in the certificate request. If the certificate is for a user, you can also include the user's email address in the subject name. Choose from **Common name**, or **Fully distinguished name**.
	- **Subject alternative name** - Specify how Configuration Manager automatically creates the values for the subject alternative name (SAN) in the certificate request. For example, if you selected a user certificate type, you can include the user principal name (UPN) in the subject alternative name. Choose from:
		- **Email address** 
		- **User principle name (UPN)** 
	- **Certificate validity period** - 
	- **Windows Key Storage Provider** (displayed only if you selected Windows as a supported platform) - 
		- 	**Install to Trusted Platform Module (TPM) if present**  
    	-   **Install to Trusted Platform Module (TPM), otherwise fail** 
    	-   **Install to Windows Hello for Business otherwise fail** 
    	-   **Install to Software Key Storage Provider** 
4. Click **Next**.

### Finish up

1.  Click **Next**, review the **Summary** page, and then close the wizard.  
2.  The certificate profile containing the PFX file is now available from the **Certificate Profiles** workspace. 
3.  To deploy the profile, in the **Assets and Compliance** workspace open **Compliance Settings** > **Company Resource Access** > **Certificate Profiles**, right-click the certificate you want, then click **Deploy**. 



## See also
[Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) walks you through the Create Certificate Profile Wizard.

[Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) provides information about deploying certificate profiles.