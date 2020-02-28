---
# required metadata

title: Assign Managed Google Play apps to Android Enterprise devices
titleSuffix: Microsoft Intune
description: Understand how to synchronize and assign apps to Android Enterprise devices from the Managed Google Play store.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 2f6c06bf-e29a-4715-937b-1d2c7cf663d4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Add Managed Google Play apps to Android Enterprise devices with Intune

Managed Google Play is Google's enterprise app store and sole source of applications for Android Enterprise. You can use Intune to orchestrate app deployment through Managed Google Play for any Android Enterprise scenario (including work profile, dedicated, and fully managed enrollments). How you add Managed Google Play apps to Intune differs from how Android apps are added for non-Android Enterprise. Store apps, line-of-business (LOB) apps, and web apps are approved in or added to Managed Google Play, and then synchronized into Intune so that they appear in the Client Apps list. Once they appear in the Client Apps list list, you can manage assignment of any Managed Google Play app as you would any other app.

To make it easier for you to configure and use Android Enterprise management, upon connecting your Intune tenant to Managed Google Play, Intune will automatically add four common Android Enterprise related apps to the Intune admin console. The four apps are the following:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed scenarios. This app is automatically installed to fully managed devices during the device enrollment process.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - Helps you sign-in to your accounts if you use two-factor verification. This app is automatically installed to fully managed devices during the device enrollment process.
- **[Intune Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used for App Protection Policies (APP) and Android Enterprise work profile scenarios.
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** - Used for Android Enterprise dedicated multi-app kiosk scenarios. IT admins should create an assignment to install this app on dedicated devices that are going to be used in multi-app kiosk scenarios.

>[!NOTE]
>When an end user enrolls their Android Enterprise fully managed device, the Intune Company Portal app is automatically installed and the application icon may be visible to the end user. If the end user attempts to launch the Intune Company Portal app, the end user will be redirected to the Microsoft Intune app and the Company Portal app icon will be subsequently hidden.

## Before you start
- Make sure you have connected your Intune tenant to Managed Google Play.  For more information, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).
- If you intend to enroll work profile devices, make sure you have configured Intune and Android work profiles to work together in the **Device enrollment** workload of the Azure portal. For more information, see [Enroll Android devices](../enrollment/android-work-profile-enroll.md).

>[!NOTE]
>When you work with Microsoft Intune, we recommend that you use either the Microsoft Edge or Google Chrome browser.

## Managed Google Play app types
There are three types of apps that are available with Managed Google Play:

- **Managed Google Play store app** - Public apps that are generally available in the Play Store. Manage these apps in Intune by browsing for the apps you want to manage, approving them, and then synchronizing them into Intune.
- **Managed Google Play private app** - These are LOB apps published to Managed Google Play by Intune admins.  These apps are private and are available only to your Intune tenant. This is how LOB apps are managed and deployed with Managed Google Play and Android Enterprise.
- **Managed Google Play web link** - Web links with IT admin-defined icons that are deployable to Android Enterprise devices. These appear on devices in the device's app list just like regular apps.

## Managed Google Play store apps
There are two ways to browse and approve Managed Google Play store apps with Intune:

1. Directly in the Intune console - browse and approve store apps in a view hosted within Intune. This opens directly in the Intune console and does not require you to reauthenticate with a different account.
1. In Managed Google Play console - you can optionally open the Managed Google Play console directly and approve apps there. See [Sync a Managed Google Play app with Intune](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune) for more information.  This requires a separate login using the account you used to connect your Intune tenant to Managed Google Play.

### Add a Managed Google Play store app directly in the Intune console

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed.

    > [!NOTE]
    > Your Intune tenant account must be connected to your Android Enterprise account to browse managed Google Play store apps. For more information, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).

5. Select an app to view the app details.
6. On the page that displays the app, click **Approve**. A window for the app opens asking you to give permissions for the app to perform various operations.
7. Select **Approve** to accept the app permissions and continue.
8. Select **Keep approved when app requests new permissions** in the **Approval Settings** tab and then click **Done**. 

    > [!IMPORTANT]
    > If you do not choose this option, you will need to manually approve any new permissions if the app developer publishes an update. This will cause installations and updates of the app to stop until permissions are approved. For this reason, it is recommended to select the option to automatically approve new permissions. 

9. Click **Select** to select the app.
10. Click **Sync** at the top of the blade to sync the app with the Managed Google Play service.
11. Click **Refresh** to update the app list and display the newly added app.

### Add a Managed Google Play store app in the Managed Google Play console (Alternative)
If you prefer to synchronize a Managed Google Play app with Intune rather than adding it directly using Intune, use the following steps.

