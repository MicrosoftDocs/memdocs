---

title: "Bulk-enroll devices for On-premises MDM"
titleSuffix: "Configuration Manager"
description: "Bulk-enroll devices in an automated way with On-premises Mobile Device Management in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: 13
caps.handback.revision: 0
author: dougeby
ms.author: dougeby
manager: angrobe

---
# How to bulk-enroll devices with On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Bulk enrollment in System Center Configuration Manager On-premises Mobile Device Management is a more automated means for  enrolling devices, as compared to user enrollment, which requires users to enter their credentials to enroll the device.  Bulk enrollment uses an enrollment package to authenticate the device during enrollment. The package (a .ppkg file) contains a certificate profile and optionally a Wi-Fi profile if the device needs intranet connectivity to support enrollment.  

> [!NOTE]  
>  The current branch of Configuration Manager supports enrollment in On-premises Mobile Device Management for devices running the following operating systems:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

The following tasks explain how to bulk-enroll computers and devices for On\-premises Mobile Device Management:  

-   [Create a certificate profile](#bkmk_createCert)  

-   [Create a Wi-Fi profile](#CreateWifi)  

-   [Create an enrollment profile](#bkmk_createEnroll)  

-   [Create an enrollment package (ppkg) file](#bkmk_createPpkg)  

-   [Use the package to bulk-enroll a device](#bkmk_getPpkg)  

-   [Verify enrollment of device](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Create a certificate profile  
 The main component of the enrollment package is a certificate profile, which is used to automatically provision a trusted root certificate to the device being enrolled.  This root certificate is required for trusted communication between the devices and the site system roles needed for On\-premises Mobile Device Management. Without the root certificate, the device would not be trusted in HTTPS connections between it and the servers hosting the enrollment point, enrollment proxy point, distribution point, and device management point site system roles.  

 As part of preparing the system for On\-premises Mobile Device Management, you export a root certificate that you can use in the enrollment package's certificate profile. For instructions on how to get the trusted root certificate, see [Export the certificate with the same root as the web server certificate](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Use the exported root certificate to create a certificate profile. For instructions, see [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="CreateWifi"></a> Create a Wi-Fi profile  
 The other component of the package used for bulk enrollment is a Wi-Fi profile. Some devices might not have the network connectivity needed to support enrollment until a network settings are provisioned. Including a Wi-Fi profile in the enrollment package provides a means for  establishing network connectivity for the device.  

 To create a Wi-Fi profile in Configuration Manager, follow the instructions in [How to create Wi-Fi profiles in System Center Configuration Manager](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Keep the following two issues in mind when creating a Wi-Fi profile for bulk enrollment:
>
> - The current branch of Configuration Manager only supports the following Wi-Fi security configurations for On\-premises Mobile Device Management:  
>   
>   - Security types: **WPA2 Enterprise** or **WPA2 Personal**  
>   - Encryption types: **AES** or **TKIP**  
>   - EAP types: **Smart Card or other certificate** or **PEAP**  
>
>
> - Although Configuration Manager has a setting for proxy server information in the Wi-Fi profile, it does not configure the proxy when the device is enrolled. If you need to set up a proxy server with your enrolled devices, you can deploy the settings using configuration items once devices are enrolled or create the second package using the Windows Image and Configuration Designer (ICD) to deploy along side the bulk enrollment package.

##  <a name="bkmk_createEnroll"></a> Create an enrollment profile  
 The enrollment profile allows you to specify settings required for device enrollment, including a certificate profile that will dynamically provision a trusted root certificate to the device and a Wi-Fi profile that will provision network settings if required.  

 Before creating an enrollment profile, make sure you have a certificate profile and Wi-Fi profile (if needed) created. For more information, see [Create a certificate profile](#bkmk_createCert) and [Create a Wi-Fi profile](#CreateWifi).  

#### To create an enrollment profile:  

1.  In the Configuration Manager console, click **Assets and Compliance** >**Overview** >**All Corporate-owned Device** >**Windows** >**Enrollment Profiles**.  

2.  Right click **Enrollment Profile** and then click **Create Profile**.  

3.  In the Create Enrollment Profile wizard, enter a  name for the profile,  make sure **On-Premises** is selected for **Management Authority**, and then click **Next**.  

4.  Select site code, and click **Next**.  

5.  Select **Intranet Only**, select enrollment proxy points the device will use initiate the enrollment process, and then click **Next**.  

6.  Select the certificate profile containing the trusted root certificate (this is the profile you created in [Create a certificate profile](#bkmk_createCert)), click **Next**.  

7.  Select the W-Fi profile containing the necessary network settings for devices to connect to the intranet (this is the profile you created in [Create a Wi-Fi profile](#CreateWifi)) and click **Next**.  

    > [!NOTE]  
    >  If you are not using a Wi-Fi profile for you enrollment package, skip this step.  

8.  Confirm the settings for the enrollment profile, and    click **Next**. Click **Close** to exit the wizard.  

##  <a name="bkmk_createPpkg"></a> Create an enrollment package (ppkg) file  
 The enrollment package is the file you use to bulk-enroll devices for On\-premises Mobile Device Management.  This file must be created with Configuration Manager. You can create similar types of packages with Windows Image and Configuration Designer (ICD), but only packages you create in Configuration Manager can be used to enroll devices for On\-premises Mobile Device Management from start to finish. Packages created with Windows ICD can only provide the user principal name (UPN) needed for enrollment, but not execute the actual enrollment process.  

 The process to create the enrollment package requires the Windows Assessment and Deployment Toolkit (ADK) for Windows 10.  On the server running the Configuration Manager console, make sure you have version 1511 of the Windows ADK  installed. For more information, see the ADK section of [Download kits and tools for Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)  

> [!TIP]  
>  If you remove an enrollment package from the Configuration Manager console, it cannot be used to enroll devices. You can use package removal as a way to manage packages that you no longer want used for bulk-enrolling devices.  

#### To create an enrollment package (ppkg) file:  

1.  Right-click on the profile just created (in [Create an enrollment profile](#bkmk_createEnroll), and click **Export**.  

2.  Click **Browse**, find a location you want to save the .ppkg file to, enter a name for the package, and then click **Save**.  

3.  If you want to password-protect the package, click the check box next to **Encrypt Package**, then click **Export** and wait for about 10 seconds for export to complete.  

    > [!NOTE]  
    >  If you encrypted the package, Configuration Manager provides a message with the decrypted password in it. Make sure you save the password information because you will need it to provision the package on devices.  

4.  Click **OK**.  

##  <a name="bkmk_getPpkg"></a> Use the package to bulk-enroll a device  
 You can use package to enroll devices before or after the device has been provisioned through the out-of-box experience (OOBE) process.   The enrollment package can also be included as part of an original equipment manufacturer's (OEM's) provisioning package.  

 The package has to be physically delivered to the device to use it for bulk enrollment. You can deliver the enrollment package to the device in various ways depending on your needs, including:  

-   Copy from file system  

-   Attach to email  

-   Copy across near field communication (NFC) connection  

-   Copy from memory card  

-   Scan barcode  

-   Copy from a tethered device  

-   Include in OEM provisioning package  

#### To bulk-enroll a device:  

1.  On device to be enrolled, find the enrollment package (using file explorer) and double-click the .ppkg file.  

2.  Click **Yes** in the User Account Control message.  

3.  In the dialog asking you if the package is from a source you trust,     click **Yes, add it**.  

     The enrollment process  starts and takes about 5 minutes.  

4.  Open **Settings**.  

5.  Click  **Accounts** > **Work access**. When enrollment is successful, you see an account under **CompanyApps**  

6.  Click the account, and then click **Sync**, which starts management with Configuration Manager.  

##  <a name="bkmk_verifyEnroll"></a> Verify enrollment of device  
 You can verify that devices have been successfully enrolled in the Configuration Manager console.  

-   Start the Configuration Manager console.  

-   Click **Assets and Compliance** > **Overview** > **Devices**. The enrolled device appears in the list.  
