---
# required metadata

title: Enroll iOS or iPadOS device with Intune Company Portal and Intercede  
description: Learn how to enroll an iOS or iPadOS device and set up derived credential authentication with Intercede.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: tisilver
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# Set up iOS or iPadOS device with Company Portal and Intercede

Enroll your device with the Intune Company Portal app to gain secure, mobile access to your organization's email, files, and apps.  After your device is enrolled, it becomes *managed*. Your organization can assign policies and apps to the device through a mobile device management (MDM) provider, such as Intune.  

During enrollment, you'll also install a derived credential on your device. Your organization might require you to use the derived credential as an authentication method when accessing resources, or for signing and encrypting emails. 

You likely need to set up a derived credential if you use a smart card to:

* Sign in to school or work apps, Wi-Fi, and virtual private networks (VPN)
* Sign and encrypt school or work emails using S/MIME certificates  

In this article, you will:  

* Enroll a mobile iOS or iPadOS device with Intune Company Portal.  
* Get a derived credential from your organization's derived credential provider, [Intercede](https://www.intercede.com/).   


## What are derived credentials?  
A derived credential is a certificate that's derived from your smart card credentials and installed on your device. It grants you remote access to work resources, while preventing unauthorized users from accessing sensitive information.  

Derived credentials are used to: 
* Authenticate students and employees who sign in to school or work apps, Wi-Fi, and VPN
* Sign and encrypt school or work emails with S/MIME certificates  

Derived credentials are an implementation of the National Institute of Standards and Technology (NIST) guidelines for Derived Personal Identity Verification (PIV) credentials as part of Special Publication (SP) 800-157.  

## Prerequisites

 To complete enrollment, you must have:

* Your school or work-provided smart card
* Access to a computer or self-service kiosk where you can sign in with your smart card
* Your mobile device
* The Intune Company Portal app for iOS and iPadOS installed on your device


## Enroll device  
1. Open the Company Portal app for iOS/iPadOS on your mobile device and sign in with your work account.  
2. Write down the code that appears on screen.  

    ![Example image of Company Portal app with onscreen message and code.](./media/enroll-ios-device-intercede/copy-code-intercede.png)  

1. Switch to your smart card-enabled device and go to https://microsoft.com/devicelogin. 

1. Enter the code you previously wrote down.
 
2. Insert your smart card to sign in.   

3. Return to the Company Portal app on your mobile device and follow the onscreen instructions to enroll your device.  
4. After enrollment is complete, Company Portal will notify you to set up your smart card. Tap the notification. If you don't get a notification, check your email.   

    ![Example screenshot of the Company Portal push notification on device home screen.](./media/enroll-ios-device-intercede/action-required-in-app-intercede.png)  

5. On the **Setup mobile smart card access** screen:  
    a. Tap the link to your organization's setup instructions. If your organization doesn't provide additional instructions,you'll be sent to this article.  
    b. Tap **Begin**.  

    ![Example screenshot of the Company Portal Set up mobile smart card access screen.](./media/enroll-ios-device-intercede/smart-card-info-intercede.png)  

6. Switch to your smart card-enabled device or self-service kiosk and open the MyID app. Sign in with your work credentials.  
7. Select the option to request your ID. 
8. When asked what profile you want to use, select the option to activate with a mobile credential. A QR code appears.  
9. Return to your mobile device. On the Company Portal > **Get QR code** screen, tap **Continue**.  

    ![Example screenshot of the Company Portal Get QR code screen.](./media/enroll-ios-device-intercede/get-qr-code-intercede.png) 
 
10. Tap **Use Camera** > **OK**.  

    ![Example screenshot of a Company Portal prompt, asking permission to allow camera access.](./media/enroll-ios-device-intercede/allow-cp-camera-access-intercede.png)  

11. Scan the image of the QR code that's on your smart card-enabled device. 
12. Wait for Company Portal to finish setting up your device.  

## Next steps  
After enrollment is complete, you'll have access to work resources, such as email, Wi-Fi, and any apps that your organization makes available. For more information about how to get, search for, install, and uninstall apps in the Company Portal see:

* [Manage apps from the Company Portal website](manage-apps-cpweb.md)  
* [Use managed apps on your device](use-managed-apps-on-your-device-ios.md)  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
