---
title: Device restriction settings for Android in Microsoft Intune
description: On Android Enterprise or Android for Work devices owned by your organization, you can restrict settings on the device using Microsoft Intune. Allow copy and paste, notifications, app permissions, data sharing, password length, sign in failures, use fingerprint to unlock, reuse passwords, and enable bluetooth sharing of work contacts. Configure devices as a dedicated device kiosk to run one app, or multiple apps.
author: MandiOhlinger
ms.author: mandia
ms.date: 09/17/2025
ms.topic: reference
params:
  siblings_only: true
ms.reviewer: cchristenson, arnab
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# Android template device settings list to restrict features using Intune

You can use a Microsoft Intune device restrictions profile to manage device features and settings on your Android Enterprise and AOSP devices.

This article lists and describes the settings you can configure on Android devices using the Intune templates. As part of your mobile device management (MDM) solution, use these settings to create password restrictions, enable Bluetooth, manage system updates, create a kiosk experience, and more.

This article applies to:

- Android Enterprise corporate-owned work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise personally owned devices with a work profile (BYOD)
- Android Open Source Project (AOSP) corporate-owned userless devices (shared)
- Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

## Before you begin

- Create a [device restrictions profile](device-restrictions-configure.md) in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). When you create the profile, select the following options:

  - **Platform**: Select **Android Enterprise** or **Android (AOSP)**.
  - **Profile type**: Select **Templates**.

  For the steps, go to [Create a device restriction profile in Microsoft Intune](device-restrictions-configure.md).

- Settings can be configured using **templates** (this article) or the **[settings catalog](settings-catalog.md)**. This article focuses on the template. For more information on **settings catalog**, go to:

  - [Use the settings catalog to configure Intune settings](settings-catalog.md)
  - [Android Enterprise device settings list in the Intune settings catalog](settings-catalog-android.md)

  > [!TIP]
  >- If you can't find a setting in **templates**, select **settings catalog**. The settings catalog is a list of the settings you can configure for corporate-owned Android Enterprise devices. It can include other settings that aren't available in **templates**.
  >- If you can't find a setting in **settings catalog**, check **templates**.

