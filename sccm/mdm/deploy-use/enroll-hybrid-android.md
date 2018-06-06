---
title: Set up Android hybrid device management with Microsoft Intune
titleSuffix: Configuration Manager
description: Prepare to manage Android mobile devices with Configuration Manager and Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This article helps you enable hybrid enrollment of Android and Android for Work devices. You can then use Configuration Manger to manage the devices through a configured Microsoft Intune subscription. From Google Play, users can download the Android company portal app that lets them enroll Android (including Samsung KNOX Standard) and Android for Work devices.

With Configuration Manager you can manage compliance settings, wipe or delete Android devices, deploy apps, and collect software and hardware inventory. Without the Android Company Portal app installed on device, you don't have management capabilities like inventory and compliance settings, but you can still deploy apps to Android devices.  



## Enable Android enrollment  
The following steps let Configuration Manager manage Android devices without a work profile (that is, "classic Android" enrollment).

1. Before you can set up enrollment for any platform, finish the prerequisites and procedures in [Setup hybrid MDM](setup-hybrid-mdm.md).  
2. In the Configuration Manager console in the **Administration** workspace, choose **Overview** > **Cloud Services** > **Microsoft Intune Subscription** and choose your Intune subscription.  
3. On the **Home** tab in the **Subscription** group, choose **Configure Platforms** > **Android**.  
4. In the **Microsoft Intune Subscription Properties** dialog box, choose the **Android** tab and check the **Enable Android enrollment** box. You can choose to **Block personally owned devices** to limit enrollment to [predeclared devices](predeclare-devices-with-hardware-id.md).

 After you're set up, you need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](/intune/end-user-educate). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.



## Enable Android for Work enrollment
The following steps let Configuration Manager manage Android devices with a work profile.

1. [Create a Google account](https://accounts.google.com/SignUp) to use as your Android for Work admin account. Or, sign in with the account associated with all Android for Work management tasks for this Intune tenant. This account might be a Google account that's shared among the admins who manage Android devices. This account is the Google account that your organization uses to manage and publish apps in the Play for Work console. You use this account to approve apps in the Play for Work store, so keep track of the account name and password.
2. Enable Android enrollment by binding the Google account to the Intune tenant that's managed in Configuration Manager:
   1. In the Configuration Manager console in the **Administration** workspace, choose **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions** and choose your Intune subscription.
   2. On the **Home** tab in the **Subscription** group, choose **Configure Platforms** > **Android for Work**.
   3. In the dialog box, choose **Configure Android for Work in the Intune console**. The Intune console opens in your web browser.
   4. Use your Intune admin credentials to sign in to the Intune on Azure portal.
   5. Click **Managed Google Play**. 
       1. Select **I agree** to grant Microsoft permission to [send user and device information to Google](/intune/data-intune-sends-to-google).
       2. Select **Launch Google to connect now** to open Google Play's Android for Work website. The website opens on a new tab in your browser.
       3. On Google's sign-in page, enter the Google account from step 1.
       4. Provide your company's name for **Organization name**. For **Enterprise mobility management (EMM) provider**, "Microsoft Intune" should be displayed. 
       5. Agree to the Android for Work agreement, and then choose **Confirm**. Your request will be processed.

   6. On Google's sign-in page, enter the Google account credentials from step 1, and then provide your company information.
3. When you return to the Intune on Azure portal, go to the **Android for Work** enrollment blade, and click **Work profiles**. Android for Work is now enabled. You have two enrollment options for Android for Work devices:
   - **Manage all devices as Android** (disabled). All Android devices, including devices that support Android for Work, are enrolled as conventional Android devices.
   - **Manage supported devices as Android for Work** (enabled). All devices that support Android for Work are enrolled as Android for Work devices. Any Android device that doesn't support Android for Work is enrolled as a conventional Android device.

> [!NOTE]
> A known issue prevents the **Manage supported devices for users only in these groups as Android for Work** option from working as expected. Users' devices in the specified Azure AD groups enroll as Android instead of Android for Work. To enable Android for Work, you must use the **Manage supported devices as Android for Work** option.


After you're set up, tell your users how to enroll their devices. See [What to tell users about enrolling their devices](/intune/end-user-educate). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

When the binding finishes, you see the account name and organization name in the Intune on Azure portal. At that time, you can close both browsers.

### Enroll an Android for Work device
How your users enroll Android for Work devices is similar to enrollment for Android. Users can download and install the Company Portal app for Android on their mobile devices. The app prompts them to create a work profile as part of the enrollment process. After the work profile is created, users must switch to the managed version of the Company Portal. The managed Company Portal is tagged with a small orange briefcase in the lower-right corner.

### Manage Android for Work devices
After you enable Android for Work enrollment, you can perform the following management tasks for Android for Work devices:
- [Approve apps](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Create configuration items](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Manage compliance settings](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Manage email profiles](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Selectively wipe the work profile](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Previous step](create-service-connection-point.md)  [Next step >](set-up-additional-management.md)