> [!IMPORTANT]
> The information provided below is an alternative method to adding a Managed Google Play app using Intune as described above.

1. Go to the [Managed Google Play store](https://play.google.com/work). Sign in with the same account you used to configure the connection between Intune and Android Enterprise.
2. Search the store and select the app you want to assign by using Intune.
3. On the page that displays the app, click **Approve**.  
    In the following example, the Microsoft Excel app has been chosen.

    ![The Approve button in the Managed Google Play store](./media/apps-add-android-for-work/approve.png)

   A window for the app opens asking you to give permissions for the app to perform various operations.

4. Select **Approve** to accept the app permissions and continue.

    ![The Approve button for app permissions](./media/apps-add-android-for-work/approve-app-permissions.png)

5. Select an option for handling new app permission requests, and then select **Save**.

    ![Options for handling new app permission requests](./media/apps-add-android-for-work/approve-app-settings.png)

    The app is approved, and it is displayed in your IT admin console. Next, you can [Sync the Android work profile app with Intune](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune).

## Managed Google Play private (LOB) apps

There are two ways to add LOB apps to Managed Google Play:

1. Directly in the Intune console - This allows you to add LOB apps by submitting just the app APK and a title, directly within Intune. This method does not require you to have a Google developer account and does not require you to pay the fee to register with Google as a developer.  This method is simpler and has a significantly reduced number of steps, and makes LOB apps available for management in as little as ten minutes.
1. In the Google Play Developer Console - If you have a Google developer account or want to configure advanced distribution features that are only available in the Google Play Developer Console (like adding additional app screenshots), you can use the [Google Play Developer Console](https://play.google.com/apps/publish). 

### Managed Google Play private (LOB) app publishing directly in the Intune console

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed within Intune.
5. Select **Private apps** (next to the *lock* icon) in the Google Play window. 
6. Click the **"+"** button at the lower right to add a new app.
7. Add an app **Title** and click **Upload APK** add the APK app package.
8. Click **Create**.
9. Close the Managed Google Play pane if you are done adding apps.
10. Click **Sync** on the **App app** pane to sync with the Managed Google Play service. 

    > [!NOTE]
    > Private apps may take several minutes to become available to sync. If the app does not appear the first time you perform a sync, wait a couple minutes and initiate a new sync.

For more information about Managed Google Play private apps including a FAQ, see Google's support article: https://support.google.com/googleplay/work/answer/9146439

>[!IMPORTANT]
>Private apps added using this method can never be made public. Only use this publishing option if you are sure that this app will always be private to your organization.

### Managed Google Play private (LOB) app publishing using the Google Developer Console

1. Sign in to the [Google Play Developer Console](https://play.google.com/apps/publish) with the same account you used to configure the connection between Intune and Android Enterprise.  
    If you are signing in for the first time, you must register and pay a fee to become a member of the Google Developer program.
2. In the console, select **Add new application**.
3. You upload and provide information about your app in the same way as you publish any app to the Google Play store. However, you must select **Only make this application available to my organization (<*organization name*>)**.

    ![Make the app available only to your organization](./media/apps-add-android-for-work/restrict.png)

    This operation makes the app available only to your organization. It won't be available on the public Google Play store.

    For more information about uploading and publishing Android apps, see [Google Developer Console Help](https://support.google.com/googleplay/android-developer/answer/113469).
4. After you've published your app, sign in to the [Managed Google Play store](https://play.google.com/work) with the same account that you used to configure the connection between Intune and Android Enterprise.
5. In the **Apps** node of the store, verify that the app you've published is displayed.  
    The app is automatically approved to be synchronized with Intune.

## Managed Google Play web links

Managed Google Play web links are installable and manageable just like other Android apps. When installed on a device, they will appear in the user's app list alongside the other apps they have installed. When tapped, they will launch in the device's browser.

Web links will open with Microsoft Edge or any other browser app you choose to deploy. Be sure to deploy at least one browser app to devices in order for web links to be able to open properly. However, all of the **Display** options available for web links (full screen, standalone, and minimal UI) will only work with the Chrome browser. 

> [!IMPORTANT]
> As of publication of this doc, there is a known Google bug that prevents web links from opening on devices with browsers other than Chrome. Google has committed to fixing this bug.  This notice will be removed when Microsoft has confirmation that Google has published their fix.

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Managed Google Play app**.
4. Click **Select**. The **Managed Google Play** app store is displayed within Intune.
5. Select **Web apps** (next to the *Globe* icon) in the Google Play window.
6. Click the **"+"** button at the lower right to add a new app.
7. Add an app **Title**, the web app **URL**, select how the app should be displayed, and select an app icon.
8. Click **Create**.
9. Close the Managed Google Play pane if you are done adding apps.
10. Click **Sync** on the **App app** pane to sync with the Managed Google Play service. 

    > [!NOTE]
    > Web apps may take several minutes to become available to sync. If the app does not appear the first time you perform a sync, wait a couple minutes and initiate a new sync.

## Sync a Managed Google Play app with Intune

If you have approved an app from the store and don't see it in the **Apps** workload, force an immediate sync as follows:

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Apps** > **Tenant administration** > **Connectors and tokens** > **Managed Google Play**.
5. In the **Managed Google Play** pane, choose **Refresh**.  
    The page updates the time and status of the last sync.
6. In the Microsoft Endpoint Manager admin center select  **Apps** > **All apps**.  
    The newly available Managed Google Play app is displayed.

## Assigning a Managed Google Play app to Android Enterprise work profile devices

When the app is displayed in the **App licenses** node of the **Apps** workload pane, you can [assign it just as you would assign any other app](/intune-azure/manage-apps/deploy-apps) by assigning the app to groups of users.

After you assign the app, it is installed (or available for install) on the devices of the users that you've targeted. The user of the device is not asked to approve the installation. For more information about Android Enterprise work profile devices, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md). 

> [!NOTE] 
> Only apps that have been assigned will show up in the Managed Google Play store for an end user. As such, this is a key step for the admin to take when setting up apps with Managed Google Play.

## Assigning a Managed Google Play app to Android Enterprise fully managed devices

[Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md) are corporate-owned devices associated with a single user and used exclusively for work and not personal use. Users on fully managed devices can get their available company apps from the managed Google Play app on their device.

By default, an Android Enterprise fully managed device will not allow employees to install any apps that are not approved by the organization. Also, employees will not be able to remove any installed apps against policy. If you wish to allow users to access the full Google Play store to install apps rather than only having access to the approved apps in Managed Google Play store, you can set the **Allow access to all apps in Google Play store** to **Allow**. With this setting, the user can access all the apps in the Google Play store using their corporate account, however purchases may limited. You can remove the limited purchases restriction by allowing users to add new accounts to the device. Doing so will enable end users to have the ability to purchase apps from the Google Play store using personal accounts, as well as conduct in-app purchases. For more information, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md). 

> [!NOTE]
> The Microsoft Intune app and the Microsoft Authenticator app will be installed as required apps onto all fully managed devices during onboarding. Having these apps automatically installed provides Conditional Access support, and Microsoft Intune app users can see and resolve compliance issues. 

## Manage Android Enterprise app permissions
Android Enterprise requires you to approve apps in the managed Google Play web console before you sync them with Intune and assign them to your users. Because Android Enterprise allows you to silently and automatically push the apps to users' devices, you must accept the app permissions on behalf of all your users. Users don't see any app permissions when they install the apps, so it's important that you understand the permissions.

When an app developer updates permissions with a new version of the app, the permissions are not automatically accepted even if you approved the previous permissions. Devices that run the previous version of the app can still use it. However, the app is not upgraded until the new permissions are approved. Devices without the app installed do not install the app until you approve the app's new permissions. 

### Update app permissions

Periodically visit the managed Google Play console to check for new permissions. You can configure Google Play to send you or others an email when new permissions are required for an approved app. If you assign an app and observe that it isn't installed on devices, check for new permissions following these steps:

1. Go to [Google Play](https://play.google.com/work).
2. Sign in with the Google account that you used to publish and approve the apps.
3. Select the **Updates** tab, and check to see whether any apps require an update.  
    Any listed apps require new permissions and are not assigned until they are applied.

Alternatively, you can configure Google Play to automatically reapprove app permissions on a per-app basis.

## Additional Managed Google Play app reporting for Android Enterprise work profile devices

For Managed Google Play apps deployed to Android Enterprise work profile devices, you can view the status and version number of the app installed on a device using Intune. 

## Delete Managed Google Play apps
When necessary, you can delete managed Google Play apps from Microsoft Intune. To delete a managed Google Play app, open Microsoft Intune in the Azure portal and select **Apps** > **All apps**. From the app list, select the ellipses (...) to the right of the managed Google Play app, then select **Delete** from the displayed list. When you delete a managed Google Play app from the app list, the managed Google Play app is automatically unapproved.

## Android Enterprise system apps

You can enable an Android Enterprise system app for [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md) or [fully managed devices](../enrollment/android-fully-managed-enroll.md). For more information about adding an Android Enterprise system app, see [Add Android Enterprise system apps to Microsoft Intune](apps-ae-system.md).

## Next steps

- [Assign apps to groups](apps-deploy.md)
