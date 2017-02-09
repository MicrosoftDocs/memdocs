---
title: "Create PFX certificate profiles | Microsoft Docs"
description: "Learn how to use PFX files in System Center Configuration Manager to generate user-specific certificates that support encrypted data exchange."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# How to create PFX certificate profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager allows you to provision personal information exchange (.pfx) files to user devices. PFX files can be used to generate user-specific certificates to support encrypted data exchange. PFX certificates can be created within Configuration Manager or imported. With System Center Configuration Manager, imported or new PFX certificates can be deployed to iOS, Android, and Windows 10 devices. These files can then be deployed to multiple devices to support user-based PKI communication.  

> [!TIP]  
>  A step-by-step walkthrough describing this process is available in [How to Create and Deploy PFX Certificate Profiles in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## Create and Deploy Personal Information Exchange (PFX) Certificate Profiles  

#### How to create and deploy a Personal Information Exchange (PFX) certificate profile  

1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Certificate Profiles**.  

3.  On the **Home** tab, in the **Create** group, click **Create Certificate Profile**. The **Create Certificate Profile** wizard opens.  

4.  On the **General** page of the **Create Certificate Profile** Wizard, specify the following information:  

    -   **Name**: Enter a unique name for the certificate profile. You can use a maximum of 256 characters.  

    -   **Description**: Provide a description that gives an overview of the certificate profile and other relevant information that helps to identify it in the System Center Configuration Manager console. You can use a maximum of 256 characters.  

    -   **Specify the type of certificate profile that you want to create**: Choose one of the following certificate profile types:  

        -   **Trusted CA certificate**: Select this certificate profile type if you want to deploy a trusted root certification authority (CA) or intermediate CA certificate to form a certificate chain of trust when the user or device must authenticate another device. For example, the device might be a Remote Authentication Dial-In User Service (RADIUS) server or a virtual private network (VPN) server. You must also configure a trusted CA certificate profile before you can create a SCEP certificate profile. In this case, the trusted CA certificate must be the trusted root certificate for the CA that will issue the certificate to the user or device.  

        -   **Simple Certificate Enrollment Protocol (SCEP) settings**: Select this certificate profile type if you want to request a certificate for a user or device, by using the Simple Certificate Enrollment Protocol and the Network Device Enrollment Service role service.  

        -   **Personal Information Exchange PKCS #12 (PFX) settings import**: Select this to import a PFX certificate.  

5.  In the **Certificate Properties** window of the **Create Certificate Profile** wizard, specify where the PFX certificate will be stored on targeted devices.  

    -   **Install to Trusted Platform Module (TPM) if present**  

    -   **Install to Trusted Platform Module (TPM), otherwise fail**  

    -   **Install to Software Key Storage Provider**  

     Click **Next**.  

6.  In the **Supported Platforms** window of the **Create Certificate Profile** wizard, specify which operating systems or platforms that can receive the imported PFX file.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Click **Next**, review the **Summary** page, and then close the wizard.  

8.  The certificate profile containing the PFX file is now available from the **Certificate Profiles** workspace. In the **Assets and Compliance** workspace go **Compliance Settings** > **Company Resource Access** > **Certificate Profiles** and right-click to deploy the new certificate to User collections.  

9. Using the SDK for Windows 8.1 available from the Download Center ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), deploy a Create PFX Script. The Create PFX Script added in Configuration Manager 2012 SP2 adds an SMS_ClientPfxCertificate class to the SDK. This class includes the following methods:  

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

    -   <blob\> = The PFX base64-encrypted blob  

    -   $Password = The password for the PFX file  

    -   $ProfileName = The name of the PFX profile  

    -   ComputerName = Name of host computer  