- To learn more about the Android enrollment options, see [Enrollment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

## Android settings

This section lists the template settings you can configure on Android Enterprise (corporate-owned and personally owned) and AOSP devices.

# [Corporate-owned](#tab/aecorporate)

These settings apply to the following Android Enterprise enrollment types where Intune controls the entire device:

- Fully managed devices
- Dedicated devices
- Corporate-owned devices with a work profile

Some settings aren't supported by all enrollment types. The [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) shows the enrollment types that the settings apply to.

:::image type="content" source="./media/device-restrictions-android-for-work/setting-headers.png" alt-text="Screenshot that shows the Android Enterprise Users and Accounts setting headers and the enrollment types they apply to in Microsoft Intune.":::

For corporate-owned devices with a work profile, some settings only apply in the work profile. These settings have **(work profile-level)** in the setting name. For fully managed and dedicated devices, these settings apply device-wide.

:::image type="content" source="./media/device-restrictions-android-for-work/work-profile-level.png" alt-text="Screenshot that shows the Android Enterprise application settings that apply at the corporate-owned work profile level in Microsoft Intune.":::

## General

### Fully managed, dedicated, and corporate-owned work profile devices

- **Screen capture (work profile-level)**: **Block**:
  - Prevents screenshots or screen captures on the device.
  - Prevents the content from being shown on display devices that don't have a secure video output.
  - Prevents apps from using the system screenshot capabilities.
  - Affects screen sharing.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image.

- **Camera (work profile-level)**: **Block** prevents access to the camera on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

- **Default permission policy (work profile-level)**: This setting defines the default permission policy for requests for runtime permissions. Your options
  - **Device default** (default): Use the device's default setting.
  - **Prompt**: Users are prompted to approve the permission.
  - **Auto grant**: Permissions are automatically granted.
  - **Auto deny**: Permissions are automatically denied.
- **Date and Time changes**: **Block** prevents users from manually setting the date and time. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to the set date and time on the device.
- **Roaming data services**: **Block** prevents data roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow data roaming when the device is on a cellular network.
- **Wi-Fi access point configuration**: **Block** prevents users from creating or changing any Wi-Fi configurations. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.
- **Bluetooth configuration**: **Block** prevents users from configuring Bluetooth on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using Bluetooth on the device.
- **Tethering and access to hotspots**: **Block** prevents tethering and access to portable hotspots. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow tethering and access to portable hotspots.
- **USB file transfer**: **Block** prevents transferring files over USB. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow transferring files.

  > [!TIP]
  > The Intune settings catalog > **USB access** setting has more options that you can configure and manage. To learn more, see [Android Intune settings catalog settings list](settings-catalog-android.md#general).

- **External media**: **Block** prevents using or connecting any external media on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow external media on the device.
- **Beam data using NFC (work-profile level)**: **Block** prevents using the Near Field Communication (NFC) technology to beam data from apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using NFC to share data between devices.
- **Developer settings**: Choose **Allow** to let users access developer settings on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from accessing developer settings on the device.
- **Microphone adjustment**: **Block** prevents users from unmuting the microphone and adjusting the microphone volume. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use and adjust the volume of the microphone on the device.
- **Factory reset protection emails**: Choose **Google account email addresses**. Enter the email addresses of device administrators that can unlock the device after the device is wiped. Be sure to separate the email addresses with a semi-colon, such as `admin1@gmail.com;admin2@gmail.com`. These emails only apply when a non-user factory reset is run, such as running a factory reset using the recovery menu.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  Factory reset protection (FRP) helps prevent unauthorized access to your device after it's been factory reset. If the device is reset without your permission, in some situations, only the email addresses you enter can unlock the device. When the **Factory reset protection emails** setting is configured, there is different factory reset protection (FRP) behavior:

  | Enrollment method | Settings > Factory data reset | Settings > Recovery/bootloader | Intune [wipe](../remote-actions/device-wipe.md) |
  | --- | --- | --- | --- |
  | **Corporate-owned devices with work profile** (COPE) | ✅ factory reset protection | ✅ factory reset protection | ❌ no factory reset protection |
  | **Fully managed** (COBO) | ❌ no factory reset protection | ✅ factory reset protection | ❌ no factory reset protection |
  | **Dedicate** (COSU) | ❌ no factory reset protection | ✅ factory reset protection | ❌ no factory reset protection |

  For background and guidance, see **[Factory reset protection (FRP) enforcement behavior for Android Enterprise](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced)**.

- **System update**: Choose an option to define how the device handles over-the-air updates. Your options
  - **Device Default** (default): Use the device's default setting. By default, if the device is connected to Wi-Fi, is charging, and is idle, then the OS updates automatically. For app updates, the OS also validates if the app isn't running in the foreground.
  - **Automatic**: Updates are automatically installed without user interaction. Setting this policy immediately installs any pending updates.
  - **Postponed**: Updates are postponed for 30 days. At the end of the 30 days, Android prompts users to install the update. It's possible for device manufacturers or carriers to prevent (exempt) important security updates from being postponed. An exempted update shows a system notification to users on the device.
  - **Maintenance window**: Installs updates automatically during a daily maintenance window that you set in Intune. Installation tries daily for 30 days, and can fail if there's insufficient space or battery levels. After 30 days, Android prompts users to install.

    This setting applies to operating system and Play Store app updates. Any maintenance window takes precedence over in-progress device changes.

    Use this option for dedicated devices, such as kiosks, as single-app dedicated device foreground apps can be updated.

- **Freeze periods for system updates**: Optional. When you set the **System update** setting to **Automatic**, **Postponed**, or **Maintenance window**, use this setting to create a freeze period:

  - **Start date**: Enter the start date in `MM/DD` format, up to 90 days long. For example, enter `11/15` to start the freeze period on November 15.
  - **End date**: Enter the end date in `MM/DD` format, up to 90 days long. For example, enter `01/15` to end the freeze period on January 15.

  During this freeze period, all incoming system updates and security patches are blocked, including manually checking for updates.

  When a device's clock is outside the freeze period, the device continues to receive updates based on your **System update** setting.

  To set multiple annually recurring freeze periods, make sure the freeze periods are separated by at least 60 days.

  This setting applies to:

  - Android 9.0 and newer

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action that admins use. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

  This setting applies to:

  - Fully managed devices running any Android version
  - Corporate owned devices with a work profile running Android 10 or older

### Fully managed and dedicated devices

- **Volume changes**: **Block** prevents users from changing the device's volume, and also mutes the main volume. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the volume settings on the device.
- **Factory reset**: **Block** prevents users from using the factory reset option in the device's settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use this setting on the device.

  For background and guidance on this feature, see [Factory reset protection (FRP) enforcement behavior for Android Enterprise](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced).

- **Status bar**: **Block** prevents access to the status bar, including notifications and quick settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users access to the status bar.
- **Wi-Fi setting changes**: **Block** prevents users from changing Wi-Fi settings created by the device owner. Users can create their own Wi-Fi configurations. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.
- **USB storage**: Choose **Allow** to access USB storage on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent access to USB storage.
- **Network escape hatch**: **Enable** allows users to turn on the network escape hatch feature. If a network connection isn't made when the device boots, then the escape hatch asks to temporarily connect to a network and refresh the device policy. After you apply the policy, the temporary network is forgotten and the device continues booting. This feature connects devices to a network if:

  - There isn't a suitable network in the last policy.
  - The device boots into an app in lock task mode.
  - Users are unable to reach the device settings.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from turning on the network escape hatch feature on the device.

- **Notification windows**: When set to **Disable**, window notifications, including toasts, incoming calls, outgoing calls, system alerts, and system errors aren't shown on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show notifications.

  > [!NOTE]
  > If **Notification windows** is set to **Disable**, any configuration that depends on the Overlay permission will not function as expected. This includes features such as the virtual home button, screen saver and automatic sign-out on Managed Home Screen.

- **Skip first use hints**: **Enable** hides or skips suggestions from apps that step through tutorials, or hints when the app starts. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show these suggestions when the app starts.

### Fully managed and corporate-owned work profile devices

- **Locate device**: **Allow** lets admins locate lost or stolen devices using a remote action. When set to **Allow**, end users receive a one-time notification stating that Intune has location permissions. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow locating devices using geolocation.

### Fully managed and Dedicated devices (kiosk mode only)

- **Power button menu**: **Block** hides the power options when users hold down the power button when in kiosk mode. Hiding these options prevents users from accidentally or intentionally shutting down devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, when users hold down the power button on a device, they're shown power options, such as Restart and Power off.

  This setting applies to:

  - Android 9.0 and newer

- **System error warnings**: **Allow** shows system warnings on the screen when in kiosk mode, including unresponsive apps and system warnings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might hide these warnings. When one of these events occurs, the system forces the app to close.

  This setting applies to:

  - Android 9.0 and newer

- **Enabled system navigation features**: Allow users to access the device home and overview buttons when in kiosk mode. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might disable the device home and overview buttons.
  - **Home button only**: Users can see and select the home button. They can't see or select the overview buttons.
  - **Home and overview buttons**: Users can see and select the home and overview buttons.

    When a device is enrolled and using the Managed Home Screen app, enabling the **Overview** button allows end users to skip or ignore the sign in and session PIN screens. The screens are still shown, but users can ignore them, and aren't required to enter anything.

  This setting applies to:

  - Android 9.0 and newer

- **System notifications and information**: Allow users to access the device status bar, and receive notifications from the status bar when in kiosk mode. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might disable the status bar, and disable notifications on the status bar.
  - **Show system information in device's status bar**: Users can see system information on the status bar. Users can't see or receive notifications from the status bar.
  - **Show system notifications and information in device's status bar**: Users can see the system information, and receive notifications from the status bar. To see notifications, enable the device home button using the **Enabled system navigation features** setting.

    On kiosk devices, if you don't want notification sounds or vibration, then don't enable this setting. If you want notification sounds or vibration, then enable this setting.

    When a device is enrolled and using the Managed Home Screen app, enabling **System notifications** allows end users to skip or ignore the sign in and session PIN screens. The screens are still shown, but users can ignore them, and aren't required to enter anything.

  This setting applies to:

  - Android 9.0 and newer

- **End-user access to device settings**: **Block** prevents users from accessing the Settings app and prevents other apps in kiosk mode from opening the Settings app. If the device is a kiosk, then set this setting to **Block**.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access the Settings and allow apps in Kiosk mode to open the Settings app.

  This setting applies to:

  - Android 9.0 and newer

### Dedicated devices

- **Locate device**: **Block** prevents admins from locating lost or stolen devices using a remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow locating devices using geolocation.

### Corporate-owned work profile devices

- **Contact sharing via Bluetooth (work profile-level)**: **Block** prevents users from sharing their work profile contacts with devices over Bluetooth. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to share their contacts via Bluetooth.

- **Search work contacts and display work contact caller-id in personal profile**: In the personal profile, **Block** prevents users from searching work contacts, and showing work caller ID information.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow searching work contacts, and show work caller IDs.

  [ShowWorkContactsInPersonalProfile](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#showworkcontactsinpersonalprofile)

- **Copy and paste between work and personal profiles**: **Allow** lets users copy and paste data between the work and personal profiles.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might:

  - Prevent users from pasting text from the work profile into the personal profile.
  - Allow users to copy text from the personal profile, and paste into the work profile.
  - Allow users to copy text from the work profile, and paste into the work profile.

  [CrossProfileCopyPaste](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#crossprofilecopypaste)

- **Data sharing between work and personal profiles**: Choose if data can be shared between work and personal profiles. Your options:

  - **Device default**: Intune doesn't change or update this setting. By default, the OS might prevent users from sharing data in the work profile with the personal profile. Data in the personal profile can be shared in the work profile.
  - **Block all sharing between profiles**: Prevents users from sharing data between the work and personal profiles.
  - **Block sharing from work to personal profile**: Prevents users from sharing data in the work profile with the personal profile. Data in the personal profile can be shared with the work profile.
  - **No restrictions on sharing**: Data can be shared between the work and personal profiles.

  [CrossProfileDataSharing](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#crossprofiledatasharing)

## System security

- **Threat scan on apps**: **Require** (default) enables Google Play Protect to scan apps before and after they're installed. If it detects a threat, it might warn users to remove the app from the device. When set to **Not configured**, Intune doesn't change or update this setting. By default, the OS might not enable or run Google Play Protect to scan apps.

- **Common Criteria mode**: **Require** enables an elevated set of security standards that are most often used in highly sensitive organizations, such as government establishments. Those settings include but aren't limited to:

  - AES-GCM encryption of Bluetooth Long Term Keys
  - Wi-Fi configuration stores
  - Blocks bootloader download mode, the manual method for software updates
  - Mandates additional key zeroization on key deletion
  - Prevents non-authenticated Bluetooth connections
  - Requires that FOTA updates have 2048-bit RSA-PSS signature

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  Learn more about Common Criteria:
  - [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org) at commoncriteriaportal.org
  - [CommonCriteriaMode](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#commoncriteriamode) in the Android Management API documentation.
  - [Knox Deep Dive: Common Criteria Mode](https://www.samsungknox.com/blog/knox-deep-dive-common-criteria-mode) at samsungknox.com

## Device experience

Use these settings to configure a kiosk-style experience on your dedicated or fully managed devices, or to customize the home screen experiences on your fully managed devices. If you're not sure which experience to configure, the [Selecting a home screen experience for your Android Enterprise corporate-owned devices](https://techcommunity.microsoft.com/blog/intunecustomersuccess/selecting-a-home-screen-experience-for-your-android-enterprise-corporate-owned-d/4224924) blog can help.

**Device experience type**: Select a device experience type to start configuring Microsoft Launcher or the Microsoft Managed Home Screen on your devices. Your options:

- **Not configured**: Intune doesn't change or update this setting. By default, users might see the device's default home screen experience.
- **Kiosk mode (dedicated and fully managed)**: Configure a kiosk-style experience on your dedicated and fully managed devices. You can configure devices to run one app, or run many apps. When a device is set with kiosk mode, only the apps you add are available. Before you configure these settings, be sure to [add](../apps/apps-add-android-for-work.md), and [assign](../apps/apps-deploy.md) the apps you want on the devices.

  When you use kiosk mode (single-app or multi-app), by default, the platform disables familiar user interfaces and workflows. Some of these features can be re-enabled on OS 9 and newer. For example, when a device is operating in a kiosk state, the system changes some behaviors, including:

  - The device's status bar is removed from view. System information and notifications are hidden from end users.
  - Device navigation buttons, like the home and overview buttons, are disabled and removed from view.
  - The device's lock screen, like the keyguard, is disabled.

    To use dialer & phone applications, or for your users to receive push notifications in kiosk mode, use the [Fully managed and Dedicated devices (kiosk mode only](#dedicated-devices) > **Enabled system navigation features** (with **Home button** options) and **System notifications and information** settings (in this article). These features are available on Android devices running 9.0 and newer.

    On OS 9 and newer, the [Device password](#device-password) > **Disable lock screen** (in this article) setting manages the device's lock screen behavior.

  > [!NOTE]
  > Kiosk mode doesn't prevent the kiosk application from being able to launch other applications that are installed on the device, including the device's **Settings** app. Admins should ensure that all applications enabled in kiosk mode don't launch other apps that users shouldn't access. And, uninstall any apps that aren't necessary on the device.

  - **Kiosk mode**: Your options:

    - **Not configured**: Intune doesn't change or update this setting.
    - **Single app**: Select this option to run one app. When users are on the devices, they can only access the app you selected. When the device starts, only the specific app starts. Users are restricted from changing the running app.

      **Select an app to use for kiosk mode**: Select the Managed Google Play or Android Enterprise system app from the list. For single-app dedicated and fully managed devices, the app you select **must be**:

      - [Added in Intune](../apps/apps-add-android-for-work.md).
      - [Assigned to the device group](../apps/apps-deploy.md) created for your dedicated or fully managed devices.

        > [!NOTE]
        > On fully managed devices, the only selected app that applies is the Managed Home Screen. All other apps are treated as a required app.

    - **Multi-app**: Select this option to run many apps. Users can access a limited set of apps on the device. When the device starts, only the apps you add start. You can also add some web links that users can open. When the policy is applied, users see icons for the allowed apps on the home screen.

      For multi-app dedicated and fully managed devices, the **Managed Home Screen** app isn't required to be in the configuration profile, but the [Managed Home Screen app](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) from Google Play **must be**:

      - [Added in Intune](../apps/apps-add-android-for-work.md).
      - [Assigned to the device group](../apps/apps-deploy.md) created for your dedicated or fully managed devices.

      Also, any packages you want launchable from Managed Home Screen **must be**:

      - [Added in Intune](../apps/apps-add-android-for-work.md).
      - [Assigned to the device group](../apps/apps-deploy.md) created for your dedicated or fully managed devices.

      When the **Managed Home Screen** app is added, any other installed apps you add in the configuration profile are shown as icons on the **Managed Home Screen** app.

      For more information on the Managed Home screen, see [Setup Microsoft Managed Home Screen on dedicated and fully managed devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

      > [!NOTE]
      > Some of the **Managed Home Screen** settings are available in a device restrictions policy. To view and use all the available settings for the **Managed Home Screen**, [create a Managed Home Screen app configuration policy](../apps/app-configuration-managed-home-screen-app.md).

      - **Custom app layout**: **Enable** lets you put apps and folders in different places on the Managed Home Screen. When set to **Not configured**, Intune doesn't change or update this setting. By default, the apps and folders you add are shown on the home screen in alphabetical order.

        - **Grid size**: Select the size of your home screen. An app or folder takes one place on the grid.
        - **Home screen**: Select the add button, and select an app from the list. Select the **Folder** option to create a folder, enter the **Folder name**, and add apps from your list to the folder.

          When you add items, select the context menu to remove items, or move them to different positions:

          :::image type="content" source="./media/device-restrictions-android-for-work/custom-layout-context-menu.png" alt-text="Screenshot that shows how to move your apps and folders to different locations on Android Enterprise dedicated devices running in multi-app mode in Microsoft Intune.":::

      - **Add**: Select your apps from the list.

        If the **Managed Home Screen** app isn't listed, then [add it from Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Be sure to [assign the app](../apps/apps-deploy.md) to the device group created for your dedicated or fully managed devices.

        You can also add other [Android apps](../apps/apps-add-android-for-work.md) and [web apps](../apps/web-app.md) created by your organization to the device. Be sure to [assign the app to the device group created for your dedicated or fully managed devices](../apps/apps-deploy.md).

        > [!IMPORTANT]
        >
        > - In multi-app mode, every app in the policy must be a required app, and must be assigned to the devices. If an app isn't required, or isn't assigned, then the devices can lock out users, and show a `Contact your IT admin. This phone will be erased.` message.
        > - Applications added within the Managed Home Screen aren't prevented from launching other applications installed on the device. Admins should ensure that all applications allowed within the Managed Home Screen don't launch other apps that users shouldn't access. And, uninstall any apps that aren't necessary on the device.

      - **Configure offline app access**: **Checked** lets you select which apps are available when the device connect to the network for sign in. Users can access these apps when unable to sign in due to network issues and must sign in once network access returns. This setting requires **MHS Sign-in screen** to be set to **Enable**.

      - **Configure app access without sign in**: **Checked** lets you select which apps users can access from the sign-in screen without signing in. These apps are available via an entry point on the top bar, regardless of network status. The setting requires **MHS Sign-in screen** to be set to **Enable**.

      - **Lock home screen**: **Enable** prevents users from moving app icons and folders. They're locked, and can't be dragged-and-dropped to different places on the grid. When set to **Not configured**, Intune doesn't change or update this setting. By default, users can move these items.

      - **Folder icon**: Select the color and shape of the folder icon that's on the Managed Home Screen. Your options:
        - Not configured
        - Dark theme rectangle
        - Dark theme circle
        - Light theme rectangle
        - Light theme circle
      - **App and Folder icon size**: Select the size of the folder icon that's on the Managed Home Screen. Your options:
        - Not configured
        - Extra small
        - Small
        - Average
        - Large
        - Extra large

          Depending on the screen size, the actual icon size can be different.

      - **Screen orientation**: Select the direction the Managed Home Screen is shown on devices. Your options:
        - Not configured
        - Portrait
        - Landscape
        - Autorotate

        > [!NOTE]
        > Android 16 and newer doesn't support this setting for devices with larger form factors with 600 dp and larger display settings, like tablets.

      - **App notification badges**: **Enable** shows the number of new and unread notifications on app icons. When set to **Not configured**, Intune doesn't change or update this setting.
      - **Virtual home button**: A soft-key button that returns users to the Managed Home Screen so users can switch between apps. Your options:
        - **Not configured** (default): A home button isn't shown. Users must use the back button to switch between apps.
        - **Swipe-up**: A home button shows when a user swipes up on the device.
        - **Floating**: Shows a persistent, floating home button on the device.

      - **Leave kiosk mode**: **Enable** allows Administrators to temporarily pause kiosk mode to update the device. To use this feature, the administrator:

        1. Continues to select the back button until the **Exit kiosk** button shows.
        2. Selects the **Exit kiosk** button, and enters the **Leave kiosk mode code** PIN.
        3. When finished, select the **Managed Home Screen** app. This step relocks the device into multi-app kiosk mode.

        When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent administrators from pausing kiosk mode. If the administrator keeps selecting the back button, and selects the **Exit kiosk** button, then a message states that a passcode is required.

      - **Leave kiosk mode code**: Enter a 4-6 digit numeric PIN. The administrator uses this PIN to temporarily pause kiosk mode.

      - **Set custom URL background**: Enter a URL to customize the background screen on the dedicated or fully managed device. For example, enter `http://contoso.com/backgroundimage.jpg`.

        For most cases, we recommend starting with images of at least the following sizes:

        - Phone: 1080x1920 px
        - Tablet: 1920x1080 px

        For the best experience and crisp details, create per-device image assets to the display specifications.

        Modern displays have higher pixel densities and can display equivalent 2K/4K definition images.

      - **Shortcut to settings menu**: **Disable** hides the Managed Settings shortcut on the Managed Home Screen. Users can still access the **Managed Settings** menu from the top bar. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the Managed Settings shortcut is shown on devices. Users can select the settings icon to access settings.

      - **Quick access to debug menu**: This setting controls how users access the debug menu. Your options:

        - **Enable**: Users can access the debug menu easier. Specifically, they can access it from the Managed Settings menu. As always, they can continue to select the back button 15 times.
        - **Not configured** (default): Intune doesn't change or update this setting. By default, easy access to the debug menu is turned off. Users must select the back button 15 times to open the debug menu.

        In the debug menu, users can:

        - See and upload Managed Home Screen logs​
        - Open Google's Android Device Policy Manager app
        - Open the [Microsoft Intune app](https://play.google.com/store/apps/details?id=com.microsoft.intune)
        - Exit kiosk mode

      - **Wi-Fi configuration**: **Enable** shows the Wi-Fi control on the Managed Home Screen, and allows users to connect the device to different WiFi networks. Enabling this feature also turns on device location. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the Wi-Fi control on the Managed Home Screen. It prevents users from connecting to Wi-Fi networks while using the Managed Home Screen.

        - **Wi-Fi allow list**: Create a list of valid wireless network names, also known as the service set identifier (SSID). Managed Home Screen users can only connect to the SSIDs you enter.

          Wi-Fi SSIDs are case sensitive. If the SSID is valid but the capitalization you enter doesn't match the network name, then the network isn't shown.

          When left blank, Intune doesn't change or update this setting. By default, all available Wi-Fi networks are allowed.

          **Import** a .csv file that includes a list of valid SSIDs.

          **Export** your current list to a .csv file.

        - **SSID**: You can also enter the Wi-Fi network names (SSID) that Managed Home Screen users can connect to. Be sure to enter valid SSIDs.

        > [!IMPORTANT]
        > In the October 2020 release, the Managed Home Screen API was updated to be compliant with the Google Play Store requirements. The following changes affect Wi-Fi configuration policies in the Managed Home Screen:
        >
        > - Users can't enable or disable Wi-Fi connections on devices. Users can switch between Wi-Fi networks, but can't turn Wi-Fi on or off.
        >
        > - If a Wi-Fi network is password protected, then users must enter the password. After they enter the password, the configured network automatically connects. If they disconnect and then reconnect to the Wi-Fi network, then users might need to enter the password again.
        >
        > - On Android 11 devices, when users connect to a network using the Managed Home Screen, they're prompted to consent. This prompt comes from Android, and isn't specific to the Managed Home Screen.
        >
        > - On Android 10 devices, when users connect to a network using the Managed Home Screen, a notification prompts them to consent. So, users need access to the status bar and notifications to consent. To enable system notifications, see [General settings for fully managed and dedicated devices](#fully-managed-and-dedicated-devices) (in this article).
        >
        > - On Android 10 devices, when users connect to a password protected Wi-Fi network using the Managed Home Screen, they're prompted for the password. If the device is connected to an unstable network, then the Wi-Fi network changes. This behavior happens even when users enter the correct password.

      - **Bluetooth configuration**: **Enable** shows the Bluetooth control on the Managed Home Screen, and allows users to pair devices over Bluetooth. Enabling this feature also turns on device location. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the Bluetooth control on the Managed Home Screen. It prevents users from configuring Bluetooth and pairing devices while using the Managed Home Screen.

        For devices running on Android 10+ and using Managed Home Screen, for Bluetooth pairing to successfully work on devices that require a pairing key, admins must enable the following Android system apps:

        - Android System Bluetooth
        - Android System Settings
        - Android System UI

        For more information on how to enable Android system apps, go to: [Manage Android Enterprise system apps](../apps/apps-ae-system.md#enable-a-system-app-in-intune)

      - **Flashlight access**: **Enable** shows the flashlight control on the Managed Home Screen, and allows users to turn the flashlight on or off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the flashlight control on Managed Home Screen. It prevents users from using the flashlight while using the Managed Home Screen.

      - **Media volume control**: **Enable** shows the media volume control on the Managed Home Screen, and allows users to adjust the device's media volume using a slider. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the media volume control on Managed Home Screen. It prevents users from adjusting the device's media volume while using the Managed Home Screen, unless their hardware buttons support it.

      - **Quick access to device information**: **Enable** allows users to swipe down to see the device information on the Managed Home Screen, such as the serial number, make and model number, and SDK level. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the device information might not be shown.

      - **Screen saver mode**: **Enable** shows a screensaver on the Managed Home Screen when the device is locked or times out. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show a screensaver on the Managed Home Screen.

        When enabled, also configure:

        - **Set custom screen saver image**: Enter the URL to a custom PNG, JPG, JPEG, GIF, BMP, WebP, or ICOimage. If you don't enter a URL, then the device's default image is used, if there's a default image.

          For example, enter:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > Any file resource URL that can be turned into a bitmap is supported.

        - **Number of seconds the device shows screen saver before turning off screen**: Choose how long the device shows the screensaver. Enter a value between 0-9999999 seconds. Default is `0` seconds. When left blank, or set to zero (`0`), the screen saver is active until a user interacts with the device.
        - **Number of seconds the device is inactive before showing screen saver**: Choose how long the device is idle before showing the screensaver. Enter a value between 1-9999999 seconds. Default is `30` seconds. You must enter a number greater than zero (`0`).
        - **Detect media before starting screen saver**: **Enable** (default) doesn't show the screen saver if audio or video is playing on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the screen saver, even if audio or video is playing.

          Managed Home Screen starts the screensaver whenever the lock screen appears:

          - If the system's lock screen timeout is longer than the number of seconds for device to show the screensaver, then the screensaver shows until the lock screen appears.
          - If the system's lock screen timeout is shorter than the number of seconds the device is inactive, then the screensaver shows as soon as the device's lock screen appears.

      - **MHS Sign-in screen** (*Dedicated devices only*): **Enable** shows a sign-in screen on the Managed Home Screen. When set to **Not configured** (default), Intune doesn't change or update this setting. This sign-in screen and related settings are intended for use on dedicated devices enrolled with Microsoft Entra shared device mode.

        When enabled, also configure:

        - **Set custom URL background for sign-in screen**: Enter the URL of the URL background for the sign-in screen. The sign-in screen must be enabled to configure this setting.
        - **Set custom URL branding logo for sign-in screen and session pin page**: Enter the URL branding logo for the sign-in screen and session pin page.
        - **Require user to set a PIN for sign-in session**: When set to **Enable**, the user must set a PIN for their sign-in session. When set to **Not configured** (default), the user isn't required to set a PIN. This setting must be enabled to show the subsettings.
          - **Choose complexity of PIN for sign-in session**: Select the complexity of the session PIN. Your options:
            - **Not configured**: Intune doesn't change or update this setting. By default, MHS requires at least one character in the session PIN.
            - **Simple**: Requires numbers. There are no restrictions on repeating (444) or ordered (123, 321, 246) sequences.
            - **Complex**: Allows users to create a PIN with alphanumeric characters. Can't use repeating (444) or ordered (123, 321, 246) sequences.

            For more information on this setting, see **Complexity of session PIN** at [create a Managed Home Screen app configuration policy](../apps/app-configuration-managed-home-screen-app.md).

          - **Require user to enter session PIN if screensaver has appeared**: Select **Enable** to require the user to enter their session PIN to resume using the Managed Home Screen after the screensaver shows.
        - **Automatically sign-out of MHS and Shared device mode applications after inactivity**: Select **Enable** to auto sign out of the Managed Home Screen based on inactivity. This setting must be enabled to show the subsettings.
          - **Number of seconds device is inactive before automatically signing user out​**: Define the period of inactivity, in seconds, before user is automatically signed out from Managed Home Screen. By default, this value is set to 300 seconds.
          - **Number of seconds to give user notice before automatically signing them out**: Define the amount of time, in seconds, for user to have option to resume their session before getting automatically signed out from Managed Home Screen. By default, this value is set to 60 seconds.

      > [!NOTE]
      > Some of the Managed Home Screen settings are available in a device restrictions policy. To view and use all the available settings for the Managed Home Screen, create a [Managed Home Screen app configuration policy](../apps/app-configuration-managed-home-screen-app.md).

- **Microsoft launcher (fully managed only)**: Configures the Microsoft Launcher app on fully managed devices. This option is best suited for devices which should provide the end user access to all applications and settings on the device.

  - **Make Microsoft Launcher the default launcher**: **Enable** sets Microsoft Launcher as the default launcher on the home screen. If you make Launcher the default, users can't use another launcher. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the Microsoft Launcher isn't forced as the default launcher.
  - **Configure custom wallpaper**: In the Microsoft Launcher app, **Enable** lets you apply your own image as the home screen wallpaper, and choose if users can change the image. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the device keeps its current wallpaper.
    - **Enter URL of wallpaper image**: Enter the URL of your wallpaper image. This image shows on the device home screen. For example, enter `http://www.contoso.com/image.jpg`.
    - **Allow user to modify wallpaper**: **Enable** allows users to change the wallpaper image. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the wallpaper.
  - **Enable launcher feed**: **Enable** turns on the launcher feed, which shows calendars, documents, and recent activities. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, this feed isn't shown.
    - **Allow user to enable/disable feed**: **Enable** lets users enable or disable the launcher feed. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the launcher feed settings.
  - **Dock presence**: The dock gives users quick access to their apps and tools. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting.
    - **Show**: The dock is shown on devices.
    - **Hide**: The dock is hidden. Users must swipe up to access the dock.
    - **Disabled**: The dock isn't shown on devices, and users are prevented from showing it.

  - **Allow user to change dock presence**: **Enable** allows users to show or hide the dock. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users aren't allowed to change the device dock configuration.

  - **Search bar replacement**: Choose where to put the search bar. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting.
    - **Top**: Search bar is shown at the top of devices.
    - **Bottom**: Search bar is shown at the bottom of devices.
    - **Hide**: Search bar is hidden.

## Device password

### Fully managed, dedicated, and corporate-owned work profile devices

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default** (default): Most devices don't require a password when set to **Device default**. If you want to require users to setup a passcode on their devices, configure this setting to something more secure than **Device default**.
  - **Password required, no restrictions**
  - **Weak biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Numeric**: Password must only be numbers, such as `123456789`. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphabetic**: Letters in the alphabet are required. Numbers and symbols aren't required. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols. Also enter:

    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
    - **Number of characters required**: Enter the number of characters the password must have, between 0 and 16 characters.
    - **Number of lowercase characters required**: Enter the number of lowercase characters the password must have, between 0 and 16 characters.
    - **Number of uppercase characters required**: Enter the number of uppercase characters the password must have, between 0 and 16 characters.
    - **Number of non-letter characters required**: Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.
    - **Number of numeric characters required**: Enter the number of numeric characters (`1`, `2`, `3`, and so on) the password must have, between 0 and 16 characters.
    - **Number of symbol characters required**: Enter the number of symbol characters (`&`, `#`, `%`, and so on) the password must have, between 0 and 16 characters.

- **Number of days until password expires**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank, Intune doesn't change or update this setting.
- **Number of passwords required before user can reuse a password**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 4-11. When the value is blank, Intune doesn't change or update this setting.

  > [!NOTE]
  >
  > - Users on fully managed, and corporate-owned work profile devices aren't prompted to set a password. The settings are required, but users might not be notified. Users need to set the password manually. The policy reports as failed until the user sets a password that meets your requirements.
  >
  >   To apply the device password settings during device enrollment, assign the device restriction profile to users (no [filters](../fundamentals/filters.md)). Don't assign the profile to devices. During enrollment, users are asked to set a screen lock. Then, they must choose a device password that meets all the requirements in this device restriction profile.
  > - On dedicated devices, if the device is set up with single or multi-app kiosk mode, then users are prompted to set a password. Screens force and guide users to create a compliant password before they can continue using the device.
  > - On dedicated devices that aren't using kiosk mode, users aren't notified of any password requirement. Users need to set the password manually. The policy reports as failed until the user sets a password that meets your requirements.

- **Disabled lock screen features**: When the device is locked, choose the features that can't be used. For example, when **Secure camera** is checked, the camera feature is disabled on the device. Any features not checked are enabled on the device.

  These features are available to users when the device is locked. Users won't see or access the features that you check.

  - On corporate-owned work profile devices, only **Unredacted notifications**, **Trust agents**, and **Fingerprint unlock** can be disabled.
  - If users turn off the **Use one lock** setting on their device, then disabling **Fingerprint unlock** and disabling **Trust agents** apply at the corporate-owned work profile-level. If users turn on the **Use one lock** setting, then disabling **Fingerprint unlock** and disabling **Trust agents** apply at the device-level.

- **Required unlock frequency**: Strong authentication is when users unlock a device using a password, PIN, or pattern. Non-strong authentication methods are when users unlock a device using some biometric options, such as a fingerprint or face scan.

  Select how long users have before they're required to unlock the device using a strong authentication method. Your options:

  - **Device default** (default): The screen locks using the device's default time.
  - **24 hours since last pin, password, or pattern unlock**: The screen locks 24 hours after users last used a strong authentication method to unlock the device. When the timeout is reached, non-strong authentication methods are disabled until the device is unlocked using strong authentication.

  [2.3.4 Advanced passcode management: Strong Authentication required timeout](https://developers.google.com/android/work/requirements#2.3.-advanced-passcode-management_1) (opens Android's web site)

### Fully managed and dedicated devices

- **Disable lock screen**: **Disable** blocks all Keyguard lock screen features from being used. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, when the device is in lock screen, the OS might allow all the Keyguard features, such as camera, fingerprint unlock, and more.

## Power settings

### Fully managed, dedicated, and corporate-owned work profile devices

- **Time to lock screen (work profile-level)**: Enter the maximum time a user can set until the device locks. For example, if you set this setting to `10 minutes`, then users can set the time from 15 seconds up to 10 minutes. When set to **Not configured** (default), Intune doesn't change or update this setting.

### Fully managed and dedicated devices

- **Screen on while device plugged in**: Choose which power sources cause the device's screen to stay on when plugged in.

## Users and Accounts

### Fully managed, dedicated, and corporate-owned work profile devices

- **Add new users**: **Block** prevents users from adding new users. Each user has a personal space on the device for custom Home screens, accounts, apps, and settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add other users to the device.
- **User can configure credentials (work profile-level)**: **Block** prevents users from configuring certificates assigned to devices, even devices that aren't associated with a user account. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might make it possible for users to configure or change their credentials when they access them in the keystore.

### Fully managed and dedicated devices

- **User removal**: **Block** prevents users from removing users. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to remove other users from the device.
- **Personal Google Accounts**: **Block** prevents users from adding their personal Google account to the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add their personal Google account.

### Dedicated devices

- **Account changes**: **Block** prevents users from updating or changing accounts when in kiosk mode. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to update user accounts on the device.

## Applications

### Fully managed, dedicated, and corporate-owned work profile devices

> [!NOTE]
> If you want to enable side-loading, set the **Allow installation from unknown sources** and **Allow access to all apps in Google Play store** settings to **Allow**.

- **Allow installation from unknown sources**: **Allow** lets users turn on **Unknown sources**. This setting allows apps to install from unknown sources, including sources other than the Google Play Store. It allows users to side-load apps on the device using means other than the Google Play Store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from turning on **Unknown sources**.

- **App auto-updates (work profile-level)**: Devices check for app updates daily. Choose when automatic updates are installed. Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **User choice**: The OS might default to this option. Users can set their preferences in the Managed Google Play app.
  - **Never**: Updates are never installed. This option isn't recommended.
  - **Wi-Fi only**: Updates are installed only when the device is connected to a Wi-Fi network.
  - **Always**: Updates are installed when they're available.

- **Allow access to all apps in Google Play store**:

  - When set to **Block**:

    - Users can't access apps in the Google Play store. They can't access any private apps added to your organization's Managed Google Play account.
    - Only shows apps in the Managed Google Play store that are approved, apps that are required, and apps that are assigned to the user.
    - Uninstalls apps that were installed outside of the Managed Google Play store.

    > [!WARNING]
    >
    > If you change this setting from **Allow** to **Block**, then any app not marked as **Required** or **Available** is automatically uninstalled from the device.

  - When set to **Allow**:

    - Users get access to all apps in the Google Play store and any private apps added to your organization's Managed Google Play account.
    - Make sure you target any app (private or public) with the uninstall intent that shouldn't be findable or apps installed by users from the Managed Google Play Store.
    - Users can't use apps that are added to a blocklist (assigned with uninstall intent) on the personal profile of corporate-owned devices with a work profile.

    For more information on excluding users and groups from specific apps, go to [Include and exclude app assignments](../apps/apps-inc-exl-assignments.md).

  - When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS:

    - Only shows apps in the Managed Google Play store that are approved, apps that are required, and apps that are assigned to the user.

- The following settings are part of the Google's delegated scope feature:

  - **Allow other apps to install and manage certificates**: Select **Add** to select existing apps for this permission. You can add multiple apps. The selected apps are granted access to install and manage certificates.

    To use this setting, your Managed Google Play app must use delegated scopes. For more information, go to [Android's built-in app configurations](../developer/app-sdk-android-phase6.md#androids-built-in-app-configurations) and [Android delegation scopes](https://developer.android.com/work/versions/android-10#new_delegation_scopes) (opens Android's web site).

  - **Allow this app to access Android security logs**: Select the app that should have this permission. You can only select one app. The app is granted access to the security logs.

    To use this setting, your Managed Google Play app must use delegated scopes. For more information, go to [Android's built-in app configurations](../developer/app-sdk-android-phase6.md#androids-built-in-app-configurations) and [Android delegation scopes](https://developer.android.com/work/versions/android-10#new_delegation_scopes) (opens Android's web site).

  - **Allow this app to access Android network activity logs**: Select the app that should have this permission. You can only select one app. The app is granted access to the network activity logs.

    To use this setting, your Managed Google Play app must use delegated scopes. For more information, go to [Android's built-in app configurations](../developer/app-sdk-android-phase6.md#androids-built-in-app-configurations) and [Android delegation scopes](https://developer.android.com/work/versions/android-10#new_delegation_scopes) (opens Android's web site).

  > [!TIP]
  > If there's a conflict with one of these settings, then the conflict applies to all three settings. Make sure you give the **Allow this app to access Android security logs** and **Allow this app to access Android network activity logs** permissions to only one app. You can give these permissions to the same app, but not different apps.
  >
  > For more information, go to [Android Management API - DelegatedScope](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#delegatedscope) (opens Google's web site).

### Dedicated devices

- **Clear local data in apps not optimized for Shared device mode**: Add any app not optimized for shared device mode to the list. The app's local data is cleared whenever a user signs out of an app that's optimized for shared device mode. Available for dedicated devices enrolled with Shared mode running Android 9 and later.

  When you use this setting, users can't initiate sign out from non-optimized apps and don't get single sign out.
  - Users need to sign out of an app that is optimized for Shared Device mode. Microsoft apps that are optimized for Shared device mode on Android include Teams and Intune's Managed Home Screen.
  - For apps that aren't optimized for Shared Device mode, deleting application data extends to local app storage only. Data can be left in other areas of the device. User identifying artifacts such as email address and username might be left behind on the app and visible by others.
  - Non-optimized apps that provide support for multiple accounts could exhibit indeterminate behavior and are therefore not recommended.

  All non-optimized apps should be thoroughly tested before being used in multi-user scenarios on shared devices to ensure they work as expected. For example, validate your core scenarios in each app, verify that the app signs out properly, and that all data is sufficiently cleared for your organization's needs.

## Connectivity

### Fully managed, dedicated, and corporate-owned work profile devices

- **Always-on VPN  (work profile-level)**: **Enable** sets the VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected. Or, immediately connect when users lock their device, the device restarts, or the wireless network changes.

  Choose **Not configured** to disable always-on VPN for all VPN clients.

  > [!IMPORTANT]
  > Be sure to deploy only one Always-on VPN policy to a single device. Deploying multiple Always-on VPN policies to a single device isn't supported.

- **VPN client**: Choose a VPN client that supports Always On. Your options:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Custom
    - **Package ID**: Enter the package ID of the app in the Google Play store. For example, if the URL for the app in the Play store is `https://play.google.com/store/details?id=com.contosovpn.android.prod`, then the package ID is `com.contosovpn.android.prod`.

  The VPN client you choose must be installed on the device, and it must support per-app VPN in corporate-owned work profiles. Otherwise, an error occurs.

  - You do need to approve the VPN client app in the **Managed Google Play Store**, sync the app to Intune, and deploy the app to the device. After these steps, the app is installed in the user's corporate-owned work profile.
  - You still need to configure the VPN client with a [VPN profile](vpn-settings-android-enterprise.md), or through an [app configuration profile](../apps/app-configuration-policies-use-android.md).
  - There might be known issues when using per-app VPN with F5 Access for Android 3.0.4. For more information, see [F5's release notes for F5 Access for Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Lockdown mode**: **Enable** forces all network traffic to use the VPN tunnel. If a connection to the VPN isn't established, then the device won't have network access. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow traffic to flow through the VPN tunnel or through the mobile network.

### Fully managed and dedicated devices

- **Recommended global proxy**: **Enable** adds a global proxy to the devices. When enabled, HTTP and HTTPS traffic use the proxy you enter, including some apps on the device. This proxy is only a recommendation. It's possible some apps won't use the proxy. **Not configured** (default) doesn't add a recommended global proxy.

  For more information on this feature, see [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (opens an Android site).

  When enabled, also enter the **Type** of proxy. Your options:

  - **Direct**: Manually enter the proxy server details, including:
    - **Host**: Enter the hostname or IP address of your proxy server. For example, enter `proxy.contoso.com` or `127.0.0.1`.
    - **Port number**: Enter the TCP port number used by the proxy server. For example, enter `8080`.
    - **Excluded hosts**: Enter a list of host names or IP addresses that won't use the proxy. This list can include an asterisk (`*`) wildcard and multiple hosts separated by semicolons (`;`) with no spaces. For example, enter `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Proxy Auto-Config**: Enter the **PAC URL** to a proxy autoconfiguration script. For example, enter `https://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

  For more information on this feature, see [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (opens an Android site).

## Work profile password

These settings apply to corporate-owned work profiles.

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default**
  - **Password required, no restrictions**
  - **Weak biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Numeric**: Password must only be numbers, such as `123456789`. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphabetic**: Letters in the alphabet are required. Numbers and symbols aren't required. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters. Also enter:
    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
  - **Alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols. Also enter:

    - **Minimum password length**: Enter the minimum length the password must have, between 4 and 16 characters.
    - **Number of characters required**: Enter the number of characters the password must have, between 0 and 16 characters.
    - **Number of lowercase characters required**: Enter the number of lowercase characters the password must have, between 0 and 16 characters.
    - **Number of uppercase characters required**: Enter the number of uppercase characters the password must have, between 0 and 16 characters.
    - **Number of non-letter characters required**: Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.
    - **Number of numeric characters required**: Enter the number of numeric characters (`1`, `2`, `3`, and so on) the password must have, between 0 and 16 characters.
    - **Number of symbol characters required**: Enter the number of symbol characters (`&`, `#`, `%`, and so on) the password must have, between 0 and 16 characters.

- **Number of days until password expires**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank, Intune doesn't change or update this setting.
- **Number of passwords required before user can reuse a password**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 4-11. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.

  > [!NOTE]
  > Fully managed, dedicated, and corporate-owned work profile devices aren't prompted to set a password. The settings are required, but users might not be notified. Users need to set the password manually. The policy reports as failed until the user sets a password that meets your requirements.

- **Required unlock frequency**: Strong authentication is when users unlock the work profile using a password, PIN, or pattern. Non-strong authentication methods are when users unlock the work profile using some biometric options, such as a fingerprint or face scan.

  Select how long users have before they're required to unlock the work profile using a strong authentication method. Your options:

  - **Device default** (default): The screen locks using the device's default time.
  - **24 hours since last pin, password, or pattern unlock**: The screen locks 24 hours after users last used a strong authentication method to unlock the work profile. When the timeout is reached, non-strong authentication methods are disabled until the work profile is unlocked using strong authentication.

  [2.3.4 Advanced passcode management: Strong Authentication required timeout](https://developers.google.com/android/work/requirements#2.3.-advanced-passcode-management_1) (opens Android's web site)

## Personal profile

- **Camera**: **Block** prevents access to the camera during personal use. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the camera in the personal profile.
- **Screen capture**: **Block**:
  - Prevents screen captures during personal use
  - Prevents apps from using the system screenshot capabilities.
  - Affects screen sharing.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to get screen captures or screenshots in the personal profile.

- **Allow users to enable app installation from unknown sources in the personal profile**: Select **Allow** so users can install apps from unknown sources in the personal profile. It allows users to install apps from sources other than the Google Play Store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from installing apps from unknown sources in the personal profile.
- **Type of restricted apps list**: Select **Allow apps** to create a list of Managed Google Play apps that are allowed and approved to install and run in the personal profile on the device. Select **Blocked apps** to create a list of Managed Google Play apps that are prohibited and prevented from installing and running in the personal profile on the device. When set to **Not configured** (default), Intune doesn't include a list of apps to allow or block.

## Custom support information

Using these settings, you can customize some support messages shown to users, and show these messages in different languages.

By default, the OEM default messages are shown. When you deploy a custom message using Intune, the Intune default message is also deployed. If you don't enter a custom message for the device's default language, then the Intune default message is automatically shown.

By default, the Intune default message is in **English (United States)**.

For example, you deploy a custom message for English and French. The user changes the device's default language to Spanish. Since you didn't deploy a custom message to the Spanish language, then the Intune default message is shown.

The Intune default message is translated for all languages in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Settings** > **Language + Region**). The **Language** setting value determines the default language used by Intune. By default, the langue is set to **English**.

You can configure the following settings:

- **Short support message**: When users try to change a setting that's managed by the organization, a short message is shown.

  Using the following settings, you can customize this message and enter a different message for different languages. By default, this message is in **English (United States)**.

  - **All, except when specified**: This message is the Intune default message, and is shown for all languages. If you don't enter a custom message, then this text is automatically shown. This text is also automatically translated to the device's default language.

    You can change this message. Any changes aren't translated. If you delete all the text in this message and leave this setting blank, then the following original short Intune default message is used and is translated:

    `You do not have permission for this action. For more information, contact your IT admin.`

  - **Select Locale**: Select the locale or region to show a different custom message for that specific locale.

    For example, to show a custom message on devices using **Spanish** as the default language, select **Spanish (Spain)**. Only devices using the **Spanish (Spain)** default language see your custom message. All other languages see the **All, except when specified** message text.

    You can add multiple locales and messages.

  - **Message**: Enter the text you want shown, a max of 200 characters. The text you enter isn't translated to the device's default language. So if you want to show a message in Spanish, enter the text in Spanish.

- **Long support message**: On the device, in **Settings** > **Security** > **Device admin apps** > **Device Policy**, a long support message is shown.

  Using the following settings, you can customize this message and enter a different message for different languages. By default, this message is in **English (United States)**.

  - **All, except when specified**: This message is the Intune default message, and is shown for all languages. If you don't enter a custom message, then this text is automatically shown, and is automatically translated to the device's default language.

    You can change this message. Any changes aren't translated. If you delete all the text in this message and leave this setting blank, then the following original long Intune default message is used and is translated:

    `The organization's IT admin can monitor and manage apps and data associated with this device, including settings, permissions, corporate access, network activity and the device's location information.`

  - **Select Locale**: Select the locale or region to show a different custom message for that specific locale.

    For example, to show a custom message on devices using **Spanish** as the default language, select **Spanish (Spain)**. Only devices using the **Spanish (Spain)** default language see your custom message. All other languages see the **All, except when specified** message text.

    You can add multiple locales and messages.

  - **Message**: Enter the text you want shown, a max of 4096 characters. The text you enter isn't translated to the device's default language. So if you want to show a message in Spanish, enter the text in Spanish.

- **Lock screen message**: Enter the text you want shown on the device lock screen.

  Using the following settings, you can customize this message and enter a different message for different languages. By default, this message is in **English (United States)**.

  - **All, except when specified**: Enter the text you want shown for all languages, a max of 4096 characters. This text is automatically translated to the device's default language. If you don't enter a custom message, then Intune doesn't change or update this setting. By default, the OS might not show a lock screen message.

  - **Select Locale**: Select the locale or region to show a different custom message for that specific locale.

    For example, to show a custom message on devices using **Spanish** as the default language, select **Spanish (Spain)**. Only devices using the **Spanish (Spain)** default language see your custom message. All other languages see the **All, except when specified** message text.

    You can add multiple locales and messages.

  - **Message**: Enter the text you want shown, a max of 4096 characters. The text you enter isn't translated to the device's default language. So if you want to show a message in Spanish, enter the text in Spanish.

  When you configure the **Lock screen message**, you can also use the following device tokens to show device-specific information:

  - `{{AADDeviceId}}`: Microsoft Entra device ID
  - `{{AccountId}}`: Intune tenant ID or account ID
  - `{{DeviceId}}`: Intune device ID
  - `{{DeviceName}}`: Intune device name
  - `{{domain}}`: Domain name
  - `{{EASID}}`: Exchange Active Sync ID
  - `{{IMEI}}`: IMEI of the device
  - `{{mail}}`: Email address of the user
  - `{{MEID}}`: MEID of the device
  - `{{partialUPN}}`: UPN prefix before the @ symbol
  - `{{SerialNumber}}`: Device serial number
  - `{{SerialNumberLast4Digits}}`: Last four digits of the device serial number
  - `{{UserId}}`: Intune user ID
  - `{{UserName}}`: User name
  - `{{userPrincipalName}}`: UPN of the user

  > [!NOTE]
  > Variables aren't validated in the UI and are case sensitive. As a result, you can see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}`, instead of `{{deviceid}}` or `{{DEVICEID}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information. All lowercase or all uppercase variables are supported, but not a mix.

# [Personally owned](#tab/aepersonal)

These settings apply to Android Enterprise personally owned devices with a work profile (BYOD). When users enroll their personal devices in Intune, a work profile is created on the device. The work profile is a separate space on the device that keeps work apps and data separate from personal apps and data.

These settings configure the work profile.

## Work profile settings

These settings apply to Android Enterprise personally owned devices with a work profile (BYOD).

### General settings

- **Copy and paste between work and personal profiles**: **Block** prevents copy-and-paste between work and personal apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to share data using copy-and-paste with apps in the personal profile.
- **Data sharing between work and personal profiles**: Choose if apps in the work profile can share with apps in the personal profile. For example, you can control sharing actions within applications, such as the **Share…** option in the Chrome browser app. This setting doesn't apply to copy/paste clipboard behavior. Your options:
  - **Device default**: Sharing from the work profile to the personal profile is blocked. Sharing from the personal profile to the work profile is allowed.
  - **Apps in work profile can handle sharing request from personal profile**: Enables the built-in Android feature that allows sharing from the personal profile to the work profile. When enabled, a sharing request from an app in the personal profile can share with apps in the work profile.
  - **No restrictions on sharing**: Enables sharing across the work profile boundary in both directions. When you select this setting, apps in the work profile can share data with unbadged apps in the personal profile. This setting allows managed apps in the work profile to share with apps on the unmanaged side of the device. So, use this setting carefully.

- **Work profile notifications while device locked**: **Block** prevents window notifications, including toasts, incoming calls, outgoing calls, system alerts, and system errors from showing on locked devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show notifications.
- **Default app permissions**: Sets the default permission policy for all apps in the work profile. Starting with Android 6, users are prompted to grant certain permissions required by apps when the app is launched. This policy setting lets you decide if users are prompted to grant permissions for all apps in the work profile. For example, you assign an app to the work profile that requires location access. Normally that app prompts users to approve or deny location access to the app. Use this policy to automatically grant permissions without a prompt, automatically deny permissions without a prompt, or let users decide. Your options:
  - **Device default**
  - **Prompt**
  - **Auto grant**
  - **Auto deny**

  You can also use an app configuration policy to grant permissions for individual apps (**Apps** > **Configuration**).

- **Add and remove accounts**: This setting allows or prevents accounts from being added in the work profile, including Google accounts. Your options:

  - **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

    In a previous release, this setting was named **Not configured**.

  - **Allow all account types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

    You can also configure:

    - **Google domain allow-list**:  Restricts users to add only certain Google account domains in the work profile. You can import a list of allowed domains in the following format:

      ```csv
      contoso.com
      microsoft.com
      ```

      Or, add the domains individually using the `contoso.com` format. When left blank, by default, the OS might allow adding all Google domains in the work profile.

    This setting requires:

    - Google Play app version 80970100 or higher

  - **Block all account types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.

  > [!NOTE]
  > On personally owned devices with a work profile (BYOD) and corporate owned devices with work profile (COPE), Google accounts can't be added to the **Settings** app > **Accounts** > **Work**.

- **Contact sharing via Bluetooth**: **Enable** allows sharing and access to personally owned devices with work profile contacts from another device that's paired using Bluetooth, including a car. Enabling this setting can allow certain Bluetooth devices to cache work contacts upon first connection. Disabling this policy after an initial pairing/sync might not remove work contacts from a Bluetooth device.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not share work contacts.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Screen capture**: **Block**:
  - Prevents screenshots or screen captures on the device in the work profile.
  - Prevents the content from being shown on display devices that don't have a secure video output.
  - Prevents apps from using the system screenshot capabilities.
  - Affects screen sharing.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow getting screenshots.

- **Display work contact caller-id in personal profile**: **Block** doesn't show the work contact caller number in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show work contact caller details.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Search work contacts from personal profile**: **Block** prevents users from searching for work contacts in apps in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow searching for work contacts in the personal profile.

- **Camera**: **Block** prevents access to the camera on the device in the personally owned work profile. This setting doesn't affect the camera on the personal side. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the camera.

- **Allow widgets from work profile apps**: **Enable** allows users to put widgets exposed by apps on the home screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.

  For example, Outlook is installed on your users' work profile. When set to **Enable**, users can put the agenda widget on the device home screen.

### Work Profile Password

These password settings apply to the work profile password on personally owned devices with a work profile.

#### All Android devices

- **Require Work Profile Password**: **Require** forces a passcode policy that only applies to apps in the work profile. By default, users can use the two separately defined PINs. Or, users can combine the PINs into the stronger of the two PINs. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use work apps without entering a password.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Maximum minutes of inactivity until work profile locks**: Enter the length of time devices must be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

  On devices, users can't set a time value greater than the configured time in the profile. Users can set a lower time value. For example, if the profile is set to `15` minutes, users can set the value to 5 minutes. Users can't set the value to 30 minutes.

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the work profile on the device is wiped, from 4-11. When the value is blank, Intune uses the default value on this setting.

- **Password expiration (days)**: Enter the number of days until user passwords must be changed (from **1**-**365**).

- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Face unlock**: **Block** prevents users from using the device's facial recognition to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using facial recognition.
- **Fingerprint unlock**: **Block** prevents users from using the device's fingerprint scanner to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.
- **Iris unlock**: **Block** prevents users from using the device's iris scanner to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using the iris scanner.
- **Smart Lock and other trust agents**: **Block** prevents Smart Lock or other trust agents from adjusting lock screen settings on compatible devices. If devices are in a trusted location, then this feature, also known as a trust agent, lets you disable or bypass the device lock screen password. For example, bypass the work profile password when devices are connected to a specific Bluetooth device, or when devices are close to an NFC tag. Use this setting to prevent users from configuring Smart Lock.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

- **One lock for device and work profile**: **Block** prevents users from using the same password for the lock screen on the device and work profile. End users are required to enter the device password to unlock the device and enter their work profile password to access their work profile.

  When set to **Not Configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access their work profile using a single password.

#### Android 12 and later

- **Password complexity**: Use this setting to set the password complexity requirements. Your options:

  - **None**: Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low**: A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least four characters.
  - **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least eight characters. The alphabetic or alphanumeric length must be at least six characters.

  On personally owned devices with a work profile, there are two passwords affected by this **Password complexity** setting:

  - The device password that unlocks the device
  - The work profile password that allows users to access the work profile

  If the device password complexity is too low, then the device password is automatically changed to require a **High** complexity. The end users must update the device password to meet the complexity requirements. Then, they sign into the work profile and are prompted to update the work profile complexity configured in the **Password complexity** setting in your policy.

  > [!IMPORTANT]
  >
  > Before the **Password complexity** setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available and deprecated by Google for Android 12+ personally owned devices with a work profile. For information on these settings, go to [Android 11 and earlier](#android-11-and-earlier) (in this article).
  >
  > Here's what you need to know:
  >
  > - If the **Required password type** and **Minimum password length** settings are changed from the default values in a policy, then:
  >   - Newly enrolled Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity. So if you don't want a **High** password complexity, then create a new policy for Android Enterprise 12+ devices and configure the **Password complexity** setting.
  >   - Existing Android Enterprise 12+ devices will continue to use the **Required password type** and **Minimum password length** settings, and the existing values that are already configured.
  >
  >     If you change an existing policy with the **Required password type** and **Minimum password length** settings that already configured, then Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity.
  >
  >     For Android Enterprise 12+ devices, configure the **Password complexity** setting.
  >
  > - If the **Required password type** and **Minimum password length** settings aren't changed from the default values in a policy, then no password policy is automatically applied to newly enrolled Android Enterprise 12+ devices.

#### Android 11 and earlier

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default** (default): Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low security biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Required**
  - **At least numeric**: Includes numeric characters, such as `123456789`.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**: Includes letters in the alphabet. Numbers and symbols aren't required.
  - **At least alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
  - **At least alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

- **Minimum password length**: Enter the minimum length the password must have, between 4 (default) and 16 characters.

> [!IMPORTANT]
>
> - Google is deprecating these **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing it with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).
> - On Android Enterprise 12+ devices, use the **Password complexity** setting.

## Password

These password settings apply to the device password on personally owned devices with a work profile.

### All Android devices

- **Maximum minutes of inactivity until screen locks**: Enter the length of time devices must be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

  On devices, users can't set a time value greater than the configured time in the profile. Users can set a lower time value. For example, if the profile is set to `15` minutes, users can set the value to 5 minutes. Users can't set the value to 30 minutes.

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the personally owned work profile in the device is wiped, from 4-11. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.
- **Password expiration (days)**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank, Intune doesn't change or update this setting.

- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Fingerprint unlock**: **Block** prevents users from using the device's fingerprint scanner to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.
- **Face unlock**: **Block** prevents users from using the device's facial recognition to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using facial recognition.
- **Iris unlock**: **Block** prevents users from using the device's iris scanner to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using the iris scanner.
- **Smart Lock and other trust agents**: **Block** prevents Smart Lock or other trust agents from adjusting lock screen settings on compatible devices. If devices are in a trusted location, then this feature, also known as a trust agent, lets you disable or bypass the device lock screen password. For example, bypass the personally owned work profile password when devices are connected to a specific Bluetooth device, or when devices are close to an NFC tag. Use this setting to prevent users from configuring Smart Lock.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

### Android 12 and later

- **Password complexity**: Use this setting to set the password complexity requirements. Your options:

  - **None**: Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low**: A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least four characters.
  - **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least eight characters. The alphabetic or alphanumeric length must be at least six characters.

  On personally owned devices with a work profile, there are two passwords affected by this **Password complexity** setting:

  - The device password that unlocks the device
  - The work profile password that allows users to access the work profile

  If the device password complexity is too low, then the device password is automatically changed to require a **High** complexity. The end users must update the device password to meet the complexity requirements. Then, they sign into the work profile and are prompted to update the work profile complexity configured in the **Password complexity** setting in your policy.

  > [!IMPORTANT]
  >
  > Before the **Password complexity** setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available and they're deprecated by Google for Android 12+ personally owned devices with a work profile. For more information on these settings, go to [Android 11 and earlier](#android-11-and-earlier-1) (in this article).
  >
  > Here's what you need to know:
  >
  > - If the **Required password type** and **Minimum password length** settings are changed from the default values in a policy, then:
  >   - Newly enrolled Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity. So if you don't want a **High** password complexity, then create a new policy for Android Enterprise 12+ devices and configure the **Password complexity** setting.
  >   - Existing Android Enterprise 12+ devices will continue to use the **Required password type** and **Minimum password length** settings, and the existing values that are already configured.
  >
  >     If you change an existing policy with the **Required password type** and **Minimum password length** settings that already configured, then Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity.
  >
  >     For Android Enterprise 12+ devices, configure the **Password complexity** setting.
  >
  > - If the **Required password type** and **Minimum password length** settings aren't changed from the default values in a policy, then no password policy is automatically applied to newly enrolled Android Enterprise 12+ devices.

### Android 11 and earlier

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default** (default): Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low security biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Required**
  - **At least numeric**: Includes numeric characters, such as `123456789`.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**: Includes letters in the alphabet. Numbers and symbols aren't required.
  - **At least alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
  - **At least alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

- **Minimum password length**: Enter the minimum length the password must have, between 4 (default) and 16 characters.

> [!IMPORTANT]
>
> - Google is deprecating these **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing it with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).
> - On Android Enterprise 12+ devices, use the **Password complexity** setting.

## System security

- **Threat scan on apps**: **Require** enforces that the **Verify Apps** setting is enabled for work and personal profiles. When set to **Not configured** (default), Intune doesn't change or update this setting.

  This setting applies to:

  - Android 8 (Oreo) and newer personally owned devices with a work profile

- **Prevent app installations from unknown sources in the personal profile**: By design, Android Enterprise personally owned devices with a work profile can't install apps from sources other than the Play Store. This setting allows administrators more control of app installations from unknown sources. **Block** prevents app installations from sources other than the Google Play Store in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow app installations from unknown sources in the personal profile. By nature, personally owned devices with a work profile are intended to be dual-profile:

  - A personally owned device with a work profile managed using MDM.
  - A personal profile that's isolated from MDM management.

## Connectivity

- **Always-on VPN**: **Enable** sets a VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected. Or, immediately connect when users lock their device, the device restarts, or the wireless network changes.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable always-on VPN for all VPN clients.

  > [!IMPORTANT]
  > Be sure to deploy only one Always On VPN policy to a single device. Deploying multiple Always VPN policies to a single device isn't supported.

- **VPN client**: Choose a VPN client that supports Always On. Your options:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Custom
    - **Package ID**: Enter the package ID of the app in the Google Play store. For example, if the URL for the app in the Play store is `https://play.google.com/store/details?id=com.contosovpn.android.prod`, then the package ID is `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  >
  > - The VPN client you choose must be installed on the device. It must also support per-app VPN in personally owned devices with a work profile. Otherwise, an error occurs.
  > - You do need to approve the VPN client app in the **Managed Google Play Store**, sync the app to Intune, and deploy the app to the device. After these steps, the app is installed in the user's personally owned devices with a work profile.
  > - There might be known issues when using per-app VPN with F5 Access for Android 3.0.4. For more information, see [F5's release notes for F5 Access for Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Lockdown mode**: **Enable** forces all network traffic to use the VPN tunnel. If a connection to the VPN isn't established, then the device won't have network access.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow traffic to flow through the VPN tunnel or through the mobile network.

# [AOSP](#tab/aosp)

Android Open Source Project (AOSP) devices are Android devices that don't have Google Mobile Services (GMS) installed.

> [!NOTE]
> Device configuration profiles aren't supported on Microsoft Teams devices running AOSP.

### Device password

- **Required password type**: Require users to use a certain type of password. Your options:

  - **Device default**: To evaluate password compliance, be sure to select a password strength other than **Device default**. If you want to require users to set up a passcode on their devices, configure this setting to a more secure option.

  - **Numeric** (default): Password must only be numbers, such as `123456789`. Also enter:

    - **Minimum password length**: Enter the minimum number of digits the password must have, from 4 to 16.

  - **Numeric complex**: Doesn't permit repeat or consecutive numbers, such as `1111` or `1234`. Also enter:

    - **Minimum password length**: Enter the minimum number of digits or characters a password must have, from 4 to 16.

- **Number of sign-in failures before wiping device**: Enter the number of sign-in attempts allowed, from 4 to 11, before the device is wiped. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.

- **Maximum minutes of inactivity until screen locks**: Enter the maximum length of time, from 1 minute to 1 hour, that devices can be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of inactivity. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

> [!NOTE]
>
>- RealWear devices currently only support device default, numeric, and numeric complex password types.
>- The password type **Password required, no restrictions** appears as an option but doesn't currently work on devices, which is a known issue.

### General

- **Block access to camera**: Prevents access to the camera on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

- **Block screen capture**: Prevents screenshots or screen captures on the device. It also prevents the content from being shown on display devices that don't have a secure video output. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image.

- **Disable factory reset**: Prevents users from using the factory reset option in the device's settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow external media on the device.

- **Block mounting of external media**: Prevents users from using or connecting any external media on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to connect external media.

- **Block USB file transfer**: Prevents users from transferring files over USB. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to transfer files.

- **Block Wi-Fi setting changes**: Prevents users from creating or changing any Wi-Fi configurations. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.

- **Disable Bluetooth**: Disables Bluetooth on the device so that users can't pair with other devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable Bluetooth on the device.

- **Block Bluetooth configuration**: Prevents users from configuring Bluetooth on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to configure Bluetooth.

- **Allow users to turn on debugging features**: Permits users to access the debugging features on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from using the debugging features on the device.

- **Block users from turning on unknown sources**: Prevents users from sideloading apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to sideload apps from unknown sources.

---

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- You can also create dedicated device kiosk profiles for [Android](device-restrictions-android.md#kiosk) and [Windows](kiosk-settings.md) devices.
- [Configure and troubleshoot Android enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974).
