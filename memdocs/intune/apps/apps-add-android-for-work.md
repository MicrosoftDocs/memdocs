---
# required metadata

title: Add and assign Managed Google Play apps to Android Enterprise devices
titleSuffix: Microsoft Intune
description: Understand how to synchronize and assign apps to Android Enterprise devices from the Managed Google Play store.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/15/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 2f6c06bf-e29a-4715-937b-1d2c7cf663d4

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Android
- highpri
- FocusArea_Apps_Add
ms.custom: intune-classic
---

# Add Managed Google Play apps to Android Enterprise devices with Intune

Managed Google Play is Google's enterprise app store and sole source of applications for Android Enterprise in Intune. You can use Intune to orchestrate app deployment through Managed Google Play for any Android Enterprise scenario (including personally owned work profile, dedicated, fully managed, and corporate-owned work profile enrollments). How you add Managed Google Play apps to Intune differs from how Android apps are added for non-Android Enterprise scenarios. Store apps, line-of-business (LOB) apps, and web apps are added to Managed Google Play, and then synchronized into Intune so that they appear in the Client Apps list. Once they appear in the Client Apps list, you can manage assignment of any Managed Google Play app as you would any other app.

To make it easier for you to configure and use Android Enterprise management, upon connecting your Intune tenant to Managed Google Play, Intune automatically adds five common Android Enterprise related apps to the Intune admin center. The five apps are follow:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed scenarios. This app is automatically installed to fully managed devices during the device enrollment process.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - Helps you sign-in to your accounts if you use two-factor verification. This app is automatically installed to fully managed and corporate-owned work profile devices during the device enrollment process.

