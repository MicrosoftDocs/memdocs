---
title: "Enable platform enrollment using System Center Configuration Manager | Microsoft Docs"
description: "Enable platform enrollment using System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9163b77-a67d-4139-8272-bb1dfdb8707c
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillmanms.author: mtillman
manager: angrobe
---
# Enable platform enrollment with System Center Configuration Manager and Microsoft Intune*Applies to: System Center Configuration Manager (Current Branch)*
Different device platforms require additional configuration to enable device enrollment:
  - [iOS and Mac enrollment setup](#ios-and-mac-enrollment-setup): Get an Apple MDM Push certificate
  - [Windows enrollment setup](#windows-enrollment-setup): Configure DNS and enable enrollment for both Windows PCs, Windows 10 Mobile, and Windows Phone devices
  - Android: Android devices require no additional steps to enable enrollment

Once you enable MDM management, you can specify the number of devices each user can enroll, up to 15 devices per user.

## iOS and Mac enrollment setup
  The following steps enable management for Apple devices by uploading an Apple MDM Push certificate to the Intune service.

  1.  **Download a certificate signing request** - A certificate signing request file (.csr) is required to request an APNs certificate from Apple.  

      1.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services**> **Microsoft Intune Subscriptions**.  

      2.  On the **Home** tab, click **Create APNs certificate request**. The **Request Apple Push Notification Service Certificate Signing Request** dialog box opens.  

      3.  **Browse** to the path to save the new certificate signing request (.csr) file. Save the certificate signing request (.csr) file locally.  

      4.  Click **Download**. The new Microsoft Intune .csr file downloads and is saved by Configuration Manager. The .csr file is used to request a trust relationship certificate from the Apple Push Certificates Portal.  

  2.  **Request an APNs certificate from Apple** - The Apple Push Notification service (APNs) certificate is used to establish a trust relationship between the management service, Intune, and enrolled iOS mobile devices.  

      1.  In a browser, go to the [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) and sign in with your company Apple ID. This Apple ID must be used in future to renew your APNs certificate.  

      2.  Complete the wizard using the certificate signing request (.csr) file. Download the APNs certificate and save the .pem file locally. This APNs certificate (.pem) file is used to establish a trust relationship between the Apple Push Notification server and Intune's mobile device management authority.  

  3.  **Enable enrollment and upload the APNs certificate** - To enable iOS enrollment, upload the APNs certificate.  

      1.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.  

      2.  On the **Home** tab in the **Subscription** group, click **Configure Platforms** > **iOS**.  

          > [!NOTE]  
          >  Do not upload the Apple Push Notification service (APNs) certificate until you enable iOS enrollment in the Configuration Manager console.  

      3.  In the **Microsoft Intune Subscription Properties** dialog box, select the **iOS** tab and click to select the **Enable iOS enrollment** checkbox.  

      4.  Click **Browse**, and go to the APNs certificate (.cer) file downloaded from Apple. Configuration Manager displays the APNs certificate information. Click **OK** to save the APNs certificate to Intune.    


Additional information about [iOS and Mac enrollment](enroll-hybrid-ios-mac.md).

## Windows enrollment setup  
You can use Configuration Manager with  Intune to manage desktops, laptops, and other devices running Windows as mobile devices. You can also configure Windows 10 devices to [automatically enroll when they join Azure Active Directory](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment) by adding a company or school account on their device.

A DNS alias (CNAME record type) makes it easier for users to enroll their devices by automatically populating the server name during device enrollment. You can then enable enrollment for Windows PCs mobile devices.  

1. In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscriptions**, then do the following:  
  - **Windows PCs:** On the **Home** tab, click **Configure Platforms**, and then click **Windows**. On the **General** tab, select **Enable Windows enrollment**.  
  - **Windows 10 Mobile and Windows Phone:** On the **Home** tab, click **Configure Platforms**, and then click **Windows Phone**.  On the **General** tab, choose  **Windows Phone 8.1 and Windows 10 Mobile**.

2.  You can also configure Configuration Manager to simplify enrollment using the Company Portal app.
(Optional) Create a DNS alias (CNAME record type) in your company's DNS records that redirects requests sent to a URL in your company's domain to Microsoft's cloud service servers.  For example, if your company's domain is contoso.com, you should to create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com.  

|Type|Host name|Points to|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

For additional information, see [Windows enrollment](enroll-hybrid-windows.md).

## Android enrollment setup
You can use Configuration Manager with  Intune to manage phonse and tablets  running Android.
1.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.  

2.  On the **Home** tab in the **Subscription** group, click **Configure Platforms** > **Android**.  

3.  In the **Microsoft Intune Subscription Properties** dialog box, select the **Android** tab and click to select the **Enable Android enrollment** checkbox.

For additional information, see [Android](enroll-hybrid-android.md).
