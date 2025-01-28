---
# required metadata

title: Apple School Manager - get Apple token and assign devices
titleSuffix: Microsoft Intune
description: Get the Apple token needed to set up Apple School Manager and Microsoft Intune for corporate-owned iOS/iPadOS devices. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/07/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
---

# Get an Apple token for school devices

Before you can enroll corporate-owned iOS/iPadOS devices with Apple School Manager, you need a token (.p7m) file from Apple. This token lets Intune sync information about Apple School Manager-participating devices. It also permits Intune to perform enrollment profile uploads to Apple and to assign devices to those profiles. While you are in the Apple portal, you can also assign device serial numbers to manage. 

## Get Apple token     
In the first set of steps, you download the Intune public key certificate required to create an Apple token.    

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.  
1. Select the **Apple** tab.  
1. Choose **Enrollment program tokens**.  
1. Select **Create**.  
1. Select **I agree** to give permission to Microsoft to send user and device information to Apple. 
1. Select **Download your public key**. This step downloads and saves the encryption key (.pem) file locally. The .pem file is used to request a trust-relationship certificate from the Apple School Manager portal. 

   In the next set of steps, you download a token and assign devices. Keep the browser and tab with the admin center open while you're completing steps in Apple School Manager. 
   
     > [!TIP]
     > The following steps describe what you need to do in Apple School Manager. For the specific steps, see the [Apple School Manager User Guide](https://support.apple.com/guide/apple-school-manager/device-workflow-axm6a88f692e/1/web/1) (opens Apple Support).  

1. Choose **Create a token via Apple School Manager**, and sign in to [Apple School Manager](https://school.apple.com) with your company Apple ID. You can use this Apple ID to renew your Apple School Manager token.
1. In Apple School Manager, go to your MDM Server assignments to add an MDM server.
1. Enter the mobile device management (MDM) server name. The server name is for your reference to identify the MDM server. It isn't the name or URL of the Microsoft Intune server.
1. Upload the public key certificate file (.pem file).  
1. Save your MDM server. 
1. Select the download button to download the server token (.p7m) file to your computer. 
1. Go to **Devices** and select the devices you want to assign to this token. You can sort by various device properties, like serial number. You can also select multiple devices simultaneously.
1. Select **Edit MDM Server**. Select the MDM server you just added, and then save your changes. This step assigns devices to the token.
1. Return to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and enter the Apple ID you used to create the token. 

   ![Example screenshot showing the Apple ID used to create the enrollment program token and browsing to the enrollment program token.](./media/apple-school-manager-set-up-ios/image03.png)  

1. For **Apple token**, browse to the certificate (.pem) file. Select **Open**, and then choose **Create**. With the push certificate, Intune can enroll and manage iOS/iPadOS devices by pushing policies to enrolled mobile devices. Intune automatically syncs your Apple School Manager devices from Apple.  

## Next steps  
This series of articles describes how to set up Microsoft Intune for devices purchased through Apple School Manager. 

1. [Prerequisites](apple-school-manager-set-up-ios.md)
1. 🡺 Get an Apple token for school devices (*You are here*)  
1. [Create an Apple enrollment profile](apple-school-manager-step-2.md)  
1. [Sync and distribute devices](apple-school-manager-step-3.md) 