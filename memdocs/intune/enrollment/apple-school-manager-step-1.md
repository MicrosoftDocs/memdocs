---
# required metadata

title: Apple School Manager - get Apple token and assign devices
titleSuffix: Microsoft Intune
description: Get the Apple token needed to set up Apple School Manager and Microsoft Intune for corporate-owned iOS/iPadOS devices. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/06/2025
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

# Get an Apple token and assign devices

Before you can enroll corporate-owned iOS/iPadOS devices with Apple School Manager, you need a token (.p7m) file from Apple. This token lets Intune sync information about Apple School Manager-participating devices. It also permits Intune to perform enrollment profile uploads to Apple and to assign devices to those profiles. While you are in the Apple portal, you can also assign device serial numbers to manage. 

## Step 1: Download the Intune public key certificate required to create an Apple token

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.    
1. Select the **Apple** tab.  
1. Choose **Enrollment Program Tokens**.  
1. Select **Add**.  
1. Select **Download your public key** to download and save the encryption key (.pem) file locally. The .pem file is used to request a trust-relationship certificate from the Apple School Manager portal.   

## Step 2: Download a token and assign devices
1. Choose **Create a token via Apple School Manager**, and sign in to Apple School with your company Apple ID. You can use this Apple ID to renew your Apple School Manager token.
2. In the [Apple School Manager portal](https://school.apple.com), go to **MDM Servers**, and then choose **Add MDM Server** (upper right).
3. Enter the MDM server name. The server name is for your reference to identify the mobile device management (MDM) server. It isn't the name or URL of the Microsoft Intune server.
4. Choose **Upload File...** in the Apple portal, browse to the .pem file, and choose **Save MDM Server** (lower right).
5. Choose **Get Token** and then download the server token (.p7m) file to your computer.
6. Go to **Device Assignments**. Choose your devices by manually entering their serial numbers or order number.  
7. Choose the action **Assign to Server**, and choose the **MDM Server** you created.
8. Specify how to **Choose Devices**, then provide device information and details.
9. Choose **Assign to Server** and choose the &lt;ServerName&gt; specified for Microsoft Intune, and then choose **OK**.

## Step 3: Save the Apple ID used to create this token

Return to the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and enter the Apple ID. 

![Screenshot of specifying the Apple ID used to create the enrollment program token and browsing to the enrollment program token.](./media/apple-school-manager-set-up-ios/image03.png)

## Step 4: Upload your token
In the **Apple token** box, browse to the certificate (.pem) file, choose **Open**, and then choose **Create**. With the push certificate, Intune can enroll and manage iOS/iPadOS devices by pushing policy to enrolled mobile devices. Intune automatically synchronizes your Apple School Manager devices from Apple.  

## Next steps  
This series of articles describes how to set up Microsoft Intune for devices purchased through Apple School Manager. 

1. [Prerequisites](apple-school-manager-set-up-ios.md)
1. 🡺 Get an Apple token and assign devices (*You are here*)  
1. [Create an Apple enrollment profile](apple-school-manager-step-2.md)  
1. [Sync managed devices](apple-school-manager-step-3.md) 