- **[Intune Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used for App Protection Policies (APP) and Android Enterprise personally owned work profile scenarios. This app is automatically installed to fully managed devices during the device enrollment process.
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** - Used for both Android Enterprise dedicated multi-app kiosk and fully managed user affiliated device scenarios. IT admins should create an assignment to install this app on dedicated devices that are going to be used in multi-app kiosk scenarios.
- **[Microsoft Launcher](https://play.google.com/store/apps/details?id=com.microsoft.launcher)** - Used for Android Enterprise fully managed scenarios. IT admins can create a policy to make the Microsoft Launcher the default launcher on fully managed devices and customize the home screen. For more information, see [Configure Microsoft Launcher](./configure-microsoft-launcher.md)

>[!NOTE]
>When an end user enrolls their Android Enterprise fully managed device, the Intune Company Portal app automatically installs on the device. The app icon might be visible to the end user. If the end user attempts to launch the Intune Company Portal app, the end user is redirected to the Microsoft Intune app, and the Company Portal app icon is subsequently hidden.
>Additionally, the Microsoft Intune and Authenticator apps won't be able to have an uninstall issued to them as they're crucial applications for multiple Android Enterprise enrollment scenarios.

## Before you start

- Make sure you have connected your Intune tenant to Managed Google Play. For more information, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- If you intend to enroll personally owned work profile devices, make sure you have configured Intune and Android personally owned work profiles to work together in the **Enrollment** workload of the portal. For more information, see [Enroll Android devices](../enrollment/android-work-profile-enroll.md).

>[!NOTE]
>When you work with Microsoft Intune, we recommend that you use either the Microsoft Edge or Google Chrome browser.

## Managed Google Play app types

There are three types of apps that are available with Managed Google Play:

- **Managed Google Play store app** - Public apps that are generally available in the Play Store. Manage these apps in Intune by browsing for the apps you want to manage, selecting them, and then synchronizing them into Intune.
- **Managed Google Play private app** - These are LOB apps published to Managed Google Play by Intune admins. These apps are private and are available only to your Intune tenant. This is how LOB apps are managed and deployed with Managed Google Play and Android Enterprise.
- **Managed Google Play web link** - Web links with IT admin-defined icons that are deployable to Android Enterprise devices. These links appear on devices in the device's app list just like regular apps.

## Managed Google Play store apps

> [!NOTE]
> Most newly created items in Intune take on the scope tags of the creator. This isn't the case for Managed Google Play Store apps. Admins can assign a scope tag to apply to all newly synced Managed Google Play apps on the Managed Google Play connector pane. For more information, see [Connect your Intune Account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
Browse and approve store apps in a view hosted within Intune. This view opens directly in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and doesn't require you to reauthenticate with a different account.

### Add a Managed Google Play store app directly in the Microsoft Intune admin center

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed.

    > [!NOTE]
    > You can create an app collection to organize apps and control the order that collections are displayed for your organization. For more information, see [Use Collections in Managed Google Play](../apps/apps-add-android-for-work.md#use-collections-in-managed-google-play).
    >
    > Your Intune tenant account must be connected to your Android Enterprise account to browse Managed Google Play store apps. For more information, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).

5. Select an app to view the app details.
6. Click **Select** to select the app.
7. Click **Sync** at the top of the blade to sync the app with the Managed Google Play service.
8. Click **Refresh** to update the app list and display the newly added app.

### Add a Managed Google Play store app in the Managed Google Play console (Alternative)

> [!IMPORTANT]
> This method is no longer supported and it’s required to add apps directly in the Microsoft Intune admin center. For more information, see [Support Tip: Intune moving to support new Google Play Android Management API](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-intune-moving-to-support-new-google-play-android/ba-p/3849875)
## Managed Google Play private (LOB) apps

There are two ways to add LOB apps to Managed Google Play:

1. Directly in the Microsoft Intune admin center - This allows you to add LOB apps by submitting just the app APK and a title, directly within Intune. This method doesn't require you to have a Google developer account and doesn't require you to pay the fee to register with Google as a developer. This method is simpler and has a significantly reduced number of steps, and makes LOB apps available for management in as little as ten minutes.
1. In the Google Play Developer Console - If you have a Google developer account or want to configure advanced distribution features that are only available in the Google Play Developer Console (like adding additional app screenshots), you can use the [Google Play Developer Console](https://play.google.com/apps/publish).

### Managed Google Play private (LOB) app publishing directly in the Microsoft Intune admin center

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed within Intune.
5. Select **Private apps** (next to the *lock* icon) in the Google Play window.
6. Click the **"+"** button at the lower right to add a new app.
7. Add an app **Title** and click **Upload APK** add the APK app package.
   > [!NOTE]
   > - Your app's package name must be globally unique in Google Play (not just unique within your enterprise or Google Play Developer account). Otherwise, you'll receive the **Upload a new APK file with a different package name** error.
   > - Your app's APK must not be marked as debuggable. Otherwise, you'll receive the **APK is marked as debuggable** error. 
8. Click **Create**.
1. Click **Select** for the private app you want to sync. 

1. Click **Sync** on the **App** pane to sync with the Managed Google Play service.

    > [!NOTE]
    > Private apps may take several minutes to become available to sync. If the app doesn't appear the first time you perform a sync, wait a couple minutes, click the **Select** button for the private app you want to sync, and then initiate a new sync.

For more information about Managed Google Play private apps including an FAQ, see Google's support article: [https://support.google.com/googleplay/work/answer/9146439](https://support.google.com/googleplay/work/answer/9146439)

>[!IMPORTANT]
>Private apps added using this method can never be made public. Only use this publishing option if you're sure that this app will always be private to your organization.

### Managed Google Play private (LOB) app publishing using the Google Developer Console

> [!IMPORTANT]
> Although this method is still supported, it’s recommended to publish apps directly in the Intune admin console. Apps published using the Google Developer Console will need to be selected and synced from the Intune admin console. 
1. Sign in to the [Google Play Developer Console](https://play.google.com/apps/publish) with the same account you used to configure the connection between Intune and Android Enterprise.
    > [!NOTE]
    > If you're signing in for the first time, you must register and pay a fee to become a member of the Google Developer program.
1. In the console, add new application. For details, see Google's support doc: [Publish Private apps](https://support.google.com/googleplay/android-developer/answer/9874937).
1. You upload and provide information about your app in the same way as you publish any app to the Google Play store. However, you must specifically add your organization using the Google Play Console. For details, see Google's support doc [Publish to your own organization](https://support.google.com/googleplay/android-developer/answer/9874937#zippy=%2Cpublish-to-your-own-organization).
    > [!NOTE]
    > Follow Google's support documentation to make the app available only to your organization. The app won't be available on the public Google Play store.
 For more information about uploading and publishing Android apps, see [Google Developer Console Help](https://support.google.com/googleplay/android-developer/answer/113469).
1. After you've published your app, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps** > **Add**. 
1. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**. 
1. Click **Select**. The **Managed Google Play** app store is displayed within Intune. 
1. Select **Private apps** (next to the *lock* icon) in the Google Play window. 
1. Click **Select** for the private app you want to sync.  
1. Click **Sync** on the **App** pane to sync with the Managed Google Play service. 

## Managed Google Play web links

Managed Google Play web links are installable and manageable just like other Android apps. When installed on a device, they will appear in the user's app list alongside the other apps they have installed. When selected, they will launch in the device's browser.

> [!NOTE]
> Web links pushed down from Managed Google Play won't open in the corporate context of Microsoft Edge if you have configured your Intune application protection policy setting **Receive data from other apps** to be **Policy managed apps**. When a web link is pushed down through Managed Google Play, it’s not recognized as a MAM-managed app, which is why Microsoft Edge will open in the personal context or InPrivate mode if the user isn't signed in with a personal account. For related information, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md).

Web links will open with Microsoft Edge or any other browser app you choose to deploy. Be sure to deploy at least one browser app to devices in order for web links to be able to open properly. However, all of the **Display** options available for web links (full screen, standalone, and minimal UI) will only work with the Chrome browser.

To create a Managed Google Play web link:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed within Intune.
5. Select **Web apps** (next to the *Globe* icon) in the Google Play window.
6. Click the **"+"** button at the lower right to add a new app.
7. Add an app **Title**, the web app **URL**, select how the app should be displayed, and select an app icon.
8. Click **Create**.
9. Close the Managed Google Play pane if you're done adding apps.
1. Click **Select** and **Sync** on the **App app** pane to sync with the Managed Google Play service.

    > [!NOTE]
    > Web apps may take several minutes to become available to sync. If the app doesn't appear the first time you perform a sync, wait a couple minutes, click the **Select** button for the web app you want to sync, and then initiate a new sync.

## Use collections in Managed Google Play

Collections are a way to group your Managed Google Play apps and determine the order they appear in the end users' Play Store.

To create a Managed Google Play collection:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed within Intune.
5. Select **Organize Apps** in the Google Play window.
6. Select **Create a collection**. A text box will appear to name the collection.
7. Enter a collection name and click **Next**.
   Check the approved MGP apps to add to the collection. If you need to approve additional apps for the collection, clicking the **Add apps** button will take you back to the Managed Google Play app store. Also, you can edit the order apps appear in the collection by clicking the arrows next to each app. You can also edit the order of the collections you've created by using the side arrow buttons. The order you set apps and collections in is the order the end user will see them in their Play Store app.
8. When you're done editing, click **save**. A popup box will appear asking you to confirm.
9. Click **save** on the popup box.

It may take some time after editing for the end user to see the changes made to their collections. If the changes haven't finished syncing yet, the end user may see an empty screen with **no results** text if they open the Play Store app. End users can still use the search bar to search for and download apps, even if the screen appears. Once at least one collection is created, all existing approved Managed Google Play apps that aren't in any other collection will appear in a default **My work app** collection. Apps approved after initial collection creation will have no collection assignment and won't be automatically added to the **My work app** collection.

Apps that aren't part of any collection won't appear on the end users' Play Store front page. However, the end user can still search for them and install in the Play Store. You can add the same Managed Google Play app to multiple collections. Each collection can contain up to 100 apps. For more information on collections, see [Google's documentation](https://support.google.com/googleplay/work/answer/9146438).

## Sync a Managed Google Play app with Intune

If you have approved an app from the store and don't see it in the **Apps** workload, force an immediate sync as follows:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps** > **Add**. 
1. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**. 
1. Click **Select**. The **Managed Google Play** app store is displayed within Intune. 
1. Click **Sync** on the **App** pane to sync with the Managed Google Play service. 

## Assign a Managed Google Play app to Android Enterprise personally owned and corporate-owned work profile devices

When the app is displayed in the **App licenses** node of the **Apps** workload pane, you can [assign it just as you would assign any other app](./apps-deploy.md) by assigning the app to groups of users.

After you assign the app, it is installed (or available for install) on the devices of the users that you've targeted. The user of the device isn't asked to approve the installation. For more information about Android Enterprise personally owned work profile devices, see [Set up enrollment of Android Enterprise personally owned work profile devices](../enrollment/android-work-profile-enroll.md).

On both work profile devices and corporate-owned devices, you can use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups. Additionally, you can use Intune to configure the app update priority on devices with a work profile. Also, you can use Intune to make required apps available for users through the Managed Google Play store. 

> [!NOTE]
> Only apps that have been assigned will show up in the Managed Google Play store for an end user. As such, this is a key step for the admin to take when setting up apps with Managed Google Play.

## Assign a Managed Google Play app to Android Enterprise fully managed devices

[Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md) are corporate-owned devices associated with a single user and used exclusively for work and not personal use. Users on fully managed devices can get their available company apps from the Managed Google Play app on their device.

By default, an Android Enterprise fully managed device won't allow employees to install any apps that aren't approved by the organization. Also, employees won't be able to remove any installed apps against policy. If you wish to allow users to access the full Google Play store to install apps rather than only having access to the approved apps in Managed Google Play store, you can set the **Allow access to all apps in Google Play store** to **Allow**. With this setting, the user can access all the apps in the Google Play store using their corporate account, however purchases may be limited. You can remove the limited purchases restriction by allowing users to add new accounts to the device. Doing so will enable end users to have the ability to purchase apps from the Google Play store using personal accounts, as well as conduct in-app purchases. For more information, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

> [!NOTE]
> The Microsoft Intune app, Microsoft Authenticator app, and the Company Portal app are installed as required apps on all fully managed and corporate-owned work profile devices during onboarding. Having these apps automatically installed provides Conditional Access support, and Microsoft Intune app users can see and resolve compliance issues.

## Update a Managed Google Play app

By default, Managed Google Play apps won't update unless the following conditions are met:

- The device is connected to Wi-Fi
- The device is charging
- The device isn't actively being used
- The app to be updated isn't running on the foreground

For more information, see the [Manage App Updates](https://support.google.com/googleplay/work/answer/9350374?hl=en) documentation from Google.

You can choose to configure the Wi-Fi requirement for dedicated, fully managed and corporate-owned work profile devices by configuring app auto-updates in [device configurations policies](../configuration/device-restrictions-android-for-work.md).

For dedicated, fully managed, corporate-owned, and personally owned work profile devices, you can choose an app update mode when an app is assigned to groups. The update modes available are:

- **Default**: The app's updates are subject to default conditions (described above).
- **High Priority**: The app will update as soon as possible from when a new update is released, disregarding all of the default conditions. This may be disruptive for some users since the update can occur while the device is being used.
- **Postponed**: When the app receives a new update, a 90-day waiting period is triggered. After 90 days, the app is updated to the newest version available, even if that version wasn't the update that triggered the waiting period. Note that the 90-day window isn't configurable. To terminate the waiting period early, change the update mode to either **Default** or **High Priority**.

To edit the app update mode:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**.
3. Select the app from the apps list.
4. Select **Properties**.
5. Select **Edit** by the **Assignments** section.
6. Find the group you'd like to edit the app update mode for by clicking the corresponding group mode for that group.
7. Under **app settings**, select the desired update mode.

## Manage Android Enterprise app permissions

Android Enterprise requires you to approve apps in the Managed Google Play web console before you sync them with Intune and assign them to your users. Because Android Enterprise allows you to silently and automatically push the apps to users' devices, you must accept the app permissions on behalf of all your users. Users don't see any app permissions when they install the apps, so it's important that you understand the permissions.

When an app developer updates permissions with a new version of the app, the permissions aren't automatically accepted even if you approved the previous permissions. Devices that run the previous version of the app can still use it. However, the app isn't upgraded until the new permissions are approved. Devices without the app installed don't install the app until you approve the app's new permissions.

### Update app permissions

Periodically visit the Managed Google Play console to check for new permissions. You can configure Google Play to send you or others an email when new permissions are required for an approved app. If you assign an app and observe that it isn't installed on devices, check for new permissions following these steps:

1. Go to [Google Play](https://play.google.com/work).
2. Sign in with the Google account that you used to publish and approve the apps.
3. Select the **Updates** tab, and check to see whether any apps require an update.
    Any listed apps require new permissions and aren't assigned until they're applied.

Alternatively, you can configure Google Play to automatically reapprove app permissions on a per-app basis.

## Additional Managed Google Play app reporting for Android Enterprise personally owned work profile devices

For Managed Google Play apps deployed to Android Enterprise personally owned work profile devices, you can view the status and version number of the app installed on a device using Intune.

## Working with Managed Google Play closed testing tracks

You can distribute a non-production version of a Managed Google Play app to devices enrolled in an Android Enterprise scenario (**Android Enterprise personally owned work profile (BYOD)**, **Android Enterprise fully managed (COBO)**, **Android Enterprise dedicated devices enrolled with Microsoft Entra shared mode (aka COSU)**, and **Android Enterprise corporate-owned work profile (COPE)**) in order to perform testing. In Intune, you can see whether an app has a pre-production build test track published to it, as well as be able to assign that track to Microsoft Entra user groups or device groups. The workflow for assigning a production version to a group that currently exists is the same as assigning a non-production channel. After deployment, the install status of each track will correspond with the track's version number in Managed Google Play. For more information, see [Google Play's closed test tracks for app pre-release testing](https://support.google.com/googleplay/android-developer/answer/3131213).

> [!NOTE]
> Required app deployments for non-production app tracks are currently unavailable for devices enrolled in Android Enterprise personally owned work profile (BYOD).
## Delete Managed Google Play apps

When necessary, you can delete Managed Google Play apps from Microsoft Intune. To delete a Managed Google Play app, open Microsoft Intune in the portal and select **Apps** > **All apps**. From the app list, select the ellipses (...) to the right of the Managed Google Play app, then select **Delete** from the displayed list.

> [!NOTE]
> If an app is unapproved or deleted from the managed Google Play store, it will not be removed from the Intune client apps list. This allows you to still target an uninstall policy to users even if the app is unapproved.
>
> To turn off Android Enterprise enrollment and management, see [Disconnect your Android Enterprise administrative account](../enrollment/connect-intune-android-enterprise.md#disconnect-your-android-enterprise-administrative-account).

## Android Enterprise system apps

You can enable an Android Enterprise system app for [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md) or [fully managed devices](../enrollment/android-fully-managed-enroll.md). For more information about adding an Android Enterprise system app, see [Add Android Enterprise system apps to Microsoft Intune](apps-ae-system.md).

<a name='mam-policies-with-ae-dedicated-devices-enrolled-with-azure-ad-shared-mode'></a>

## MAM policies with AE dedicated devices enrolled with Microsoft Entra shared mode

Intune-managed Android Enterprise dedicated devices enrolled with Microsoft Entra shared mode can receive MAM policies and can be targeted separately from other Android enterprise devices. Intune-managed Android Enterprise dedicated devices that aren't in Shared Device Mode will continue to be blocked from getting MAM. For more information about Intune-managed Android Enterprise dedicated devices enrolled with Microsoft Entra shared mode, see [Android Enterprise dedicated devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-dedicated-devices).

## Next steps

- [Assign apps to groups](apps-deploy.md)
