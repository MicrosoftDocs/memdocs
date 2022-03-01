---
# required metadata

title: Get an Apple MDM Push certificate for Intune
titleSuffix: 
description: Get an Apple MDM Push certificate to manage iOS/iPadOS devices with Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/08/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Get an Apple MDM push certificate

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Upload and renew your Apple MDM push certificates in Microsoft Intune. An Apple MDM Push certificate is required to manage iOS/iPadOS and macOS devices in Microsoft Intune, and enables devices to enroll via: 

- The Intune Company Portal app.
- Apple bulk enrollment methods, such as the Device Enrollment Program, Apple School Manager, and Apple Configurator.

Certificates must be renewed annually. 

This article describes how to use Intune to create and renew an Apple MDM push certificate.  


## Steps to get your certificate
Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Apple enrollment** > **Apple MDM Push Certificate**, and then follow these steps.

### Step 1. Grant Microsoft permission to send user and device information to Apple
Select **I agree.** to give Microsoft permission to send data to Apple.

![The Configure MDM Push Certificate screen with MDM Push not set up.](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### Step 2. Download the Intune certificate signing request required to create an Apple MDM push certificate
Select **Download your CSR** to download and save the request file locally. The file is used to request a trust relationship certificate from the Apple Push Certificates Portal.

### Step 3. Create an Apple MDM push certificate
Select **Create your MDM push Certificate** to go to the Apple Push Certificates Portal. Sign in with your company email address Apple ID, and then click **Create a Certificate**. Select **Choose File** and browse to the certificate signing request file, and then choose **Upload**. On the Confirmation page, choose **Download** to the download the certificate (.pem)  file, and save the file locally.

> [!NOTE]
> The certificate is associated with the Apple ID used to create it. As a best practice, use a company email address for Apple ID for management tasks and make sure the mailbox is monitored by more than one person like a distribution list. Avoid using personal Apple ID.

> [!NOTE]
> If you plan to federate your existing AAD Accounts with Apple for Managed Apple ID Usage, please contact Apple to have the existing APNS certificate migrated to new managed apple ID. Refer https://support.apple.com/en-in/guide/apple-school-manager/apd6603d9206/web for more info.

### Step 4. Enter the Apple ID used to create your Apple MDM push certificate
Record this ID as a reminder for when you need to renew this certificate.

### Step 5. Browse to your Apple MDM push certificate to upload
Go to the certificate (.pem) file, choose **Open**, and then choose **Upload**. With the push certificate, Intune can enroll and manage Apple devices.

## Renew Apple MDM push certificate
The Apple MDM push certificate is valid for one year. You must renew it annually to maintain iOS/iPadOS and macOS device management. Once the certificate expires, there is a 30-day grace period to renew it.  

Renew the MDM push certificate with the same Apple ID you used to create it.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Apple enrollment** > **Apple MDM Push Certificate**.
2. Choose **Download your CSR** to download and save the request file locally. The file is used to request a trust relationship certificate from the Apple Push Certificates Portal.
3. Select **Create your MDM push Certificate** to go to the Apple Push Certificates Portal. Find the certificate you want to renew and select **Renew**.
4. On the **Renew Push Certificate** screen, provide notes to help you identify the certificate in the future, select **Choose File** to browse to the new request file you downloaded, and choose **Upload**.
   > [!TIP]
   > A certificate can be identified by its UID. Examine the **Subject ID** in the certificate details to find the GUID portion of the UID. Or, on an enrolled iOS/iPadOS device, go to **Settings** > **General** > **Device** **Management** > **Management Profile** > **More Details** > **Management Profile**. The second line item, **Topic**, contains the unique GUID that you can match up to the certificate in the Apple Push Certificates portal.
 
6. On the **Confirmation** screen, select **Download** and save the .pem file locally.
7. In [Intune](https://go.microsoft.com/fwlink/?linkid=2090973), select the **Apple MDM push certificate** browse icon, select the .pem file downloaded from Apple, and choose **Upload**.

Your Apple MDM push certificate appears **Active** and has 365 days until expiration.

## Next steps  

For more information about enrollment options, see [Choose how to enroll iOS/iPadOS devices](ios-enroll.md).
