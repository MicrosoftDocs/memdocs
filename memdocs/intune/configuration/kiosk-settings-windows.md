---
# required metadata

title: Kiosk settings for Windows 10/11 in Microsoft Intune
description: Configure your Windows 10/11 client devices as single-app and multi-app kiosks, customize the start menu, add apps, show the task bar, and configure a web browser in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/19/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Windows 10/11 and newer device settings to run as a kiosk in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

On Windows 10/11 devices, you can configure these devices to run in single-app kiosk mode. On Windows 10 devices, you can configure these devices to run in multi-app kiosk mode.

This article describes some of the settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to configure your Windows client devices to run in kiosk mode.

As an Intune administrator, you can create and assign these settings to your devices.

To learn more about the Windows kiosk feature in Intune, see [configure kiosk settings](kiosk-settings.md).

## Before you begin

- Create a [Windows 10/11 kiosk device configuration profile](kiosk-settings.md#create-the-profile).

- This kiosk profile is directly related to the device restrictions profile you create using the [Microsoft Edge kiosk settings](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older). To summarize:

  1. Create this kiosk profile to run the device in kiosk mode.
  2. Create the [device restrictions profile](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older), and configure specific features and settings allowed in Microsoft Edge.

- Be sure that any files, scripts, and shortcuts are on the local system. For more information, including other Windows requirements, see [Customize and export Start layout](/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Be sure to assign this kiosk profile to the same devices as your [Microsoft Edge profile](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older).

## Single app, full-screen kiosk

Runs only one app on the device, such as a web browser or Store app.

- **Select a kiosk mode**: Choose **Single app, full-screen kiosk**.

- **User logon type**: Select the account type that runs the app. Your options:

  - **Auto logon (Windows 10 version 1803 and newer)**: Use on kiosks in public-facing environments that don't require the user to sign in, similar to a guest account. This setting uses the [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Local user account**: Enter the local (to the device) user account. The account you enter signs in to the kiosk.

- **Application type**: Select the application type. Your options:

  - **Add Microsoft Edge browser**: Select this option for Microsoft Edge version 87 and newer.

    > [!NOTE]
    > These settings enable the Microsoft Edge browser on the device. To configure Microsoft Edge settings, use the [Settings Catalog](settings-catalog.md), or create an [Administrative template](administrative-templates-configure-edge.md).

    - **Edge Kiosk URL**: Enter a default webpage that opens when Microsoft Edge browser opens and restarts. For example, enter `https://www.contoso.com` or `http://bing.com`.
    - **Microsoft Edge kiosk mode type**: Select the kiosk mode type. Both options help protect user data.
      - **Public Browsing (InPrivate)**: Runs a limited multi-tab version of Microsoft Edge. Users can browse publicly, or end their browsing session.
      - **Digital/Interactive Signage (InPrivate)**: Opens a URL full screen, and only shows the content on that website. [Set up digital signs](/windows/configuration/setup-digital-signage) provides more information on this feature.

    For more information on these options, see [Support policies for kiosk mode](/deployedge/microsoft-edge-configure-kiosk-mode#support-policies-for-kiosk-mode).

    - **Refresh browser after idle time**: Enter the idle time when the browser should restart, from 0-1440 minutes. The idle time is the user's last interaction.

  - **Add Microsoft Edge Legacy browser**: Select this option for Microsoft Edge version 77, and version 45 and older.

    > [!NOTE]
    > This setting enables the Microsoft Edge browser on the device.
    >
    > - To configure Microsoft Edge version 77 and newer settings, use the [Settings Catalog](settings-catalog.md), or create an [Administrative template](administrative-templates-configure-edge.md).
    > - To configure Microsoft Edge version 45 and older, create a [device restrictions profile](device-restrictions-configure.md), and [configure the settings](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older).

    - **Microsoft Edge kiosk mode type**: Select the kiosk mode type. Both options help protect user data.

      - **Digital/Interactive signage**: Opens a URL full screen, and only shows the content on that website. [Set up digital signs](/windows/configuration/setup-digital-signage) provides more information on this feature.
      - **Public browsing (InPrivate)**: Runs a limited multi-tab version of Microsoft Edge. Users can browse publicly, or end their browsing session.

    For more information on these options, see [Deploy Microsoft Edge kiosk mode](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

  - **Add Kiosk browser**: Select **Kiosk browser settings**. These settings control a web browser app on the kiosk. Be sure you get the [Kiosk browser app](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) from the Store, add it to Intune as a [Client App](../apps/apps-add.md). Then, assign the app to the kiosk devices.

    Enter the following settings:

    - **Default home page URL**: Enter the default URL shown when the kiosk browser opens, or when the browser restarts. For example, enter `http://bing.com` or `http://www.contoso.com`.

    - **Home button**: **Show** or **hide** the kiosk browser's home button. By default, the button isn't shown.

    - **Navigation buttons**: **Show** or **hide** the forward and back buttons. By default, the navigation buttons aren't shown.

    - **End session button**: **Show** or **hide** the end session button. When shown, the user selects the button, and the app prompts to end the session. When confirmed, the browser clears all browsing data (cookies, cache, and so on), and then opens the default URL. By default, the button isn't shown.

    - **Refresh browser after idle time**: Enter the amount of idle time, from 1-1440 minutes, until the kiosk browser restarts in a fresh state. Idle time is the number of minutes since the user's last interaction. By default, the value is empty or blank, which means there isn't any idle timeout.

    - **Allowed websites**: Use this setting to allow specific websites to open. In other words, use this feature to restrict or prevent websites on the device. For example, you can allow all websites at `http://contoso.com` to open. By default, all websites are allowed.

      To allow specific websites, upload a file that includes a list of the allowed websites on separate lines. If you don't add a file, all websites are allowed. By default, Intune allows all subdomains of the website. For example, you enter the `sharepoint.com` domain. Intune automatically allows all subdomains, such as `contoso.sharepoint.com`, `my.sharepoint.com`, and so on. Don't enter wildcards, such as the asterisk (`*`).

      Your sample file should look similar to the following list:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Windows 10/11 Kiosks with Autologon enabled using Microsoft Kiosk Browser must use an offline license from the Microsoft Store for Business. This requirement is because Autologon uses a local user account with no Azure Active Directory (AD) credentials. So, online licenses can't be evaluated. For more information, see [Distribute offline apps](/microsoft-store/distribute-offline-apps).

  - **Add Store app**: Select **Add a store app**, and choose an app from the list.

    Don't have any apps listed? Add some using the steps at [Client Apps](../apps/apps-add.md).

- **Specify Maintenance Window for App Restarts**: Some apps require a restart to complete the app installation, or complete the installation of updates. **Require** creates a maintenance window. If the app requires a restart, then it's restarted during this window.

  Also enter:

  - **Maintenance Window Start Time**: Select the date and time of day to begin checking clients for any app updates that require restart. The default start time is midnight, or zero minutes. If blank, then apps restart at an unscheduled time 3 days after an app update is installed.

  - **Maintenance Window Recurrence**: Default is daily. Select how often Maintenance windows for app updates take place. To avoid unscheduled app restarts, the recommendation is **Daily**.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## Multi-app kiosk

Runs multiple app on the device. Apps in this mode are available on the start menu. These apps are the only apps the user can open. If an app has a dependency on another app, then add both apps to the allowed apps list. For example, Internet Explorer 64-bit has a dependency on Internet Explorer 32-bit. So, you must allow `C:\Program Files\internet explorer\iexplore.exe` and `C:\Program Files (x86)\Internet Explorer\iexplore.exe`.

- **Select a kiosk mode**: Select **Multi app kiosk**.

- **Target Windows 10 in S mode devices**:
  - **Yes**: Allows store apps and AUMID apps in the kiosk profile. It excludes Win32 apps.
  - **No**: Allows store apps, Win32 apps, and AUMID apps in the kiosk profile. This kiosk profile isn't deployed to S-mode devices.

- **User logon type**: Select the account type that runs your apps. Your options:

  - **Auto logon (Windows 10 version 1803 and later)**: Use on kiosks in public-facing environments that don't require the user to sign in, similar to a guest account. This setting uses the [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Local user account**: **Add** the local (to the device) user account. The account you enter signs in to the kiosk.
  - **Azure AD user or group (Windows 10 version 1803 and later)**: Select **Add**, and choose Azure AD users or groups from the list. You can select multiple users and groups. Choose **Select** to save your changes.
  - **HoloLens visitor**: The visitor account is a guest account that doesn't require any user credentials or authentication, as described in [shared PC mode concepts](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser and Applications**: Add the apps to run on the kiosk device. Remember, you can add several apps.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Add browsers or apps to multi-app kiosk profile in Microsoft Intune.":::  

  - **Browsers**

    - **Add Microsoft Edge Legacy**: Select this option for Microsoft Edge version 77, and version 45 and older. Microsoft Edge is added to the app grid, and all applications can run on this kiosk. Select the **Microsoft Edge kiosk mode type**:

      - **Normal mode (full version of Microsoft Edge)**: Runs a full-version of Microsoft Edge with all browsing features. User data and state are saved between sessions.
      - **Public browsing (InPrivate)**: Runs a multi-tab version of Microsoft Edge InPrivate with a tailored experience for kiosks that run in full-screen mode.

      For more information on these options, see [Deploy Microsoft Edge kiosk mode](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > This setting enables the Microsoft Edge browser on the device.
      >
      > - To configure Microsoft Edge version 77 and newer settings, use the [Settings Catalog](settings-catalog.md), or create an [Administrative template](administrative-templates-configure-edge.md).
      > - To configure Microsoft Edge version 45 and older, create a [device restrictions profile](device-restrictions-configure.md), and [configure the settings](device-restrictions-windows-10.md#microsoft-edge-legacy-version-45-and-older).

    - **Add Kiosk browser**: These settings control a web browser app on the kiosk. Be sure you deploy a web browser app to the kiosk devices using [Client Apps](../apps/apps-add.md).

      Enter the following settings:

      - **Default home page URL**: Enter the default URL shown when the kiosk browser opens, or when the browser restarts. For example, enter `http://bing.com` or `http://www.contoso.com`.

      - **Home button**: **Show** or **hide** the kiosk browser's home button. By default, the button isn't shown.

      - **Navigation buttons**: **Show** or **hide** the forward and back buttons. By default, the navigation buttons aren't shown.

      - **End session button**: **Show** or **hide** the end session button. When shown, the user selects the button, and the app prompts to end the session. When confirmed, the browser clears all browsing data (cookies, cache, and so on), and then opens the default URL. By default, the button isn't shown.

      - **Refresh browser after idle time**: Enter the amount of idle time (1-1440 minutes) until the kiosk browser restarts in a fresh state. Idle time is the number of minutes since the user's last interaction. By default, the value is empty or blank, which means there isn't any idle timeout.

      - **Allowed websites**: Use this setting to allow specific websites to open. In other words, use this feature to restrict or prevent websites on the device. For example, you can allow all websites at `contoso.com*` to open. By default, all websites are allowed.

        To allow specific websites, upload a .csv file that includes a list of the allowed websites. If you don't add a .csv file, all websites are allowed.

      > [!NOTE]
      > Windows 10 Kiosks with Autologon enabled using Microsoft Kiosk Browser must use an offline license from the Microsoft Store for Business. This requirement is because Autologon uses a local user account with no Azure Active Directory (AD) credentials. So, online licenses can't be evaluated. For more information, see [Distribute offline apps](/microsoft-store/distribute-offline-apps).

  - **Applications**

    - **Add store app**: Add an app from the Microsoft Store for Business. If you don't have any apps listed, then you can get apps, and [add them to Intune](../apps/store-apps-windows.md). For example, you can add Kiosk Browser, Excel, OneNote, and more.

    - **Add Win32 App**: A Win32 app is a traditional desktop app, such as Visual Studio Code or Google Chrome. Enter the following properties:

      - **Application name**: Required. Enter a name for the application.
      - **Local path to app executable file**: Required. Enter the path to the executable, such as `C:\Program Files (x86)\Microsoft VS Code\Code.exe` or `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **Application user model ID (AUMID) for the Win32 app**: Enter the Application user model ID (AUMID) of the Win32 app. This setting determines the start layout of the tile on the desktop. To get this ID, see [Get-StartApps](/powershell/module/startlayout/get-startapps).

    - **Add by AUMID**: Use this option to add inbox Windows apps, such as Notepad or Calculator. Enter the following properties:

      - **Application name**: Required. Enter a name for the application.
      - **Application user model ID (AUMID)**: Required. Enter the Application user model ID (AUMID) of the Windows app. To get this ID, see [find the Application User Model ID of an installed app](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AutoLaunch**: Optional. After you add your apps and browser, select one app or browser to automatically open when the user signs in. Only a single app or browser can be autolaunched.
    - **Tile size**: Required. After you add your apps, select a Small, Medium, Wide, or Large app tile size.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Automatically launch the app or browser, and select the tile size in a multi-app kiosk profile in Microsoft Intune.":::

  > [!TIP]
  > After you add all the apps, you can change the display order by clicking-and-dragging the apps in the list.  

- **Use alternative Start layout**: Select **Yes** to enter an XML file that describes how the apps appear on the start menu, including the order of the apps. Use this option if you require more customization in your start menu. [Customize and export Start layout](/windows/configuration/customize-and-export-start-layout) has some guidance, and sample XML.

- **Windows Taskbar**: Choose to **Show** or **hide** the taskbar. By default, the taskbar isn't shown. Icons, such as the Wi-Fi icon, are shown, but the settings can't be changed by end users.

- **Allow Access to Downloads Folder**: Choose **Yes** to allow users to access the Downloads folder in Windows Explorer. By default, access to the Downloads folder is disabled. This feature is commonly used for end users to access items downloaded from a browser.

- **Specify Maintenance Window for App Restarts**: Some apps require a restart to complete the app installation, or complete the installation of updates. **Require** creates a maintenance window. If apps require a restart, then they're restarted during this window.

  Also enter:

  - **Maintenance Window Start Time**: Select the date and time of day to begin checking clients for any app updates that require restart. The default start time is midnight, or zero minutes. If blank, then apps restart at an unscheduled time 3 days after an app update is installed.

  - **Maintenance Window Recurrence**: Default is daily. Select how often Maintenance windows for app updates take place. To avoid unscheduled app restarts, the recommendation is **Daily**.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

You can also create kiosk profiles for [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience), and [Windows Holographic for Business](kiosk-settings-holographic.md) devices.

Also see [set up a single-app kiosk](/windows/configuration/kiosk-single-app) or [set up a multi-app kiosk](/windows/configuration/lock-down-windows-10-to-specific-apps) in the Windows guidance.
