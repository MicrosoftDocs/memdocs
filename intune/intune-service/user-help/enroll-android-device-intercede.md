---
# required metadata

title: Enroll Android device with Intune Company Portal and Intercede  
description: Enroll an Android device and set up derived credential authentication with Intercede.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/19/2022
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:
#ms.devlang:
ms.reviewer: jieyan
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
- M365-identity-device-management
---


# Set up Android device with Company Portal and Intercede

Enroll your device with the Intune Company Portal app to gain secure, mobile access to your work email, files, and apps. After your device is enrolled, it becomes *managed*, which means your organization can assign policies and apps to the device through a mobile device management (MDM) provider, such as Microsoft Intune.  

During enrollment, you'll also install a derived credential on your device. Your organization might require you to use the derived credential as an authentication method when accessing resources, or for signing and encrypting emails.

You likely need to set up a derived credential if you use a smart card to:

* Sign in to school or work apps, Wi-Fi, and virtual private networks (VPN)
* Sign and encrypt school or work emails using S/MIME certificates

In this article, you will:

* Enroll a mobile Android device with Intune Company Portal.
* Set up your smart card by installing a derived credential from your organization's derived credential provider, [Intercede](https://www.intercede.com/).  

## What are derived credentials?

A derived credential is a certificate that's derived from your smart card credentials and installed on your device. It grants you remote access to work resources, while preventing unauthorized users from accessing sensitive information.

Derived credentials are used to:

* Authenticate students and employees who sign in to school or work apps, Wi-Fi, and VPN
* Sign and encrypt school or work emails with S/MIME certificates

Derived credentials are an implementation of the National Institute of Standards and Technology (NIST) guidelines for Derived Personal Identity Verification (PIV) credentials as part of Special Publication (SP) 800-157.

## Prerequisites

 To complete enrollment, you must have:

* Your school or work-provided smart card
* Access to a computer or kiosk where you can sign in with your smart card
* A new or factory-reset device running Android 8.0 or later
* The Microsoft Intune app installed on your device

## Enroll device  

