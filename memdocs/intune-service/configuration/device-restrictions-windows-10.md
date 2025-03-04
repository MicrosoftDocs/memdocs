---
# required metadata

title: Device restriction settings for Windows 10/11 in Microsoft Intune
description: See a list of all the settings and their descriptions for creating device restrictions on Windows 10/11 client devices. Use these settings in a configuration profile to control screenshots, password requirements, kiosk settings, apps in the store, Microsoft Edge browser, Microsoft Defender, access to the cloud, start menu, and more in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/16/2023
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
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Windows 10/11 device settings to allow or restrict features using Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes some of the settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, set password rules, customize the lock screen, use Microsoft Defender, and more.

These settings apply to:

- Windows 11
- Windows 10

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your Windows client devices.

> [!NOTE]
> Some settings are only available on specific Windows editions, such as Enterprise. To see the supported editions, refer to the [policy CSPs](/windows/client-management/mdm/policy-configuration-service-provider) (opens another Microsoft web site).
>  
> In a Windows 10/11 device restrictions profile, most configurable settings are deployed at the device level using device groups. Policies deployed to user groups apply to targeted users. The policies also apply to users who have an Intune license, and users that sign in to that device.

## Before you begin

[Create a Windows 10/11 device restrictions profile](device-restrictions-configure.md#create-the-profile).

## App Store

These settings use the [ApplicationManagement policy CSP](/windows/client-management/mdm/policy-csp-applicationmanagement), which also lists the supported Windows editions.

- **App store (mobile only)**: **Block** prevents users from accessing the app store on mobile devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users access to the app store.
- **Auto-update apps from store**: **Block** prevents updates from being automatically installed from the Microsoft Store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps installed from the Microsoft Store to be automatically updated.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Trusted app installation**: Choose if non-Microsoft Store apps can be installed, also known as sideloading. Sideloading is installing, and then running or testing an app that isn't certified by the Microsoft Store. For example, an app that is internal to your company only. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Block**: Prevents sideloading. Non-Microsoft Store apps can't be installed.
  - **Allow**: Allows sideloading. Non-Microsoft Store apps can be installed.

- **Developer unlock**: Allow Windows developer settings, such as allowing sideloaded apps to be modified by users. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Block**: Prevents developer mode and sideloading apps.
  - **Allow**: Allows developer mode and sideloading apps.

  [Enable your device for development](/windows/uwp/get-started/enable-your-device-for-development) has more information on this feature.
  
  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Shared user app data**: Choose **Allow** to share application data between different users on the same device and with other instances of that app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent sharing data with other users and other instances of the same app.

  [ApplicationManagement/AllowSharedUserAppData CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Use private store only**: **Allow** only allows apps to be downloaded from a private store, and not downloaded from the public store, including a retail catalog. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps to be downloaded from a private store and a public store.

  [ApplicationManagement/RequirePrivateStoreOnly CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Store originated app launch**: **Block** disables all apps that were pre-installed on the device, or downloaded from the Microsoft Store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these apps to open.

  [ApplicationManagement/DisableStoreOriginatedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Install app data on system volume**: **Block** stops apps from storing data on the system volume of the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps to store data on the system disk volume.

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Install apps on system drive**: **Block** prevents apps from installing on the system drive on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps to install on the system drive.

  [ApplicationManagement/RestrictAppToSystemVolume CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (desktop only)**: **Block** disables Windows Game recording and broadcasting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow recording and broadcasting of games.

  [ApplicationManagement/AllowGameDVR CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Apps from store only**: This setting determines the user experience when users install apps from places other than the Microsoft Store. It doesn't prevent installation of content from USB devices, network shares, or other non-internet sources. Use a trustworthy browser to help make sure these protections work as expected.

  Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to install apps from places other than the Microsoft Store, including apps defined in other policy settings.  
  - **Anywhere**: Turns off app recommendations, and allows users to install apps from any location.  
  - **Store Only**: Intent is to prevent malicious content from affecting your user devices when downloading executable content from the internet. When users try to install apps from the internet, the installation is blocked. Users see a message recommending they download apps from the Microsoft Store.
  - **Recommendations**: When installing an app from the web that's available in the Microsoft Store, users see a message recommending they download it from the store.  
  - **Prefer Store**: Warns users when they install apps from places other than the Microsoft Store.

  [SmartScreen/EnableAppInstallControl CSP](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **User control over installations**: **Block** prevents users from changing the installation options typically reserved for system administrators, such as entering the directory to install the files. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, Windows Installer might prevent users from changing these installation options, and some of the Windows Installer security features are bypassed.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Install apps with elevated privileges**: **Block** directs Windows Installer to use elevated permissions when it installs any program on the system. These privileges are extended to all programs. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the system might apply the current user's permissions when it installs programs that a system administrator doesn't deploy or offer.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Startup apps**: Enter a list of apps to open after a user signs in to the device. Be sure to use a semi-colon delimited list of Package Family Names (PFN) of Windows applications. For this policy to work, the manifest in the Windows apps must use a startup task.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## Cellular and Connectivity

These settings use the [connectivity policy](/windows/client-management/mdm/policy-csp-connectivity) and [Wi-Fi policy](/windows/client-management/mdm/policy-csp-wifi) CSPs, which also list the supported Windows editions.

- **Cellular data channel**: Choose if users can use data, like browsing the web, when connected to a cellular network. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. users can turn it off.
  - **Block**: Don't allow the cellular data channel. Users can't turn it on.
  - **Allow (not editable)**: Allows the cellular data channel. Users can't turn it off.

- **Data roaming**: **Block** prevents cellular data roaming on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, when accessing data, roaming between networks might be allowed.
- **VPN over the cellular network**: **Block** prevents the device from accessing VPN connections when connected to a cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow VPN to use any connection, including cellular.
- **VPN roaming over the cellular network**: **Block** stops the device from accessing VPN connections when roaming on a cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow VPN connections when roaming.
- **Connected devices service**: **Block** disables the Connected Devices Platform (CDP) component. CDP enables discovery and connection to other devices (through Bluetooth/LAN or the cloud) to support remote app launching, remote messaging, remote app sessions, and other cross-device experiences. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the connected devices service, which enables discovery and connection to other Bluetooth devices.
- **NFC**: **Block** prevents near field communications (NFC) capabilities. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to enable and configure NFC features on the device.
- **Wi-Fi**: **Block** prevents users from and enabling, configuring, and using Wi-Fi connections on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Wi-Fi connections.
- **Automatically connect to Wi-Fi hotspots**: **Block** prevents devices from automatically connecting to Wi-Fi hotspots. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let devices automatically connect to free Wi-Fi hotspots, and automatically accept any terms and conditions for the connection.
- **Manual Wi-Fi configuration**: **Block** prevents devices from connecting to Wi-Fi outside of MDM server-installed networks. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add and configure their own Wi-Fi connections network SSIDs.
- **Wi-Fi scan interval**: Enter how often devices scan for Wi-Fi networks. Enter a value from 1 (most frequent) to 500 (least frequent). Default is `0` (zero).

### Bluetooth

These settings use the [Bluetooth policy CSP](/windows/client-management/mdm/policy-csp-bluetooth), which also lists the supported Windows editions.

- **Bluetooth**: **Block** prevents users from enabling Bluetooth. **Not configured** (default) allows Bluetooth on the device.
- **Bluetooth discoverability**: **Block** prevents the device from being discoverable by other Bluetooth-enabled devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow other Bluetooth-enabled devices, such as a headset, to discover the device.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth pre-pairing**: **Block** prevents specific Bluetooth devices to automatically pair with a host device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow automatic pairing with the host device.

  [Bluetooth/AllowPrepairing CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Bluetooth advertising**: **Block** prevents the device from sending out Bluetooth advertisements. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device to send out Bluetooth advertisements.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Bluetooth proximal connections**: **Block** prevents a device user from using Swift Pair and other proximity based scenarios. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device to send out Bluetooth advertisements.

  [Bluetooth/AllowPromptedProximalConnections CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Bluetooth allowed services**: **Add** a list of allowed Bluetooth services and profiles as hex strings, such as `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [ServicesAllowedList usage guide](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) has more information on the service list.

  [Bluetooth/ServicesAllowedList CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## Cloud and Storage

These settings use the [accounts policy CSP](/windows/client-management/mdm/policy-csp-accounts), which also lists the supported Windows editions.

> [!IMPORTANT]
>
> Blocking or disabling these Microsoft account settings can impact enrollment scenarios that require users to sign in to Microsoft Entra ID. For example, you're using [Autopilot pre-provisioned](/autopilot/pre-provision). Typically, users are shown a Microsoft Entra sign-in window. When these settings are set to **Block** or **Disable**, the Microsoft Entra sign-in option may not show. Instead, users are asked to accept the EULA, and create a local account, which may not be what you want.

- **Microsoft account**: **Block** prevents users from associating a Microsoft account with the device. **Block** may also affect some enrollment scenarios that rely on users to complete the enrollment process. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow adding and using a Microsoft account.
- **Non-Microsoft account**: **Block** prevents users from adding non-Microsoft accounts using the user interface. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add email accounts that aren't associated with a Microsoft account.
- **Settings synchronization for Microsoft account**: **Block** prevents device and app settings associated with a Microsoft account to synchronize between devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this synchronization.
- **Microsoft Account sign-in assistant**: This OS service allows users to sign in to their Microsoft account. By default, the OS might allow users to start and stop the **Microsoft Account Sign-In Assistant** (wlidsvc) service.
  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to start and stop the **Microsoft Account Sign-In Assistant** (wlidsvc) service.
  - **Disabled**: Sets the Microsoft Sign-in Assistant service (wlidsvc) to Disabled, and prevents users from manually starting it.

      **Disable** may also affect some enrollment scenarios that rely on users to complete the enrollment. For example, you're using [Autopilot pre-provisioned](/autopilot/pre-provision). Typically, users are shown a Microsoft Entra sign-in window. When set to **Disable**, the Microsoft Entra sign-in option may not show. Instead, users are asked to accept the EULA, and create a local account, which may not be what you want.

## Cloud Printer

These settings use the [EnterpriseCloudPrint policy CSP](/windows/client-management/mdm/policy-csp-enterprisecloudprint), which also lists the supported Windows editions.

- **Printer discovery URL**: Enter the URL for finding cloud printers. For example, enter `https://cloudprinterdiscovery.contoso.com`.
- **Printer access authority URL**: Enter the authentication endpoint URL to get OAuth tokens. For example, enter `https://azuretenant.contoso.com/adfs`.
- **Azure native client app GUID**: Enter the GUID of a client application allowed to get OAuth tokens from the OAuthAuthority. For example, enter `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **Print service resource URI**: Enter the OAuth resource URI for print service configured in the Azure portal. For example, enter `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Maximum printers to query**: Enter the maximum number of printers that you want to be queried. The default value is `20`.
- **Printer discovery service resource URI**: Enter the OAuth resource URI for printer discovery service configured in the Azure portal. For example, enter `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> After you setup a [Windows Server Hybrid Cloud Print](/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview), you can configure these settings, and then deploy to your Windows devices.

## Control Panel and Settings

- **Settings app**: **Block** prevents users from accessing to the Windows settings app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to open the Settings app on the device.
  - **System**: **Block** prevents access to the System area of the Settings app. When set to **Not configured** (default), Intune doesn't change or update this setting.
    - **Power and sleep settings modification** (desktop only): **Block** prevents users from changing the power and sleep settings on the device. **Not configured** (default) allows users to change power and sleep settings.
  - **Devices**: **Block** prevents access to the Devices area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Network Internet**: **Block** prevents access to the Network & Internet area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Personalization**: **Block** prevents access to the Personalization area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Apps**: **Block** prevents access to the Apps area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Accounts**: **Block** prevents access to the Accounts area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Time and Language**: **Block** prevents access to the Time & Language area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
    - **System Time modification**: **Block** prevents users from changing the date and time settings on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. Users can change these settings.
    - **Region settings modification** (desktop only): **Block** prevents users from changing the region settings on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. Users can change these settings.
    - **Language settings modification (desktop only)**: **Block** prevents users from changing the language settings on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. Users can change these settings.

      [Settings policy CSP](/windows/client-management/mdm/policy-csp-settings)

  - **Gaming**: When set to **Block**, this setting:
  
    - Prevents access to the **Settings** app > **Gaming** area on the device. 
    - On Windows 11 22H2 and later, it hides the **Settings** app > **System** > **Notifications** area on the device. Specifically, it adds the `ms-settings:quietmomentsgame` page to the [Settings/PageVisibilityList CSP](/windows/client-management/mdm/policy-csp-settings#settings-pagevisibilitylist).

    When set to **Not configured** (default), Intune doesn't change or update this setting.
    
  - **Ease of Access**: **Block** prevents access to the Ease of Access area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Privacy**: **Block** prevents access to the Privacy area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Update and Security**: **Block** prevents access to the Update & Security area of the Settings app on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Display

These settings use the [display policy CSP](/windows/client-management/mdm/policy-csp-display), which also lists the supported Windows editions.

GDI DPI scaling enables applications that aren't DPI aware to become per monitor DPI aware.

- **Turn on GDI scaling for apps**: **Add** the legacy apps that you want GDI DPI scaling turned on. For example, enter `filename.exe` or `%ProgramFiles%\Path\Filename.exe`.

  GDI DPI scaling is turned on for all legacy applications in your list.

- **Turn off GDI scaling for apps**: **Add** the legacy apps that you want GDI DPI scaling turned off. For example, enter `filename.exe` or `%ProgramFiles%\Path\Filename.exe`.

  GDI DPI scaling is turned off for all legacy applications in your list.

You can also **Import** a .csv file with the list of apps.

## General

These settings use the [experience policy CSP](/windows/client-management/mdm/policy-csp-experience), which also lists the supported Windows editions. 

- **Screen capture** (mobile only): **Block** prevents users from getting screenshots on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Copy and paste (mobile only)**: **Block** prevents users from using copy-and-paste between apps on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Manual unenrollment**: **Block** prevents users from deleting the workplace account using the workplace control panel on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  This policy setting doesn't apply if the computer is Microsoft Entra joined and auto-enrollment is enabled.

- **Manual root certificate installation** (mobile only): **Block** prevents users from manually installing root certificates, and intermediate CAP certificates. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Camera**: **Block** prevents users from using the camera on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the device camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

  [Camera CSP](/windows/client-management/mdm/policy-csp-camera)

- **OneDrive file sync**: **Block** prevents users from synchronizing files to OneDrive from the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [System/DisableOneDriveFileSync CSP](/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Removable storage**: **Block** prevents users from using external storage devices, like USB drives or SD cards with the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [System/AllowStorageCard CSP](/windows/client-management/mdm/policy-csp-system#system-allowstoragecard)

- **Geolocation**: **Block** prevents users from turning on location services on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [System/AllowLocation CSP](/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Internet sharing**: **Block** prevents Internet connection sharing on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Phone reset**: **Block** prevents users from wiping or doing a factory reset on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **USB connection**: **Block** prevents access to syncing files through a USB connection or using developer tools on a HoloLens device. Changing this policy doesn't affect USB charging. When set to **Not configured** (default), Intune doesn't change or update this setting. USB charging isn't affected by this setting.

  [Connectivity/AllowUSBConnection CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **AntiTheft mode** (mobile only): **Block** prevents users from selecting AntiTheft mode preference on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Cortana**: **Block** disables the Cortana voice assistant on the device. When Cortana is off, users can still search to find items on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Cortana.

  [Experience/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

  [!INCLUDE [cortana-app-deprecation](../includes/cortana-app-deprecation.md)]

- **Voice recording** (mobile only): **Block** prevents users from using the device voice recorder on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow voice recording for apps.
- **Device name modification** (mobile only): **Block** prevents users from changing the name of the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Add provisioning packages**: **Block** prevents the run time configuration agent that installs provisioning packages on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Remove provisioning packages**: **Block** prevents the run time configuration agent that removes provisioning packages from the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Device discovery**: **Block** prevents the device from being discovered by other devices. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Experience/AllowDeviceDiscovery](/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Task Switcher** (mobile only): **Block** prevents task switching on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **SIM card error dialog** (mobile only): **Block** error messages from showing on the device if no SIM card is detected. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the error messages.
- **Ink Workspace**: Choose if and how user access the ink workspace. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might turn on the ink workspace, and users are allowed to use it above the lock screen.
  - **Disabled on lock screen**: The ink workspace is enabled and feature is turned on. But, users can't access it above the lock screen.
  - **Disabled**: Access to ink workspace is disabled. The feature is turned off.

  [WindowsInkWorkspace policy CSP](/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Autopilot Reset**: Choose **Allow** so users with administrative rights can delete all user data and settings using **CTRL + Win + R** at the device lock screen. The device is automatically reconfigured and re-enrolled into management. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent this feature.
- **Require users to connect to network during device setup**: Choose **Require** so the device connects to a network before going past the Network page during Windows setup. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to go past the Network page, even if it's not connected to a network.

  The setting becomes effective the next time the device is wiped or reset. Like any other Intune configuration, the device must be enrolled and managed by Intune to receive configuration settings. But once it's enrolled, and receiving policies, then resetting the device enforces the setting during the next Windows setup.

  [TenantLockdown CSP](/windows/client-management/mdm/tenantlockdown-csp)

- **Direct Memory Access**: **Block** prevents direct memory access (DMA) for all hot pluggable PCI downstream ports until a user signs into Windows. **Enabled** (default) allows access to DMA, even when a user isn't signed in.

  [DataProtection/AllowDirectMemoryAccess CSP](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **End processes from Task Manager**: This setting determines whether non-administrators can use Task Manager to end tasks. **Block** prevents standard users (non-administrators) from using Task Manager to end a process or task on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow standard users to end a process or task using Task Manager.

  [TaskManager/AllowEndTask CSP](/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## Locked screen experience

- **Action center notifications (mobile only)**: **Block** prevents Action Center notifications from showing on the device lock screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to choose which apps show notifications on the lock screen.

  [AboveLock/AllowActionCenterNotifications CSP](/windows/client-management/mdm/policy-configuration-service-provider#AboveLock_AllowActionCenterNotifications)

- **Locked screen picture URL (desktop only)**: Enter the URL to a picture in JPG, JPEG, or PNG format that's used as the Windows lock screen wallpaper. For example, enter `https://contoso.com/image.png`. This setting locks the image, and can't be changed afterwards.

  [Personalization/LockScreenImageUrl CSP](/windows/client-management/mdm/personalization-csp)

- **User configurable screen timeout (mobile only)**: **Allow** lets users configure the screen timeout. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not give users this option.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana on locked screen** (desktop only): **Block** prevents users from interacting with Cortana when the device is on the lock screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow interaction with Cortana.

  [AboveLock/AllowCortanaAboveLock CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Toast notifications on locked screen**: **Block** prevents toast notifications from showing on the device lock screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these notifications.

  [AboveLock/AllowToasts CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Screen timeout (mobile only)**: Set the duration (in seconds) from the screen locking to the screen turning off. Supported values are 11-1800. For example, enter `300` to set this timeout to 5 minutes.

  [DeviceLock/ScreenTimeoutWhileLocked CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_ScreenTimeoutWhileLocked)

## Messaging

These settings use the [messaging policy CSP](/windows/client-management/mdm/policy-csp-messaging), which also lists the supported Windows editions.

- **Message sync (mobile only)**: **Block** disables text messages from being backed up and restored, and from syncing messages between Windows devices. Disabling helps avoid information being stored on servers outside of the organization's control. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these settings, and sync their messages.
- **MMS (mobile only)**: **Block** disables MMS send and receive functionality on the device. For enterprises, use this policy to disable MMS on devices as part of the auditing or management requirement. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow MMS send and receive.
- **RCS (mobile only)**: **Block** disables Rich Communication Services (RCS) send and receive functionality on the device. For enterprises, use this policy to disable RCS on devices as part of the auditing or management requirement. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow RCS send and receive.

## Microsoft Edge Legacy (Version 45 and older)

These settings use the [browser policy CSP](/windows/client-management/mdm/policy-csp-browser), which also lists the supported Windows editions.

> [!NOTE]
> Using the browser policy CSP applies to Microsoft Edge version 45 and older. For Microsoft Edge version 77 and newer, see [Configure Microsoft Edge policy settings in Microsoft Intune](administrative-templates-configure-edge.md).

### Use Microsoft Edge kiosk mode

The available settings change depending on what you choose. Your options:

- **No** (default): Microsoft Edge isn't running in kiosk mode. All Microsoft Edge settings are available for you to change and configure.
- **Digital/Interactive signage (single app kiosk)**: Filters Microsoft Edge settings that apply to Digital/Interactive signage Microsoft Edge Kiosk mode on Windows 10/11 single-app kiosks. Choose this setting to open a URL full screen, and only show the content on that website. [Set up digital signs](/windows/configuration/setup-digital-signage) provides more information on this feature.
- **InPrivate Public browsing (single app kiosk)**: Filters Microsoft Edge settings that are applicable for InPrivate Public Browsing Microsoft Edge Kiosk mode for use on Windows 10/11 single-app kiosks. Runs a multi-tab version of Microsoft Edge.
- **Normal mode (multi-app kiosk)**: Filters Microsoft Edge settings that are applicable for Normal Microsoft Edge Kiosk mode. Runs a full-version of Microsoft Edge with all browsing features.
- **Public browsing (multi-app kiosk)**: Filters Microsoft Edge settings that are applicable for Public browsing on a Windows 10 multi-app kiosk.  Runs a multi-tab version of Microsoft Edge InPrivate.

> [!TIP]
> For more information on what these options do, see [Microsoft Edge kiosk mode configuration types](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

This device restrictions profile is directly related to the kiosk profile you create using the [Windows kiosk settings](kiosk-settings-windows.md). To summarize:

1. Create the [Windows kiosk settings](kiosk-settings-windows.md) profile to run the device in kiosk mode. Select Microsoft Edge as the application and set the Microsoft Edge Kiosk Mode in the Kiosk profile.
2. Create the device restrictions profile described in this article, and configure specific features and settings allowed in Microsoft Edge. Be sure to choose the same Microsoft Edge kiosk mode type as selected in your kiosk profile ([Windows kiosk settings](kiosk-settings-windows.md)). 

    [Supported kiosk mode settings](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) is a great resource.

> [!IMPORTANT] 
> Be sure to assign this Microsoft Edge profile to the same devices as your kiosk profile ([Windows kiosk settings](kiosk-settings-windows.md)).

[ConfigureKioskMode CSP](/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### Start experience

- **Start Microsoft Edge with**: Choose which pages open when Microsoft Edge starts. Your options:
  - **Custom start pages**: Enter the start pages, such as `http://www.contoso.com`. Microsoft Edge loads the start pages you enter.
  - **New Tab page**: Microsoft Edge load whatever is entered in the **New Tab URL** setting.
  - **Last session's page**: Microsoft Edge loads the last session page.
  - **Start pages in local app settings**: Microsoft Edge start with the default start page defined by the OS.

- **Allow user to change start pages**: **Yes** (default) lets users change the start pages. Administrators can use the `EdgeHomepageUrls` to enter the start pages that users see by default when open Microsoft Edge. **No** blocks users from changing the start pages.
- **Allow web content on new tab page​**: When set to **Yes** (default), Microsoft Edge opens the URL entered in the **New Tab URL** setting. If the **New Tab URL** setting is blank, Microsoft Edge opens the new tab page listed in Microsoft Edge settings. Users can change it. When set to **No**, Microsoft Edge opens a new tab with a blank page. Users can't change it.​​
- **New Tab URL**: Enter the URL to open on the New Tab page. For example, enter `https://www.bing.com` or `https://www.contoso.com`.

- **Home button**: Choose what happens when the home button is selected. Your options:
  - **Start pages**: Opens the option you chose in the **Start Microsoft Edge with** setting
  - **New Tab page**: Opens the URL you entered in the **New Tab URL** setting.
  - **Home button URL**: Enter the URL to open. For example, enter `https://www.bing.com` or `https://www.contoso.com`.
  - **Hide Home button**: Hides the home button
- **Allow users to change home button**: **Yes** lets users change the home button. User changes override any administrator settings to the home button.​ **No** (default) blocks users from changing how the administrator configured the home button.
- **Show First Run Experience page (Mobile only)**: **Yes** (default) shows the first use introduction page in Microsoft Edge. **No** stops the introduction page from showing the first time you run Microsoft Edge. This feature allows enterprises, such as organizations enrolled in zero emissions configurations, to block this page.
- **First Run Experience URL list location** (Windows 10 Mobile only): Enter the URL that points to the XML file containing the first run page URL(s). For example, enter `https://www.contoso.com/sites.xml`.

- **Refresh browser after idle time**: Enter the number of idle minutes until the browser is refreshed, from 0-1440 minutes. Default is `5` minutes. When set to `0` (zero), the browser doesn't refresh after being idle.

  This setting is only available when running in [InPrivate Public browsing (single-app kiosk)](#use-microsoft-edge-kiosk-mode).

- **Allow pop-ups** (desktop only): **Yes** (default) allows pop-ups in the web browser. **No** prevents pop-up windows in the browser.
- **Send intranet traffic to Internet Explorer** (Desktop only): **Yes** lets users open intranet websites in Internet Explorer instead of Microsoft Edge. This setting is for backwards compatibility. **No** (default) allows users to use Microsoft Edge.
- **Enterprise mode site list location** (Desktop only): Enter the URL that points to the XML file containing a list of web sites that open in Enterprise mode. Users can't change this list. For example, enter `https://www.contoso.com/sites.xml`.
- **Message when opening sites in Internet Explorer**: Use this setting to configure Microsoft Edge to show a notification before a site opens in Internet Explorer 11. Your options:
  - **Don't show message**: The OS default behavior is used, which may not show a message.
  - **Show message that site is opened in Internet Explorer 11**: Show the message when opening sites in IE. Sites open in IE. 
  - **Show message with option to open sites in Microsoft Edge**: Show the message when opening sites in Microsoft Edge. The message includes a **Keep going in Microsoft Edge** link so users can choose Microsoft Edge instead of IE.

  > [!IMPORTANT]
  > This setting requires you to use the **Enterprise mode site list location** setting, the **Send intranet traffic to Internet Explorer** setting, or both settings.

- **Allow Microsoft compatibility list**: **Yes** (default) allows using a Microsoft compatibility list. **No** prevents the Microsoft compatibility list in Microsoft Edge. This list from Microsoft helps Microsoft Edge properly display sites with known compatibility issues.
- **Preload start pages and New Tab page**: **Yes** (default) uses the OS default behavior, which may be to preload these pages. Preloading minimizes the time to start Microsoft Edge, and load new tabs. **No** prevents Microsoft Edge from preloading start pages and the new tab page.
- **Prelaunch Start pages and New Tab page**: **Yes** (default) uses the OS default behavior, which may be to prelaunch these pages. Pre-launching helps the performance of Microsoft Edge, and minimizes the time required to start Microsoft Edge. **No** prevents Microsoft Edge from pre-launching the start pages and new tab page.

### Favorites and search

- **Show Favorites bar**: Choose what happens to the favorites bar on any Microsoft Edge page. Your options:
  - **On Start and new Tab pages**: Shows the favorites bar when Microsoft Edge starts, and on all Tab pages. Users can change this setting.
  - **On all pages**: Shows the favorites bar on all pages. Users can't change this setting.
  - **Hidden**: Hides the favorites bar on all pages. Users can't change this setting.
- **Allow changes to favorites**: **Yes** (default) uses the OS default, which allows users to change the list. **No** prevents users from adding, importing, sorting, or editing the Favorites list.
  - **Favorites List**: Add a list of URLs to the favorites file. For example, add `http://contoso.com/favorites.html`.
- **Sync favorites between Microsoft browsers** (Desktop only): **Yes** forces Windows to synchronize favorites between Internet Explorer and Microsoft Edge. Additions, deletions, modifications, and order changes to favorites are shared between browsers.  **No** (default) uses the OS default, which may give users the choice to sync favorites between the browsers.
- **Default search engine**: Choose the default search engine on the device. Users can change this value at any time. Your options:
  - Search engine in client Microsoft Edge settings
  - Bing
  - Google
  - Yahoo
  - Custom value: In **OpenSearch Xml URL**, enter an HTTPS URL with the XML file that includes the short name and the URL to the search engine, at minimum. For example, enter `https://www.contoso.com/opensearch.xml`.
- **Show search suggestions**: **Yes** (default) lets your search engine suggest sites as you type search phrases in the address bar. **No** prevents this feature.
- **Allow changes to search engine**: **Yes** (default) allows users to add new search engines, or change the default search engine in Microsoft Edge. Choose **No** to prevent users from customizing the search engine.

  This setting is only available when running in [Normal mode (multi-app kiosk)](#use-microsoft-edge-kiosk-mode).

### Privacy and security

- **Allow InPrivate browsing**: **Yes** (default) allows InPrivate browsing in Microsoft Edge. After closing all InPrivate tabs, Microsoft Edge deletes the browsing data from the device. **No** prevents users from opening InPrivate browsing sessions.
- **Save browsing history**: **Yes** (default) allow saving the browsing history in Microsoft Edge. **No** prevents saving the browsing history.
- **Clear browsing data on exit** (desktop only): **Yes** clears the history, and browsing data when users exit Microsoft Edge. **No** (default) uses the OS default, which may cache the browsing data.
- **Sync browser settings between user's devices**: Choose how you want to sync browser settings between devices. Your options:
  - **Allow**: Allow syncing of Microsoft Edge browser settings between user's devices
  - **Block and enable user override**: Block syncing of Microsoft Edge browser settings between user's devices. Users can override this setting. When this option is selected, users can override the admin designation.
  - **Block**: Block syncing of Microsoft Edge browser setting between users devices. Users can't override this setting.

- **Allow Password Manager**: **Yes** (default) allows Microsoft Edge to automatically use Password Manager, which allows users to save and manage passwords on the device. **No** prevents Microsoft Edge from using Password Manager.
- **Cookies**: Choose how cookies are handled in the web browser. Your options:
  - **Allow**: Cookies are stored on the device.
  - **Block all cookies**: Cookies aren't stored on the device.
  - **Block only third party cookies**: Third party or partner cookies aren't stored on the device.
- **Allow Autofill in forms**: **Yes** (default) allows users to change autocomplete settings in the browser, and populate form fields automatically. **No** disables the Autofill feature in Microsoft Edge.
- **Send do-not-track headers**: **Yes** sends do-not-track headers to websites requesting tracking info (recommended). **No** (default) doesn't send headers that allow websites to track the user. Users can configure this setting.
- **Show WebRTC localhost IP address**: **Yes** (default) allows users' localhost IP address to be shown when making phone calls using this protocol. **No** prevents users' localhost IP address from being shown. 
- **Allow live tile data collection**: **Yes** (default) allows Microsoft Edge to collect information from Live Tiles pinned to the start menu. **No** prevents collecting this information, which may provide users with a limited experience.
- **User can override certificate errors**: **Yes** (default) allows users to access websites that have Secure Sockets Layer/Transport Layer Security (SSL/TLS) errors. **No** (recommended for increased security) prevents users from accessing websites with SSL or TLS errors.

### Additional

- **Allow Microsoft Edge browser** (mobile only): **Yes** (default) allows using the Microsoft Edge web browser on the mobile device. **No** prevents using Microsoft Edge on devices. If you choose **No**, the other individual settings only apply to desktop.
- **Allow address bar dropdown**: **Yes** (default) allows Microsoft Edge to show the address bar drop-down with a list of suggestions. **No** stops Microsoft Edge from showing a list of suggestions in a drop-down list when you type. When set to **No**, you:
  - Help minimize network bandwidth between Microsoft Edge and Microsoft services.
  - Disable the **Show search and site suggestions as I type** in Microsoft Edge > Settings.
- **Allow full screen mode**: **Yes** (default) allows Microsoft Edge to use fullscreen mode, which shows only the web content and hides the Microsoft Edge UI. **No** prevents fullscreen mode in Microsoft Edge.
- **Allow about flags page**: **Yes** (default) uses the OS default, which may allow accessing the `about:flags` page. The `about:flags` page allows users to change developer settings and enable experimental features. **No** prevents users from accessing the `about:flags` page in Microsoft Edge.
- **Allow developer tools**: **Yes** (default) allows users to use the F12 developer tools to build and debug web pages by default. **No** prevents users from using the F12 developer tools.
- **Allow JavaScript**: **Yes** (default) allows scripts, such as JavaScript, to run in the Microsoft Edge browser. **No** prevents Java scripts in the browser from running.
- **User can install extensions**: **Yes** (default) allows users to install Microsoft Edge extensions on devices. **No** prevents the installation.
- **Allow sideloading of developer extensions**: **Yes** (default) uses the OS default, which may allow sideloading. Sideloading installs and runs unverified extensions. **No** prevents Microsoft Edge from sideloading using the **Load extensions** feature. It doesn't prevent sideloading extensions using other ways, such as PowerShell.
- **Required extensions**: Choose which extensions can't be turned off by users in Microsoft Edge. Enter the package family names, and select **Add**. [Find a package family name (PFN) for per app VPN](/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) provides some guidance.

  You can also **Import** a CSV file that includes the package family names. Or, **Export** the package family names you enter.

## Network proxy

These settings use the [NetworkProxy policy CSP](/windows/client-management/mdm/networkproxy-csp), which also lists the supported Windows editions.

- **Automatically detect proxy settings**: **Block** disables devices from automatically detecting a proxy auto config (PAC) script. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable this feature, and devices try to find the path to a PAC script.

  When set to **Block**, the **ProxySettingsPerUser** setting is automatically set to `0`.  

- **Use proxy script**: Choose **Allow** to enter a path to your PAC script to configure the proxy server. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not let you enter the URL to a PAC script.
  - **Setup script address URL**: Enter the URL of a PAC script you want to use to configure the proxy server.
- **Use manual proxy server**: Choose **Allow** to manually enter the  name or IP address, and TCP port number of a proxy server. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not let you manually enter details of a proxy server.
  - **Address**: Enter the name, or IP address of the proxy server.
  - **Port number**: Enter the port number of your proxy server.
  - **Proxy exceptions**: Enter any URLs that must not use the proxy server. Use a semicolon (`;`) to separate each item.
  - **Bypass proxy server for local address**: **Allow** doesn't use the proxy server for local intranet addresses. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might use a proxy server for local addresses on your intranet.

## Password

These settings use the [DeviceLock policy CSP](/windows/client-management/mdm/policy-csp-devicelock), which also lists the supported Windows editions.

- **Password**: **Require** forces users to enter a password to access the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to devices without a password. Applies to local accounts only. Domain account passwords remain configured by Active Directory (AD) and Microsoft Entra ID.

  [DeviceLock/DevicePasswordEnabled CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Required password type**: Choose the type of password. Your options:
    - **Not configured**: Intune doesn't change or update this setting. By default, the OS might allow the password to include numbers and letters.
    - **Alphanumeric**: Password must be a mix of numbers and letters.
    - **Numeric**: Password must only be numbers.

    [DeviceLock/AlphanumericDevicePasswordRequired CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Minimum password length**: Enter the minimum number of characters required, from 4-16. For example, enter `6` to require at least six characters in the password length. By default, the OS might set it to `4`.
  
    [DeviceLock/MinDevicePasswordLength CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > When the password requirement is changed on a Windows desktop, users are impacted the next time they sign in, as that's when devices goes from idle to active. Users with passwords that meet the requirement are still prompted to change their passwords.

  - **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, up to 11. The valid number you enter depends on the edition. [DeviceLock/MaxDevicePasswordFailedAttempts CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) lists the supported values. `0` (zero) may disable the device wipe functionality.

    This setting also has a different impact depending on the edition. For specific details on this setting, see the [DeviceLock/MaxDevicePasswordFailedAttempts CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Maximum minutes of inactivity until screen locks**: Enter the length of time a device must be idle before the screen is locked. For example, enter `5` to lock devices after 5 minutes of being idle. When set to **Not configured**, Intune doesn't change or update this setting. By default, the OS might set it to `0` (zero), which is no timeout.

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Password expiration (days)**: Enter the length of time in days when the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the value is blank, Intune doesn't change or update this setting. By default, the OS might set it to `0` (zero), which is no expiration.

    [DeviceLock/DevicePasswordExpiration CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Prevent reuse of previous passwords**: Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.

    [DeviceLock/DevicePasswordHistory CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Require password when device returns from idle state** (Mobile and Holographic): **Require** forces users to enter a password to unlock the device after being idle. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require a PIN or password after being idle.

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Simple passwords**: **Block** prevents users from creating simple passwords, such as `1234` or `1111`. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users create simple passwords. This setting also blocks using picture passwords.

    [DeviceLock/AllowSimpleDevicePassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Automatic encryption during AADJ**: **Block** prevents automatic BitLocker device encryption when devices are prepared for first use, and when devices are Microsoft Entra joined. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable encryption.

  More on [BitLocker device encryption](/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices CSP](/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Federal Information Processing Standard (FIPS) policy**: **Allow** uses the Federal Information Processing Standard (FIPS) policy, which is a U.S. government standard for encryption, hashing, and signing. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not allow FIPS.

  [Cryptography/AllowFipsAlgorithmPolicy CSP](/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello device authentication**: **Allow** users to use a Windows Hello companion device, such as a phone, fitness band, or IoT device, to sign in to a Windows 10/11 computer. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent Windows Hello companion devices from authenticating.

  [Authentication/AllowSecondaryAuthenticationDevice CSP](/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Preferred Microsoft Entra tenant domain**: Enter an existing domain name in your Microsoft Entra organization. When users in this domain sign in, they don't have to type the domain name. For example, enter `contoso.com`. Users in the `contoso.com` domain can sign in using their user name, such as `abby`, instead of `abby@contoso.com`.

  [Authentication/PreferredAadTenantDomainName CSP](/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## Per-app privacy exceptions

**Add** apps that should have a different privacy behavior from what you define in "Default privacy".

- **Package Name**: App package family name.
- **App Name**: The name of the app.

### Exceptions

- **Account information**: Define whether this app can access the user name, picture, and other contact info.
- **Background apps**: Define whether this app can run in the background.
- **Calendar**: Define whether this app can access the calendar.
- **Call history**: Define whether this app can access my call history.
- **Camera**: Define whether this app can access the camera.
- **Contacts**: Define whether this app can access contacts.
- **Email**: Define whether this app can access and send email.
- **Location**: Define whether this app can access location information.
- **Messaging**: Define whether this app can read or send text or MMS messages.
- **Microphone**: Define whether this app can use the microphone.
- **Motion**: Define whether this app can access device motion information.
- **Notifications**: Define whether this app can access notifications.
- **Phone**: Define whether this app can access the phone.
- **Radios**: Some apps use radios (for example, Bluetooth) in your device to send and receive data and need to turn these radios on or off. Define whether this app can control these radios.
- **Tasks**: Define whether this app can access your tasks.
- **Trusted devices**: Choose if this app can use trusted devices. Trusted devices are hardware you've already connected, or hardware that comes with device. For example, use TVs, projectors, and so on, as trusted devices.
- **Feedback and diagnostics**: Define whether this app can access diagnostic information.
- **Sync with devices**: Choose if this app can automatically share and sync information with wireless devices that don't explicitly pair with the device.

## Personalization

These settings use the [personalization policy CSP](/windows/client-management/mdm/personalization-csp), which also lists the supported Windows editions.

- **Desktop background picture URL (Desktop only)**: Enter the URL to a picture in .jpg, .jpeg or .png format that you want to use as the Windows desktop wallpaper. Users can't change the picture. For example, enter `https://contoso.com/logo.png`.

  When left blank, Intune doesn't change or update this setting.

## Printer

- **Printers**: Add printers using their network host names (DNS name). The OS searches and installs matching printer drivers for each printer on the device. If you don't enter a value, Intune doesn't change or update this setting.

  [Education/PrinterNames CSP](/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Default printer**: Enter the network host name (DNS name) of an installed printer to use as the default printer. If you don't enter a value, Intune doesn't change or update this setting.

  [Education/DefaultPrinterName CSP](/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Add new printers**: **Block** prevents users from adding new printers. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow adding new printers.

  [Education/PreventAddingNewPrinters CSP](/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## Privacy

These settings use the [privacy policy CSP](/windows/client-management/mdm/policy-csp-privacy), which also lists the supported Windows editions.

- **Privacy experience**: **Block** prevents the privacy experience from opening when users sign in, and from opening for new and upgraded users. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Privacy/DisablePrivacyExperience](/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Input personalization**: **Block** prevents using voice for dictation and to talk to apps that use Microsoft cloud-based speech recognition. It's disabled and users can't enable online speech recognition using settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users choose. If you allow these services, Microsoft might collect voice data to improve the service.

  [Privacy/AllowInputPersonalization CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Automatic acceptance of the pairing and privacy user consent prompts**: Choose **Allow** so Windows can automatically accept pairing and privacy consent messages when running apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent the automatic acceptance.

  [Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Publish user activities**: **Block** prevents apps and the OS from publishing user activities. It also prevents shared experiences and discovery of recently used resources in the activity feed. User Activities track the state of a user's tasks in an app or the OS. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable this feature so apps can publish user activities.

  [Privacy/PublishUserActivities CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Local activities only**: **Block** prevents shared experiences and the discovery of recently used resources in task switcher, based only on local activity. When set to **Not configured** (default), Intune doesn't change or update this setting.

You can configure information that all apps on the device can access. Also, define exceptions on a per-app basis using **Per-app privacy exceptions**.

### Exceptions

- **Account information**: Define whether this app can access the user name, picture, and other contact info.
- **Background apps**: Define whether this app can run in the background.
- **Calendar**: Define whether this app can access the calendar.
- **Call history**: Define whether this app can access my call history.
- **Camera**: Define whether this app can access the camera.
- **Contacts**: Define whether this app can access contacts.
- **Email**: Define whether this app can access and send email.
- **Location**: Define whether this app can access location information.
- **Messaging**: Define whether this app can read or send text or MMS messages.
- **Microphone**: Define whether this app can use the microphone.
- **Motion**: Define whether this app can access device motion information.
- **Notifications**: Define whether this app can access notifications.
- **Phone**: Define whether this app can access the phone.
- **Radios**: Some apps use radios (for example, Bluetooth) in your device to send and receive data and need to turn these radios on or off. Define whether this app can control these radios.
- **Tasks**: Define whether this app can access your tasks.
- **Trusted devices**: Choose if this app can use trusted devices. Trusted devices are hardware you've already connected, or hardware that comes with the device. For example, use TVs, projectors, and so on, as trusted devices.
- **Feedback and diagnostics**: Choose if this app can access diagnostic information.
- **Sync with devices** -Define whether this app can automatically share and sync info with wireless devices that don't explicitly pair with this PC, tablet, or phone.

## Projection

These settings use the [WirelessDisplay policy CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay), which also lists the supported Windows editions.

- **User input from wireless display receivers**: **Block** prevents user input from wireless display receivers. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow a wireless display to send keyboard, mouse, pen, and touch input back to the source device.

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Projection to this PC**: **Block** prevents other devices from finding the device for projection, and prevents projecting to other devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to be discoverable, and can project to the device above the lock screen.

  [WirelessDisplay/AllowProjectionFromPC CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Require PIN for pairing**: **Require** always prompts for a PIN when connecting to a projection device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require a PIN to pair the device.

  [WirelessDisplay/RequirePinForPairing CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## Reporting and telemetry

For information about recent changes for Windows Telemetry, see [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection).

- **Share usage data**: Choose the level of diagnostic data that's submitted. Your options:
  - **Not configured**: (default): Intune doesn't change or update this setting. No setting is forced. Users choose the level that's submitted. By default, the OS might not share any data.
  - **Diagnostic data off**: (Not recommended). Review the *CSP System/AllowTelemetry* for details about this setting.
  - **Required**: Sends basic device information, including quality-related data, app compatibility, and other similar data to keep the device secure and up-to-date.
  - **Enhanced (1903 and earlier)**: Additional insights, including how Windows, Windows Server, System Center, and apps are used, how they perform, advanced reliability data, and data from the *Required* level. When this option is deployed to a device that runs Windows 1909 and later, the device is set to *Required*.
  - **Optional**: All data necessary to identify and help to fix problems, plus data from the *Required* and *Enhanced* level.

  [System/AllowTelemetry CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Send Microsoft Edge browsing data to Microsoft 365 Analytics**: To use this feature, set the **Share usage data** settings to **Enhanced** or **Full**. This feature controls what data Microsoft Edge sends to Microsoft 365 Analytics for enterprise devices with a configured commercial ID. Your options:
  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might not collect or send any browsing history data.
  - **Only send intranet data**: Allows the administrator to send intranet data history.
  - **Only send internet data**: Allows the administrator to send internet data history.
  - **Send intranet and internet data**: Allows the administrator to send intranet and internet data history.

  [Browser/ConfigureTelemetryForMicrosoft365Analytics CSP](/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Telemetry proxy server**: Enter the fully qualified domain name (FQDN) or IP address of a proxy server to forward Connected User Experiences and Telemetry requests, using a Secure Sockets Layer (SSL) connection. The format for this setting is *server*:*port*. If the named proxy fails, or if a proxy isn't entered, then the Connected User Experiences and Telemetry data isn't sent. It stays on the local device.

  If you don't enter a value, Intune doesn't change or update this setting. By default, the OS might send the Connected User Experiences and Telemetry data to Microsoft using the default proxy configuration.

  Example formats:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy CSP](/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## Search

These settings use the [search policy CSP](/windows/client-management/mdm/policy-csp-search), which also lists the supported Windows editions.

- **Safe Search (mobile only)**: Control how Cortana filters adult content in search results. Your options:
  - **User defined**: Intune doesn't change or update this setting. No setting is forced. Users choose their own settings.
  - **Strict**: Highest filtering against adult content
  - **Moderate**: Moderate filtering against adult content. Valid search results aren't filtered.
- **Display web results in search**: **Block** prevents users from using Windows Search to search the internet, and web results aren't shown in Search. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to search the web, and the results are shown on the device.
- **Diacritics**: **Block** prevents diacritics from being shown in Windows Search. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show diacritics.

  [Search/AllowUsingDiacritics CSP](/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Automatic language detection**: **Block** prevents Windows Search from automatically detecting the language when indexing content or properties. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.

  [Search/AlwaysUseAutoLangDetection CSP](/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Search location**: **Block** prevents Windows Search from using the location. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Indexer backoff**: **Block** disables the search indexer backoff feature. Indexing continues at full speed, even if the system activity is high. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might use backoff logic to throttle back indexing activity when system activity is high.

  [Search/DisableBackoff CSP](/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Removable drive indexing**: **Block** prevents locations on removable drives from being added to libraries, and from being indexed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.

  [Search/DisableRemovableDriveIndexing CSP](/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Low disk space indexing**: **Enable** allows automatic indexing, even when disk space is low. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn off automatic indexing when the hard disk space is 600 MB or less. If devices in your organization have limited hard drive space, then set it to **Not configured**.

  [Search/PreventIndexingLowDiskSpaceMB CSP](/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Remote queries**: **Enable** allows remote queries of the device's index. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from querying the device's index remotely.

  [Search/PreventRemoteQueries CSP](/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## Start

These settings use the [start policy CSP](/windows/client-management/mdm/policy-csp-start), which also lists the supported Windows editions.  

> [!NOTE]
> Management capabilities to deliver customized Start and Taskbar experiences are currently limited on Windows 11. For more information, see [Supported configuration service provider (CSP) policies for Windows 11 Start menu](/windows/configuration/supported-csp-start-menu-layout-windows).

- **Start menu layout**: Upload an XML file that includes your customizations, including the order the apps are listed, and more. The XML file overrides the default start layout. Users can't change the start menu layout you enter.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/StartLayout CSP](/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Pin websites to tiles in Start menu**: Import images from Microsoft Edge. These images are shown as links in the Windows Start menu for desktop devices. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/ImportEdgeAssets CSP](/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Unpin apps from task bar**: **Block** prevents users from unpinning apps from the task bar. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unpin apps from the task bar.

  [Start/NoPinningToTaskbar CSP](/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Fast user switching**: **Block** prevents switching between users that are logged on simultaneously without logging off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the **Switch user** on the user tile.

  [WindowsLogon/HideFastUserSwitching CSP](/windows/client-management/mdm/policy-csp-windowslogon#windowslogon-hidefastuserswitching)

- **Most used apps**: **Block** hides the most used apps from showing on the start menu. It also disables the corresponding toggle in the Settings app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the most used apps.

  [Start/HideFrequentlyUsedApps CSP](/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Recently added apps**: **Block** hides recently added apps on the start menu. It also disables the corresponding toggle in the Settings app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the recently added apps on the start menu.

  [Start/HideRecentlyAddedApps CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Start screen mode**: Choose the size of the start screen. Your options:
  - **User defined**: Intune doesn't change or update this setting. No setting is forced. Users can set the size.
  - **Full screen**: Forces a fullscreen size of Start.
  - **Non-full screen**: Force a non-fullscreen size of Start.

  [Start/ForceStartSize CSP](/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Recently opened items in Jump Lists**: **Block** hides recent jump lists from being shown on the start menu and taskbar. It also disables the corresponding toggle in the Settings app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show recently opened items in the jumplists.

  [Start/HideRecentJumplists CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **App list**: Choose how the all apps lists are shown. Your options:
  - **User defined**: Intune doesn't change or update this setting. No setting is forced. Users choose how the app list is shown.
  - **Collapse**: Hides the all apps list.
  - **Collapse and disable the Settings app**: Hides the all apps list, and disables **Show app list in Start menu** in the Settings app.
  - **Removes and disables the Settings app**: Hides the all apps list, removes all apps button, and disables **Show app list in Start menu** in the Settings app.

  [Start/HideAppList CSP](/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Power button**: **Block** hides the power button in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the power button.

  [Start/HidePowerButton CSP](/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **User Tile**: **Block** hides the user tile in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the user tile. Configure the following settings:
  - **Lock**: **Block** hides the **Lock** option in the user tile in the start menu.  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the **Lock** option.
  - **Sign out**: **Block** hides the **Sign out** option in the user tile in the start menu. **Not configured** (default) shows the **Sign out** option.

  [Start/HideUserTile CSP](/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Shut Down**: **Block** hides the **Update and shut down** and **Shut down** options in the power button in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/HideShutDown CSP](/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Sleep**: **Block** hides the **Sleep** option in the power button in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/HideSleep CSP](/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Hibernate**: **Block** hides the **Hibernate** option in the power button in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/HideHibernate CSP](/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Switch Account**: **Block** hides the **Switch account** in the user tile in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/HideSwitchAccount CSP](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Restart Options**:  **Block** hides the **Update and restart** and **Restart** options in the power button in the start menu. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Start/HideRestart CSP](/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documents on Start**: Hide or show the Documents folder in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderDocuments CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Downloads on Start**: Hide or show the Downloads folder in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderDownloads CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **File Explorer on Start**: Hide or show File Explorer in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderFileExplorer CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **HomeGroup on Start**: Hide or show the HomeGroup shortcut in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderHomeGroup CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Music on Start**: Hide or show the Music folder in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderMusic CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Network on Start**: Hide or show Network in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderNetwork CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Personal folder on Start**: Hide or show Personal folder in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderPersonalFolder CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Pictures on Start**: Hide or show the folder for pictures in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderPictures CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Settings on Start**: Hide or show the Settings shortcut in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderSettings CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Videos on Start**: Hide or show the folder for videos in the Windows Start menu. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose to show or hide the shortcut.
  - **Hide**: The shortcut is hidden, and setting is disabled in the Settings app.
  - **Show**: The shortcut is shown, and setting is disabled in the Settings app.

  [Start/AllowPinnedFolderVideos CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## Microsoft Defender SmartScreen

- **SmartScreen for Microsoft Edge**: **Require** turns on Microsoft Defender SmartScreen, and prevents users from turning it off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on SmartScreen, and allow users to turn it on and off.

  Microsoft Edge uses Microsoft Defender SmartScreen (turned on) to protect users from potential phishing scams and malicious software.

  [Browser/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Malicious site access**: **Block** prevents users from ignoring the Microsoft Defender SmartScreen Filter warnings, and blocks them from going to the site. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to ignore the warnings, and continue to the site.

  [Browser/PreventSmartScreenPromptOverride CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Unverified file download**: **Block** prevents users from ignoring the Microsoft Defender SmartScreen Filter warnings, and blocks them from downloading unverified files. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to ignore the warnings, and continue to download the unverified files.

  [Browser/PreventSmartScreenPromptOverrideForFiles CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## Windows Spotlight

These settings use the [experience policy CSP](/windows/client-management/mdm/policy-csp-experience), which also lists the supported Windows editions.

- **Windows Spotlight**: **Block** turns off Windows spotlight on the lock screen, Windows Tips, Microsoft consumer features, and other related features. If your goal is to minimize network traffic from devices, then select **Yes**. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Windows spotlight features, and might be controlled by users.

  [Experience/AllowWindowsSpotlight CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  When set to **Not configured**, you can also allow or block the following settings:

  - **Windows Spotlight on lock screen**: **Block** stops Windows Spotlight from showing information on the device lock screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show Windows spotlight information on the lock screen.

    [Experience/ConfigureWindowsSpotlightOnLockScreen CSP](/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Third-party suggestions in Windows Spotlight**: **Block** stops Windows Spotlight from suggesting content that isn't published by Microsoft. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow app and content suggestions from partners, and show suggested apps in the Start menu, and Windows tips.

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Consumer Features**: **Block** turns off experiences that are typically for consumers, such as start suggestions, membership notifications, post-out of box experience app installation, and redirect tiles. When set to **Not configured** (default), Intune doesn't change or update this setting.

    [Experience/AllowWindowsConsumerFeatures CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Windows Tips**: **Block** disables pop-up Windows Tips. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the Windows Tips to show.

    [Experience/AllowWindowsTips CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Windows Spotlight in action center**: **Block** prevents Windows spotlight notifications from showing in the Action Center. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show notifications in the Action Center that suggest apps or features to help users be more productive on Windows.

    [Experience/AllowWindowsSpotlightOnActionCenter CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Windows Spotlight personalization**: **Block** prevents Windows from using diagnostic data to provide customized experiences to users. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Microsoft to use diagnostic data to provide personalized recommendations, tips, and offers to tailor Windows for the user's needs.

    [Experience/AllowTailoredExperiencesWithDiagnosticData CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Windows welcome experience**: **Block** turns off the Windows spotlight Windows welcome experience feature. The Windows welcome experience won't show when there are updates and changes to Windows and its apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Windows welcome experience that shows users information about new, or updated features.

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## Microsoft Defender Antivirus

These settings use the [defender policy CSP](/windows/client-management/mdm/policy-csp-defender), which also lists the supported Windows editions.

- **Real-time monitoring**: **Enable** turns on real-time scanning for malware, spyware, and other unwanted software. Users can't turn it off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS turns on this feature, and allows users to change it.

  If you enable this setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowRealtimeMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Behavior monitoring**: **Enable** turns on behavior monitoring, and checks for certain known patterns of suspicious activity on devices. Users can't turn behavior monitoring off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on Behavior Monitoring, and allow users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowBehaviorMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Network Inspection System (NIS)**: NIS helps to protect devices against network-based exploits. It uses the signatures of known vulnerabilities from the Microsoft Endpoint Protection Center to help detect and block malicious traffic.

  - **Enable**: Turns on network protection and network blocking. Users can't turn it off. When enabled, users are blocked from connecting to known vulnerabilities.

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS turns on NIS, and allows users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/EnableNetworkProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Scan all downloads**: **Enable** turns on this setting, and Defender scans all files downloaded from the Internet. Users can't turn off this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on this setting, and allow users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowIOAVProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Scan scripts loaded in Microsoft web browsers**: **Enable** allows Defender to scan scripts that are used in Internet Explorer. Users can't turn off this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on this setting, and allow users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowScriptScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **End user access to Defender**: **Block** hides the Microsoft Defender user interface from users. All Microsoft Defender notifications are also suppressed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow user access to the Microsoft Defender UI, and allow users to change it.

  If you block the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  When this setting is changed, it takes effect the next time the device is restarted.

  [Defender/AllowUserUIAccess CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Security intelligence update interval (in hours)**: Enter the interval that Defender checks for new security intelligence, from 0-24. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. The operating system default may check for updates every 8 hours.
  - **Do not check**: Defender doesn't check for new security intelligence updates.
  - **1-24**: `1` checks every hour, `2` checks every two hours, `24` checks every day, and so on.
  
  [Defender/SignatureUpdateInterval CSP](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Monitor file and program activity**: Allows Defender to monitor file and program activity on devices. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. The operating system default may monitor all files.
  - **Monitoring disabled**
  - **Monitor all files**
  - **Monitor incoming files only**
  - **Monitor outgoing files only**

  [Defender/RealTimeScanDirection CSP](/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Days before deleting quarantined malware**: Continue tracking resolved malware for the number of days you enter so you can manually check previously affected devices. 

  If you don't configure this setting, or set it to `0` days, malware stays in the Quarantine folder, and isn't automatically removed. When set to `90`, quarantine items are stored for 90 days on the system, and then removed.

  [Defender/DaysToRetainCleanedMalware CSP](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **CPU usage limit during a scan**: Limit the amount of CPU that scans are allowed to use, from `0` to `100` percent. By default, the OS might set it to 50%.

  [Defender/AvgCPULoadFactor CSP](/windows/client-management/mdm/policy-csp-defender#avgcpuloadfactor)
  
- **Scan archive files**: **Enable** turns on Defender so it scans archive files, such as Zip or Cab files. Users can't turn off this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on this scanning, and allow users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowArchiveScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Scan incoming mail messages**: **Enable** allows Defender to scan email messages as they arrive on devices. When enabled, the engine parses the mailbox and mail files to analyze the mail body and attachments. You can scan .pst (Outlook), .dbx, .mbx, MIME (Outlook Express), and BinHex (Mac) formats.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS turns off this scanning, and allows users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowEmailScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Scan removable drives during a full scan**: **Enable** turns on Defender removable drive scans during a full scan. Users can't turn off this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let Defender scan removable drives, such as USB sticks, and allow users to change this setting.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  During a quick scan, removable drives may still be scanned.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowFullScanRemovableDriveScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Scan mapped network drives during a full scan**: **Enable** has Defender scan files on mapped network drives. If the files on the drive are read-only, Defender can't remove any malware found in them. Users can't turn off this setting.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS turns on this feature, and allows users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state. 

  During a quick scan, mapped network drives may still be scanned.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Scan files opened from network folders**: **Enable** has Defender scans files opened from network folders or shared network drives, such as files accessed from a UNC path. Users can't turn off this setting. If the files on the drive are read-only, Defender can't remove any malware found in them.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS scans files opened from network folders, and allows users to change it.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowScanningNetworkFiles CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Cloud protection**: **Enable** turns on the Microsoft Active Protection Service to receive information about malware activity from devices that you manage. Users can't change this setting. 

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS allows the Microsoft Active Protection Service to receive information, and allows users to change this setting.

  If you enable the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously configured state.

  Intune doesn't turn off this feature. To disable it, use a custom URI.

  [Defender/AllowCloudProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Prompt users before sample submission**: Controls whether potentially malicious files that might require further analysis are automatically sent to Microsoft. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. The operating system default may send safe samples automatically.
  - **Always prompt**
  - **Prompt before sending personal data**
  - **Never send data**
  - **Send all data without prompting**: Data is sent automatically.

  [Defender/SubmitSamplesConsent CSP](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Time to perform a daily quick scan**: Choose the hour to run a daily quick scan. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might run this scan at 2 AM.

  If you want more customization, then configure the **Type of system scan to perform** setting.

  [Defender/ScheduleQuickScanTime CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Type of system scan to perform**: Schedule a system scan, including the level of scanning, and the day and time to run the scan. Your options:
  - **Not configured**: Intune doesn't change or update this setting. No setting is forced. Users can manually run scans as needed or wanted on their devices.
  - **Disable**: Disables any system scanning on devices. Choose this option if you're using a partner anti-virus solution that scans devices.
  - **Quick scan**: Looks at common locations where there could be malware registered, such as registry keys and known Windows startup folders.
    - **Day scheduled**: Choose the day to run the scan.
    - **Time scheduled**: Choose the hour to run the scan.
  - **Full scan**: Looks at common locations where there could be malware registered, and also scans every file and folder on the device.
    - **Day scheduled**: Choose the day to run the scan.
    - **Time scheduled**: Choose the hour to run the scan.

  > [!TIP]
  > This setting may conflict with the **Time to perform a daily quick scan** setting. Some recommendations:  
  >
  > - If you want to schedule a daily quick scan, and a weekly full scan, then:
  >   1. Configure the **Time to perform a daily quick scan** setting.
  >   2. Configure the **Type of system scan to perform** to do a full scan.
  > 
  > - If you only want one quick scan daily (no full scan), then use either setting: **Time to perform a daily quick scan** or **Type of system scan to perform**. For example, to run a quick scan every Tuesday at 6 AM, configure the **Type of system scan to perform** setting.
  > 
  > - Don't configure the **Time to perform a daily quick scan** setting simultaneously with the **Type of system scan to perform** set to **Quick scan**. These settings may conflict, and a scan may not run.

  [Defender/ScanParameter CSP](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Detect potentially unwanted applications**: This feature identifies and blocks potentially unwanted applications (PUA) from downloading and installing in your network. These applications aren't considered viruses, malware, or other types of threats. But, they can run actions on endpoints that might affect their performance or use. Choose the level of protection when Windows detects PUAs. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, Microsoft Defender might disable this feature.
  - **Off** or **Disabled**: PUA Protection off.
  - **Enable**: Microsoft Defender detects PUAs, and detected items are blocked. These items show in history along with other threats.
  - **Audit**: Microsoft Defender detects PUAs, but takes no action. You can review information about the applications Microsoft Defender would take action against. For example, search for events created by Microsoft Defender in the Event Viewer.

  In **Endpoint Security** > **Antivirus** > **Microsoft Defender Antivirus** > **Remediation**, this setting is called **Action to take on potentially unwanted applications**.

  For more information about potentially unwanted apps, see [Detect and block potentially unwanted applications](/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus). 

  [Defender/PUAProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Submit samples consent**: Currently, this setting has no impact. Don't use this setting. It may be removed in a future release.

- **On Access Protection**: **Block** prevents scanning files that have been accessed or downloaded. Users can't turn it on. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable this feature, and allows users to change it.

  If you block the setting, and then change it back to **Not configured**, then Intune leaves the setting in its previously OS-configured state.

  Intune doesn't turn on this feature. To enable it, use a custom URI.

  [Defender/AllowOnAccessProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Actions on detected malware threats**: Select **Enable** to choose the actions you want Defender to take for each threat level it detects: low, moderate, high, and severe. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let Microsoft Defender choose the best option.

  When set to **Enable**, select the action:
  
  - **Clean**
  - **Quarantine**
  - **Remove**
  - **Allow**
  - **User defined**
  - **Block**

  If your action isn't possible, then Microsoft Defender chooses the best option to ensure the threat is remediated.

  [Defender/ThreatSeverityDefaultAction CSP](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### Microsoft Defender Antivirus Exclusions

You can exclude certain files from Microsoft Defender Antivirus scans by modifying exclusion lists. **Generally, you shouldn't need to apply exclusions**. Microsoft Defender Antivirus includes a number of automatic exclusions based on known OS behaviors and typical management files, such as those used in enterprise management, database management, and other enterprise scenarios and situations.

> [!WARNING]
> **Defining exclusions lowers the protection offered by Microsoft Defender Antivirus**. Always evaluate the risks that are associated with implementing exclusions. Only exclude files you know aren't malicious.

- **Files and folders to exclude from scans and real-time protection**: Adds one or more files and folders like **C:\Path** or **%ProgramFiles%\Path\filename.exe** to the exclusions list. These files and folders aren't included in any real-time or scheduled scans.
- **File extensions to exclude from scans and real-time protection**: Add one or more file extensions like **jpg** or **txt** to the exclusions list. Any files with these extensions aren't included in any real-time or scheduled scans.
- **Processes to exclude from scans and real-time protection**: Add one or more processes of the type **.exe**, **.com**, or **.scr** to the exclusions list. These processes aren't included in any real-time, or scheduled scans.

For more information, see [Exclusions overview](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions) in the Microsoft Defender documentation.

## Power settings

These settings use the [power policy CSP](/windows/client-management/mdm/policy-csp-power), which also lists the supported Windows editions.

### Battery

- **Battery level to turn Energy Saver on**: When the device is using battery power, enter the battery charge level to turn on Energy Saver, from 0-100. Enter a percentage value that indicates the battery charge level. For example, when set to `80`, Energy Saver turns on when the battery has 80% charge or less available.

  If you don't enter a value, Intune doesn't change or update this setting. By default, the OS might set it to 70%.

  [Power/EnergySaverBatteryThresholdOnBattery CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Lid close (mobile only)**: When the device is using battery power, choose what happens when the lid is closed. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to control this setting.
  - **No action**: The device stays on, and continues to use battery power.
  - **Sleep**: The device goes into sleep mode, and uses a small amount of battery charge. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.

  [Power/SelectLidCloseActionOnBattery CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Power button**: When the device is using battery power, choose what happens when the Power button is selected. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to control this setting.
  - **No action**: The device stays on, and continues to use battery power.
  - **Sleep**: The device goes into sleep mode, and uses a small amount of battery charge. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.

  [Power/SelectPowerButtonActionOnBattery CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Sleep button**: When the device is using battery power, choose what happens when the Sleep button is selected. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to control this setting.
  - **No action**: The device stays on, and continues to use battery power.
  - **Sleep**: The device goes into sleep mode and uses a small amount of battery charge. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.

  [Power/SelectSleepButtonActionOnBattery CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybrid sleep**: When the device is using battery power, choose to allow or disable hybrid sleep mode.

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to control this setting.
  - **Enable**: Devices can go into hybrid sleep mode. Opened apps and files are stored in random access memory (RAM), and on the hard disk. It uses a small amount of battery charge.
  - **Disable**: Prevents devices from going into hybrid sleep mode.

  [Power/TurnOffHybridSleepOnBattery CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### PluggedIn

- **Battery level to turn Energy Saver on**: When the device is plugged in, enter the battery charge level to turn on Energy Saver from 0-100. Enter a percentage value that indicates the battery charge level. For example, when set to `80`, Energy Saver turns on when the battery has 80% charge or less available.

  If you don't enter a value, Intune doesn't change or update this setting. By default, the OS might set it to 70%.

  [Power/EnergySaverBatteryThresholdPluggedIn CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Lid close (mobile only)**: When the device is plugged in, choose what happens when the lid is closed. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **No action**: The device stays on.
  - **Sleep**: The device goes into sleep mode. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.
  
    [Power/SelectLidCloseActionPluggedIn CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Power button**: When the device is plugged in, choose what happens when the Power button is selected. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **No action**: The device stays on.
  - **Sleep**: The device goes into sleep mode. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.

  [Power/SelectPowerButtonActionPluggedIn CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Sleep button**: When the device is plugged in, choose what happens when the Sleep button is selected. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **No action**: The device stays on.
  - **Sleep**: The device goes into sleep mode. The computer is still on, and opened apps and files are stored in random access memory (RAM).
  - **Hibernate**: The device goes into hibernate mode. Opened apps and files are stored on the hard disk, and the device turns off.
  - **Shutdown**: The device shuts down. Opened apps and files are closed without saving.

  [Power/SelectSleepButtonActionPluggedIn CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Hybrid sleep**: When the device is plugged in, choose to allow or disable hybrid sleep mode.

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow users to control this setting.
  - **Enable**: Devices can go into hybrid sleep mode. Opened apps and files are stored in random access memory (RAM), and on the hard disk.
  - **Disable**: Prevents devices from going into hybrid sleep mode.

  [Power/TurnOffHybridSleepPluggedIn CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## Next steps

For additional technical details on each setting and what editions of Windows are supported, see [Windows 10/11 Policy CSP Reference](/windows/client-management/mdm/policy-configuration-service-provider)

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
