---
title: "Set up iOS and Mac hybrid device management with System Center Configuration Manager and Microsoft Intune | Microsoft Docs"
description: "Set up iOS device management with System Center Configuration Manager and Microsoft Intune."
ms.custom: na
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe

---
# Set up iOS hybrid device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

With Configuration Manager and Intune, you enable iOS and macOS device enrollment to give access to company email and resources to iPhone, iPad, and Mac users. Once users install the Intune company portal app, their devices can be targeted with policy. Before you can manage iOS and Mac devices, you must import an Apple Push Notification service (APNs) certificate from Apple. This certificate lets Intune manage iOS and Mac devices by establishing a connection with Apple's device management service.  

 You can also enroll corporate-owned iOS devices.  See [Enroll company-owned devices](enroll-company-owned-devices.md).  

**Prerequisites**<br>
Before you can set up enrollment for any platform, complete the prerequisites and procedures in [Setup hybrid MDM](setup-hybrid-mdm.md).

To support enrollment of iOS  devices, you must follow these steps:  

## Download a certificate signing request
A certificate signing request file is required to request an APNs certificate from Apple.  

1.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services**> **Microsoft Intune Subscriptions**.  

2.  On the **Home** tab, click **Create APNs certificate request**. The **Request Apple Push Notification Service Certificate Signing Request** dialog box opens.  

3.  **Browse** to the path to save the new certificate signing request file. Save the certificate signing request file locally.  

4.  Click **Download**. The new Microsoft Intune certificate signing request file downloads and is saved by Configuration Manager. The certificate signing request file is used to request a trust relationship certificate from the Apple Push Certificates Portal.  

## Request an MDM Push certificate from Apple
The MDM Push certificate is used to establish a trust relationship between the management service, Intune, and enrolled iOS mobile devices.  

1.  In a browser, go to the [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) and sign in with your company Apple ID. This Apple ID must be used in future to renew your APNs certificate.  

2.  Complete the wizard using the certificate signing request (.csr) file. Download the MDM Push certificate and save the pem file locally. This certificate (.pem) file is used to establish a trust relationship between the Apple Push Notification server and Intune's mobile device management authority.  

> [!NOTE]  
>  Do not upload the Apple Push Notification service (APNs) certificate to Intune until you enable iOS enrollment in the Configuration Manager console.  

## Enable enrollment and upload the MDM Push certificate
To enable iOS enrollment, upload the APNs certificate.  

1.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.  

2.  On the **Home** tab in the **Subscription** group, click **Configure Platforms** > **iOS**.  

3.  In the **Microsoft Intune Subscription Properties** dialog box, select the **iOS** tab and click to select the **Enable iOS enrollment** checkbox.  
4.  Click **Browse**, and go to the APNs certificate (.cer) file downloaded from Apple. Configuration Manager displays the APNs certificate information. Click **OK** to save the APNs certificate to Intune.  

After you're set up, you need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/end-user-educate). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

## Configure enrollment restrictions

You can limit devices that can enroll by blocking personally owned devices. This prevents users from enrolling their devices using the Company Portal. If you block personally owned devices, only the following devices can enroll:
- [Predeclared devices](predeclare-devices-with-hardware-id.md)
- [Apple Configurator managed devices](ios-hybrid-enrollment-using-apple-configurator.md)
- [Device Enrollment Program (DEP) managed devices](ios-device-enrollment-program-for-hybrid.md)
- Devices enrolled with a [device enrollment manager account](enroll-devices-with-device-enrollment-manager.md)

### To enable enrollment restrictions
1.	In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.
2.	On the **Home** tab in the **Subscription** group, click **Configure Platforms** > **iOS**.
3.	Choose **Block personally owned devices** to limit enrollment to company-owned devices.

> [!div class="button"]
[< Previous step](create-service-connection-point.md)  [Next step >](set-up-additional-management.md)
