---
# required metadata

title: Enroll your Mac with Intune Company Portal | Microsoft Docs
description: Learn how to enroll your Mac in Intune with the Company Portal app.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:
#ms.devlang:
ms.reviewer: kakyker
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Enroll your macOS device using the Company Portal app  

Enroll your macOS device with the Intune Company Portal app to gain secure access to your work or school email, files, and apps.

Organizations typically require you to enroll your device before you can access proprietary data. After your device is enrolled, it becomes *managed*. Your organization can assign policies and apps to the device through a mobile device management (MDM) provider, such as Intune. To get continuous access to work or school information on your device, you must configure your device to match your organization’s policy settings.  

This article describes how to use the Company Portal app for macOS to enroll, configure, and maintain your device so that you meet your organization's requirements.  


## What to expect from the Company Portal app

During initial setup, the Company Portal app requires you to sign in and authenticate yourself with your organization. Company Portal then informs you of any device settings you need to configure to meet your organization's requirements. For example, organizations often set minimum or maximum character password requirements that you'll be required to meet.    

After you enroll your device, Company Portal will always make sure that your device is protected according to your organization's requirements. For example, if you install an app from an untrusted source, Company Portal will alert you and might restrict access to your organization's resources. App protection policies like this one are common. To regain access, you'll likely need uninstall the untrusted app. 

If after enrollment your organization enforces a new security requirement, such as multi-factor authentication, Company Portal will notify you. You'll have the chance to adjust your settings so that you can continue to work from your device.  

To learn more about enrollment, see [What happens when I install the Company Portal app and enroll my device?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## Get your macOS device managed  
Use the following steps to enroll your macOS device with your organization. Your device must be running macOS 10.12 or later.   

> [!NOTE]
> Throughout this process, you might be prompted to allow Company Portal to use confidential information that's stored in your keychain. These prompts are part of Apple security. When you get the prompt, type in your login keychain password and select **Always Allow**. If you press **Enter** or **Return** on your keyboard, the prompt will instead select **Allow**, which may result in additional prompts.  

### Install Company Portal app  
1. Go to [Enroll My Mac](https://go.microsoft.com/fwlink/?linkid=853070).  
2. The Company Portal installer .pkg file will download. Open the installer and continue through the steps. 
3. Agree to the software license agreement. 
4. Enter your device password or registered fingerprint to install the software.  
5. Open Company Portal. 

> [!IMPORTANT]
> Microsoft AutoUpdate might open to update your Microsoft software. After all updates are installed, open the Company Portal app. For the best setup experience, install the latest versions of Microsoft AutoUpdate and Company Portal.  


### Enroll your Mac  


1. Sign in to Company Portal with your work or school account.  
2. When the app opens, select **Begin**.  
3. Review what your organization can and can't see on your enrolled device. Then select **Continue**.
4.  If prompted to, enter your device password on the **Install management profile** screen.

    ![Example screenshot of Company Portal, Install management profile screen, highlighting password prompt.](./media/install-management-profile-macos-1912.PNG)   
5. On the **Confirm device management** screen, select **Open System Preferences**.  

    ![Example screenshot of Confirm device management screen, highlighting "Open System Preferences" button.](./media/confirm-device-management-macos-1912.PNG)  
6. Your device's system preferences will open. Select **Management Profile** from the device profiles list and then select **Approve** > **Approve**.  
    ![Example screenshot of System Preferences, Management Profile screen, highlighting "Approve" button.](./media/management-profile-approve-macos-1912.PNG)   
1. Return to Company Portal and select **Continue**.    
2. Your organization might require you to update your device settings. When you're done updating settings, select **Check settings**.  

    ![Example screenshot of Company Portal, Update device settings screen, highlighting "Check settings" button.](./media/update-settings-mac-1911.PNG)  
9. When setup is complete, select **Done**.  


 ## Troubleshooting and feedback   

If you run into issues during enrollment, go to **Help** > **Send Diagnostic Report** to report the issue to Microsoft app developers. This information is used to help improve the app. They'll also use this information to help resolve the problem if your IT support person reaches out to them for help.  

After you report the problem to Microsoft, you can send the details of your experience to your IT support person. Select **Email Details**. Type in what you experienced in the body of the email. To find your support person's email address, go to the Company Portal app > **Contact**. Or check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
 

Additionally, the Microsoft Intune Company Portal team would love to hear your feedback. Go to **Help** > **Send Feedback** to share your thoughts and ideas.  

## Unverified profiles  
When you view the installed mobile device management (MDM) profiles in **System Preferences** > **Profiles**, some profiles might show an unverified status. As long as the management profile shows a verified status, you don’t need to be concerned.  

The management profile is what defines the MDM channel connection. As long as the management profile is verified, any other profiles delivered to the machine via that channel inherit the security traits of the management profile.  

## Updating the Company Portal app

Updating the Company Portal app is done the same way as any other Office app, through Microsoft AutoUpdate for macOS. Find out more about [updating Microsoft apps for macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## Next Steps  
Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  


