---
# required metadata

title: Set up personal iOS device in Intune Company Portal app | Microsoft Docs
description: Describes how to enroll and register a personal iPhone or iPad for work or school in the Intune Company Portal app.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/21/2023
ms.topic: end-user-help
ms.localizationpriority: high
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 6eeec7aa-1b07-4ce3-894c-13e09b89bdd4
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience: 

ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Set up personal iOS device for work or school      

**Applies to iOS/iPadOS**  
Enroll and register your personal iPhone or iPad for work or school to access apps, Wi-Fi, and other resources. This article describes how to enroll your device using the Intune Company Portal app.

> [!IMPORTANT]
> We do not sell any data collected by our service to any third parties for any reason.  

</br>

> [!VIDEO https://www.youtube.com/embed/mJyv6YcHi7c?rel=0]

> [!NOTE]
> If you tried to access your work email in the Mail app, and received a prompt to get your device managed, you're in the right place. Follow the instructions in this article to regain access to your email and other work resources on your iOS device.  

## Before you begin    

[Install the Intune Company Portal app](https://apps.apple.com/us/app/intune-company-portal/id719171358) from the Apple App Store. The Company Portal app is used to enroll and manage your device, install work apps, and get IT support.  The app supports devices running iOS 14.0 and later.  

You also need the Safari web browser on your device.  

## Enroll device  

Maintain a Wi-Fi connection until all steps are complete. Pausing for more than a few minutes during enrollment might cause the Company Portal app to close or end setup. If this happens, reopen the app and try again.  

1. Open the Company Portal app on your personal device and sign in with your work or school account.  

2. When prompted to receive Company Portal notifications, tap **Allow.** Company Portal uses notifications to alert you of things you need to do to make your device more secure and maintain work access.  

3. On the **Set up access** screen, select **Begin.**   

    ![Example screenshot of Company Portal, "Set up access" screen.](./media/enroll-your-device-in-intune-ios/ios-enrollment-checklist-1909.PNG)  

4. Select your device and enrollment type.  

    ![Example screenshot of Company Portal, "Select device and enrollment type" screen, device type options.](./media/enroll-your-device-in-intune-ios/ios-device-type-1909.PNG)  

   Your options:  

    * Tap **(Organization) owns this device** if you received your device from your organization. Then skip to [Secure entire device](#secure-entire-device) in this article to finish setup.  
    * Tap **I own this device** if you're using a personal device that you brought from home. Then continue to the next step.  

    If you don't see this screen, skip to [Secure entire device](#secure-entire-device).  


6. Choose how to protect the data on your device once it's enrolled.  

    ![Example screenshot of Company Portal, "Select device and enrollment type" screen, enrollment type options.](./media/enroll-your-device-in-intune-ios/ios-enrollment-type-1909.PNG)  

    Your options:  

    * Tap **Secure entire device** to secure all apps and data on the device. Then go to [Secure entire device](enroll-your-device-in-intune-ios.md#secure-entire-device) to finish setup.
    * Tap **Secure work-related apps and data only** to secure only the apps and data you access with your work account. Then go to [Secure work-related apps and data](enroll-your-device-in-intune-ios.md#secure-work-related-apps-and-data).  

### Secure entire device  

1. On the **Device management and privacy** screen, read through the list of device information your organization can and can't see. Then tap **Continue**.  


 > [!IMPORTANT]
> These next steps and screens will differ depending on your iOS version. Follow the steps for your iOS version. 

2. Safari opens the Company Portal website on your device. When prompted to download the configuration profile, tap **Allow**. If you're on a device running:  
    * iOS 12.2 and later: When the download is complete, tap **Close**. Then continue to step 3.  
    * iOS 12.1 and earlier: When the download is complete, you are automatically redirected to the Settings app. Skip to step 4.  
 
    If you accidentally tap **Ignore**, refresh the page. You'll be prompted to open the Company Portal app. Once you're there, tap **Download again**.

  > [!NOTE]
  > You must install the management profile as described in the next steps within 8 minutes of downloading it. If you don't, the profile will be removed and you'll have to restart enrollment.  

3. When prompted to open Company Portal, tap **Open**. Read through the information on the **How to install Management Profile** screen.  

4. Go to the Settings app and tap **Enroll in < organization name >** or **Profile Downloaded**.  

    ![Example screenshot of the Settings app, Enroll in organization option.](./media/enroll-your-device-in-intune-ios/enroll-in-organization-ios-1909.PNG)  

   If neither options appear, go to **General** and select the VPN & device management option to view installed profiles. If you still don't see the profile, try downloading it again. 

5. Tap **Install**.  
    
6. Enter your device password. Then tap **Install**.    

7. The next screen is a standard system warning about device management. To continue with installation, tap **Install**. If you're prompted to trust remote management, tap **Trust**.  

8. After installation is complete, tap **Done**. To verify that the profile was installed, go to your VPN and device management settings. You should see the profile listed under **Mobile Device Management**.   

9. Return to the Company Portal app. Company Portal will begin to sync and set up your device. Company Portal might prompt you to update additional device settings. If it does, tap **Continue**.  

10. You'll know that setup is complete when all items in the list show a green checkmark. Tap **Done**.   

> [!Note]
> If your organization monitors voice and data limits, or provides you with a company-owned device, you might have a few more steps to complete. If your organization is part of Apple's Device Enrollment Program, find out [how to enroll your company-owned device](enroll-your-device-dep-ios.md).  

### Secure work-related apps and data  
1. The **Download Microsoft Authenticator** screen appears (if you already have Authenticator, you won't see this screen so skip to step 2).  
    1. Tap **Download from App Store**.
    2. When the App Store opens, install the app. 
    3. Return to Company Portal and tap **Continue**.    
    
   After you install Microsoft Authenticator, you won't need to do anything else with the app. It just needs to be present on your device. 

   ![Example screenshot of Company Portal, "Download Microsoft Authenticator" screen.](./media/enroll-your-device-in-intune-ios/download-ms-authenticator-1909.PNG)  

2. On the **Device management and privacy** screen, read through the list of device information your organization can and can't see. Then tap **Continue**.  


 > [!IMPORTANT]
> These next steps and screens will differ depending on your iOS version. Follow the steps for your iOS version. 

3. Safari opens the Company Portal website on your device. When prompted to download the configuration profile, tap **Allow**. If you're on a device running:  
    * iOS 12.2 and later: When the download is complete, tap **Close**. Then continue to step 4.  
    * iOS 12.1 and earlier: When the download is complete, you are automatically redirected to the Settings app. Skip to step 5.  
 
    If you accidentally tap **Ignore**, refresh the page. You'll be prompted to open the Company Portal app. From the app, you can tap **Download again**.

  > [!NOTE]
  > You must install the management profile as described in the next steps within 8 minutes of downloading it. If you don't, the profile will be removed and you'll have to restart enrollment.  

4. Go to the Settings app.

5. Go to **General** and select the VPN & device management option.

6. **Sign in** with your work or school account, or with the Apple ID provided to you by your organization.

7. Select **Sign In to iCloud**.
   
8. Enter the password for the username that's shown on screen. Then select **Continue**.

9. Select **Allow Remote Management**.
    
 Wait a few minutes while your device is configured and the management profile is installed.
 
 To confirm your device is ready to use for work, go to VPN & Device Management. Confirm that your work account is listed under **MANAGED ACCOUNT**.
 
 Microsoft Authenticator is required to access work apps. Wait a few minutes after enrollment for Authenticator to install on your device. An error message appears if you try to sign in to a work app without Authenticator.
 
 You might receive more prompts asking for your approval to install work apps. Select **Install** to approve installation.  

11. Return to the Company Portal app. Company Portal might prompt you to update additional device settings. If it does, tap **Continue**.    

12. You'll know that setup is complete when all items in the list show a green checkmark. Tap **Done**.  

## IT administrator support  
If you're an IT administrator and run in to problems while enrolling devices, see [Troubleshooting iOS device enrollment problems in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors). This article lists common errors, their causes, and steps to resolve them.  

## Next steps  
Find apps that will help you at work or school. Learn [how apps are made available](use-managed-apps-on-your-device-ios.md) to you through Company Portal.  

Still need help? Check in with your company support. You can find their contact information on the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