1. Turn on your new or factory-reset device.  
2. On the **Welcome** screen, select your language. If you've been instructed to enroll with a QR code or NFC, follow the step below that matches the method.  
     * NFC: Tap your NFC-supported device against a programmer device to connect to your organization's network. Follow the onscreen prompts. When you reach the screen for Chrome's Terms of Service, continue to step 5.  

     * QR code: Complete the steps in [QR code enrollment](#qr-code-enrollment).  

     If you've been instructed to use another method, continue to step 3.    

3. Connect to Wi-Fi and tap **NEXT**. Follow the step that matches your enrollment method. 

    * Token: When you get to the Google sign-in screen, complete the steps in [Token enrollment](#token-enrollment).  
    * Google Zero Touch: After you connect to Wi-Fi, your device will be recognized by your organization. Continue to step 4 and follow the onscreen prompts until setup is complete.    

   
4. Review the terms from Google. Then tap **ACCEPT & CONTINUE**.  

5. Review the terms from Chrome. Then tap **ACCEPT & CONTINUE**.  

6. On the sign-in screen, tap **Sign-in options** and then **Sign in from another device**. 

7. Write down the onscreen code.  

8. Switch to your smart card-enabled device and go to the web address that's shown on your screen. 

9. Enter the code you previously wrote down.

   > [!div class="mx-imgBorder"]
   > ![Screenshot of the Company Portal website "Enter code" prompt.](./media/enroll-android-device-disa-purebred/enter-code-intercede.png)

10. Insert your smart card to sign in.  

11. On the sign-in screen, select your work or school account. Then switch back to your mobile device.

12. Depending on your organization's requirements, you might be prompted to update settings, such as screen lock or encryption. If you see these prompts, tap **SET** and follow the onscreen instructions.  

       ![Example image of Set up your work phone screen, highlighting Set button.](./media/enroll-android-device-disa-purebred/fully-managed-intune-app-10.png)   

13. To install work apps on your device, tap **INSTALL**. After installation is complete, tap **NEXT**.  

14. Tap **START** to open the Microsoft Intune app. 
 

15. Return to the Intune app on your mobile device and follow the onscreen instructions until enrollment is done. 

    ![Example image of Set up access, register your device screen, highlighting Done button.](./media/enroll-android-device-disa-purebred/fully-managed-intune-app-19.png)   

16. Continue to the [set up your smart card](enroll-android-device-intercede.md#set-up-smart-card) section in this article to finish setting up your device.  

### QR code enrollment  
In this section, you'll scan your company-provided QR code.  When you're done, we'll redirect you back to the device enrollment steps.     
  
1. On the **Welcome** screen, tap the screen five times to start QR code setup.  

2. Follow any onscreen instructions to connect to Wi-Fi.  
3. If your device doesn't have a QR code scanner, the setup screens will show the progress as a scanner is installed. Wait for installation to complete.  
4. When prompted, scan the enrollment profile QR code that your organization gave you.  
5. Return to [Enroll device](#enroll-device), step 4 to continue setup.  

### Token enrollment  
In this section, you'll enter your company-provided token. When you're done, we'll redirect you back to the device enrollment steps.  

1. On the Google sign-in screen, in the **Email or phone** box, type **afw#setup**. Then tap **Next**. 

2. Choose **Install** for the **Android Device Policy** app. Continue through the installation. Depending on your device, you might need to review and accept additional terms.    

3. On the **Enroll this device** screen, select **Next**.  

4. Select **Enter code**.  

5. On the **Scan or enter code** screen, type in the code that your organization gave you.  Then select **Next**.  

6. Return to [Enroll device](#enroll-device), step 4 to continue setup.

## Set up smart card  

1. After enrollment is complete, the Intune app will notify you to set up your smart card. Tap the notification. If you don't get a notification, check your email.

   > [!div class="mx-imgBorder"]
   > ![Example screenshot of the Company Portal push notification on device home screen.](./media/enroll-android-device-disa-purebred/action-required-in-app-android.png)

2. On the **Set up smart card** screen:

   1. Tap the link to your organization's setup instructions. If your organization doesn't provide additional instructions, you'll be sent to this article.

   2. Tap **BEGIN**.  

   > [!div class="mx-imgBorder"]
   > ![Example screenshot of the Company Portal Set up mobile smart card access screen.](./media/enroll-android-device-entrust-datacard/smart-card-open-entrust-android.png)

3. Switch to your smart card-enabled device or self-service kiosk and open the MyID app. Sign in with your work credentials.

4. Select the option to request your ID.

5. When asked what profile you want to use, select the option to activate with a mobile credential. A QR code appears.  

6. Return to your Android device. On the Company Portal > **Get QR code** screen, tap **NEXT**.

    > [!div class="mx-imgBorder"]
    > ![Example screenshot of the Company Portal Get QR code screen.](./media/enroll-android-device-entrust-datacard/get-qr-code-entrust-android.png)

7. If you're prompted to allow the Intune app to use your camera, tap **Allow**.

8. Scan the image of the QR code that's on your smart card-enabled device.

9. The Intune app will start downloading and installing the certificates needed to access work or school resources. Depending on your internet connection, this process might take some time. Don't close the app during this time.

    > [!div class="mx-imgBorder"]
    > ![Example screenshot of the Company Portal "Downloading and installing certificates" screen](./media/enroll-android-device-entrust-datacard/install-certificates-entrust-android.png)

10. Once all of the certificates are processed, wait for the Intune app to finish setting up your device. You'll know setup is complete when you see the **You're all set!** screen.

    > [!div class="mx-imgBorder"]
    > ![Example screenshot of the "You're all set" screen](./media/enroll-android-device-disa-purebred/all-set-android.png)

## Next steps

After enrollment is complete, you'll have access to work resources, such as email, Wi-Fi, and any apps that your organization makes available. For more information about how to get, search for, install, and uninstall apps in the Intune app see:

* [Use managed apps on your device](use-managed-apps-on-your-device-android.md)  
* [Manage apps from the Company Portal website](manage-apps-cpweb.md)  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
