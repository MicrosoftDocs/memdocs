---
title: "Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune | Microsoft Docs"
description: "Prepare to manage Android mobile devices with Configuration Manager and Intune."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe

---
# Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This topic helps the IT admin enable hybrid enrollment of Android and Android for Work devices. Devices can then be managed with Configuration Manager by using a configured Microsoft Intune Subscription. Users can download the Android company portal app from Google Play that lets them enroll Android (including Samsung KNOX Standard) and Android for Work devices. As an Configuration Manager admin, you can manage compliance settings, wipe or delete Android devices, deploy apps, and collect software and hardware inventory. If the Android company portal app is not installed on Android devices, then you will not have all the management capabilities, such as inventory and compliance settings, but you can still deploy apps to Android devices.  

## Enable Android enrollment  
The following steps allow Configuration Manager to manage Android devices without a work profile (i.e. "classic Android" enrollment).

1.  **Prerequisites** - Before you can set up enrollment for any platform, complete the prerequisites and procedures in [Setup hybrid MDM](setup-hybrid-mdm.md).  
2.  In the Configuration Manager console in the **Administration** workspace, select **Overview** > **Cloud Services** > **Microsoft Intune Subscription** and select your Intune subscription.  
3.  On the **Home** tab in the **Subscription** group, select **Configure Platforms** > **Android**.  

4.  In the **Microsoft Intune Subscription Properties** dialog box, select the **Android** tab and click to select the **Enable Android enrollment** checkbox.  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

## Enable Android for Work enrollment
The following steps allow Configuration Manager to manage Android devices without a work profile (i.e. "classic Android" enrollment).

 1. Create a Google account at https://accounts.google.com/SignUp to use as your Android for Work admin account or sign in with the account that will be associated with all Android for Work management tasks for this Intune tenant. This could be a Google account shared among the administrators who manage Android devices. This is the Google account that your organization uses to manage and publish apps in the Play for Work console. You will use this account to approve apps in the Play for Work store, so keep track of the account name and password.
 2. Enable Android enrollment by binding the Google account to the Intune tenant managed in Configuration Manager:
   1. In the Configuration Manager console in the **Administration** workspace, select **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions** and select your Intune subscription.
   2. On the **Home** tab in the **Subscription** group, select **Configure Platforms** > **Android for Work**.
   3. In the dialog box, select **Configure Android for Work in the Intune console**. The Intune console opens in your web browser.
   4. Use your Intune administrator credentials to log in to the Intune portal.
   5. Select **Configure** to open Google Play's Android for Work website.
   6. On Google's sign-in page, enter the Google account credentials from step 1, and then provide your company information.
 3. When you return to the Intune portal, Android for Work is enabled and you have three enrollment options for Android for Work devices:
   - **Manage all devices as Android** - (Disabled) All Android devices, including devices that support Android for Work, will be enrolled as conventional Android devices
   - **Manage supported devices as Android for Work** - (Enabled) All devices that support Android for Work are enrolled as Android for Work devices. Any Android device that does not support Android for Work is enrolled as a conventional Android device.
   - **Manage supported devices for users only in these groups as Android for Work** - (Enabled for some groups only) Lets you target Android for Work management to a limited set of users. Only members of the selected groups who enroll a device that supports Android for Work are enrolled as Android for Work devices. All others are enrolled as Android devices.

 > [!NOTE]
 > A known issue prevents the **Manage supported devices for users only in these groups as Android for Work** option from working as expected. Users' devices in the specified Azure AD groups will enroll as Android instead of Android for Work. To enable Android for Work, you must use the **Manage all supported devices as Android for Work**.


Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

You'll see the account name and organization name in the Intune portal when the binding is complete; at that point, you can close both browsers.

### Enroll an Android for Work device
 How your end users enroll Android for Work devices is similar to enrollment for Android. Users can download and install the Company Portal app for Android on their mobile devices. The app prompts them to create a work profile as part of the enrollment process.  Once the work profile is created, users must switch to the managed version of the Company Portal. The managed Company Portal is tagged with a small orange briefcase in the bottom-right corner.

> [!div class="button"]
[< Previous step](create-service-connection-point.md)  [Next step >](set-up-additional-management.md)
