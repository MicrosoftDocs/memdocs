---
title: Common Education device restrictions configuration
description: Learn about common device restrictions configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: devicerestrictions
author: yegor-a
ms.author: egorabr
---

# Device Restrictions

Tables in this article represent a list of device restrictions and configurations as used commonly by education organizations throughout the world.

## Organization-specific settings

Configure these settings to personalize user experience and simplify the Windows sign-in process. Values for these settings should be defined by an Intune administrator according to the environment.

#### Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Preferred Aad Tenant Domain Name** | _domain_ | Simplifies the sign-in to Windows by automatically appending the domain to the username | [Authentication/PreferredAadTenantDomainName](/windows/client-management/mdm/policy-csp-authentication#preferredaadtenantdomainname) |
  | **Desktop Image** **Url** | _url_ | An http or https Url to a jpg, jpeg or png image that needs to be downloaded and used as the Desktop Image or a file Url to a local image on the file system that needs to be used as the Desktop Image. | [Personalization/DesktopImageUrl](/windows/client-management/mdm/personalization-csp#desktopimageurl) |
  | **Lock Screen Image** **Url** | _url_ | An http or https URL to a jpg, jpeg or png image that needs to be downloaded and used as the Lock Screen Image. | [Personalization/LockScreenImageUrl](/windows/client-management/mdm/personalization-csp#lockscreenimageurl) |
  | **Configure Time Zone** | _timezone_ | Use Timezone column from [Default Time Zones](/windows-hardware/manufacture/desktop/default-time-zones) | [TimeLanguageSettings/ConfigureTimeZone](/windows/client-management/mdm/policy-csp-timelanguagesettings#configuretimezone) |

## General restrictions

These restrictions are commonly applied to most devices in many educational organizations.

#### Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Allow Cortana Above Lock** | Block | The system will need to be unlocked for the user to interact with Cortana using speech. | [AboveLock/AllowCortanaAboveLock](/windows/client-management/mdm/policy-csp-abovelock#allowcortanaabovelock) |
  | **Allow Toasts** | Block | Block toast notifications above the device lock screen | [AboveLock/AllowToasts](/windows/client-management/mdm/policy-csp-abovelock#allowtoasts) |
  | **Allow Adding Non Microsoft Accounts Manually** | Block | Block users from adding non-MSA email account. | [Accounts/AllowAddingNonMicrosoftAccountsManually](/windows/client-management/mdm/policy-csp-accounts#allowaddingnonmicrosoftaccountsmanually) |
  | **Allow Microsoft Account Connection** | Block | Block users from using an MSA account for non-email related connection authentication and services. | [Accounts/AllowMicrosoftAccountConnection](/windows/client-management/mdm/policy-csp-accounts#allowmicrosoftaccountconnection) |
  | **Specify the system hibernate timeout (on battery)** | Disabled | | [Power/HibernateTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#hibernatetimeoutonbattery) |
  | **Specify the system sleep timeout (on battery)** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#standbytimeoutonbattery) |
  | **System Sleep Timeout (seconds):** | 3600 | | [Power/StandbyTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#standbytimeoutonbattery) |
  | **Specify the system sleep timeout (plugged in)** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#standbytimeoutpluggedin) |
  | **System Sleep Timeout (seconds):** | 3600 | | [Power/StandbyTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#standbytimeoutpluggedin) |
  | **Turn off the display (on battery)** | Enabled | | [Power/DisplayOffTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#displayofftimeoutonbattery) |
  | **On battery power, turn display off after (seconds)** | 300 | | [Power/DisplayOffTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#displayofftimeoutonbattery) |
  | **Turn off the display (plugged in)** | Enabled | | [Power/DisplayOffTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#displayofftimeoutpluggedin) |
  | **When plugged in, turn display off after (seconds)** | 300 | | [Power/DisplayOffTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#displayofftimeoutpluggedin) |
  | **All Removable Storage classes: Deny all access** | Disabled | Do not block access to removable storage | [ADMX_RemovableStorage/RemovableStorageClasses_DenyAll_Access_2](/windows/client-management/mdm/policy-csp-admx-removablestorage#removablestorageclasses_denyall_access_2) |
  | **Allow Advertising** | Block | Blocks the device from sending out Bluetooth advertisements. | [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#allowadvertising) |
  | **Allow Discoverable Mode** | Allow | Allow other Bluetooth-enabled devices discover the device. | [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#allowdiscoverablemode) |
  | **Allow Prompted Proximal Connections** | Block | Block users on these managed devices from using Swift Pair and other proximity based scenarios. | [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#allowpromptedproximalconnections) |
  | **Allow Camera** | Allowed | | [Camera/AllowCamera](/windows/client-management/mdm/policy-csp-camera#allowcamera) |
  | **Allow Bluetooth** | Allow Bluetooth. The radio in the Bluetooth control panel will be functional and the user will be able to turn Bluetooth on. | | [Connectivity/AllowBluetooth](/windows/client-management/mdm/policy-csp-connectivity#allowbluetooth) |
  | **Allow Cellular Data Roaming** | Do not allow cellular data roaming. The user cannot turn it on. This value is not supported in Windows 10, version 1511. | | [Connectivity/AllowCellularDataRoaming](/windows/client-management/mdm/policy-csp-connectivity#allowcellulardataroaming) |
  | **Allow Cortana** | Block | | [Experience/AllowCortana](/windows/client-management/mdm/policy-csp-experience#allowcortana) |
  | **Allow Manual MDM Unenrollment** | Block | Block the user from deleting the workplace account using the workplace control panel. | [Experience/AllowManualMDMUnenrollment](/windows/client-management/mdm/policy-csp-experience#allowmanualmdmunenrollment) |
  | **Allow Widgets** | Not allowed. | This policy applies to the entire widgets experience, including content on the taskbar. | [AllowNewsAndInterests](/windows/client-management/mdm/policy-csp-newsandinterests) |
  | **Allow Windows Spotlight (User)** | Block | Turn off Windows spotlight on lock screen, Windows Tips, Microsoft consumer features and other related features. | [Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#allowwindowsspotlight) |
  | **Allow All Trusted Apps** | Explicit allow unlock. | Allow install of any LOB or developer-signed Windows Store app (which must be signed with a certificate chain that can be successfully validated by the local computer) | [ApplicationManagement/AllowAllTrustedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#allowalltrustedapps) |
  | **Allow Developer Unlock** | Explicit deny. | Block developing Microsoft Store apps or installing them directly from an IDE. | [ApplicationManagement/AllowDeveloperUnlock](/windows/client-management/mdm/policy-csp-applicationmanagement#allowdeveloperunlock) |
  | **Allow Shared User App Data** | Block | Windows app can't share app data with other instances of that app. | [ApplicationManagement/AllowSharedUserAppData](/windows/client-management/mdm/policy-csp-applicationmanagement#allowshareduserappdata) |
  | **Turn off the Store application** | Enabled | Access to the Store application is denied. | [ADMX_WindowsStore/RemoveWindowsStore_2](/windows/client-management/mdm/policy-csp-admx-windowsstore#removewindowsstore_2) |
  | **Allow Hibernate** | Block | Windows 11 only | [Power/AllowHibernate](/windows/client-management/mdm/policy-csp-power#allowhibernate) |
  | **Energy Saver Battery Threshold On Battery** | 50 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdOnBattery](/windows/client-management/mdm/policy-csp-power#energysaverbatterythresholdonbattery) |
  | **Energy Saver Battery Threshold Plugged In** | 40 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdPluggedIn](/windows/client-management/mdm/policy-csp-power#energysaverbatterythresholdpluggedin) |
  | **Select Lid Close Action On Battery** | Sleep | | [Power/SelectLidCloseActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectlidcloseactiononbattery) |
  | **Select Lid Close Action Plugged In** | Sleep | | [Power/SelectLidCloseActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectlidcloseactionpluggedin) |
  | **Select Power Button Action On Battery** | Sleep | | [Power/SelectPowerButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectpowerbuttonactiononbattery) |
  | **Select Power Button Action Plugged In** | Sleep | | [Power/SelectPowerButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectpowerbuttonactionpluggedin) |
  | **Select Sleep Button Action On Battery** | Sleep | | [Power/SelectSleepButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectsleepbuttonactiononbattery) |
  | **Select Sleep Button Action Plugged In** | Sleep | | [Power/SelectSleepButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectsleepbuttonactionpluggedin) |
  | **Turn Off Hybrid Sleep On Battery** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepOnBattery](/windows/client-management/mdm/policy-csp-power#turnoffhybridsleeponbattery) |
  | **Turn Off Hybrid Sleep Plugged In** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepPluggedIn](/windows/client-management/mdm/policy-csp-power#turnoffhybridsleeppluggedin) |
  | **Unattended Sleep Timeout On Battery** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#unattendedsleeptimeoutonbattery) |
  | **Unattended Sleep Timeout Plugged In** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#unattendedsleeptimeoutpluggedin) |
  | **Allow Add Provisioning Package** | Allow | Allow the runtime configuration agent to install provisioning packages. | [Security/AllowAddProvisioningPackage](/windows/client-management/mdm/policy-csp-security#allowaddprovisioningpackage) |
  | **Allow Remove Provisioning Package** | Allow | Allow the runtime configuration agent to remove provisioning packages. | [Security/AllowRemoveProvisioningPackage](/windows/client-management/mdm/policy-csp-security#allowremoveprovisioningpackage) |
  | **Allow Date Time** | Block | Block the user from changing date and time settings. | [Settings/AllowDateTime](/windows/client-management/mdm/policy-csp-settings#allowdatetime) |
  | **Allow Language** | Block | Block the user from changing the language settings. | [Settings/AllowLanguage](/windows/client-management/mdm/policy-csp-settings#allowlanguage) |
  | **Allow Power Sleep** | Block | Block the user from changing power and sleep settings. | [Settings/AllowPowerSleep](/windows/client-management/mdm/policy-csp-settings#allowpowersleep) |
  | **Allow Region** | Block | Block the user from changing the region settings. | [Settings/AllowRegion](/windows/client-management/mdm/policy-csp-settings#allowregion) |
  | **Enable Shared PC Mode** | FALSE | | [SharedPC/EnableSharedPCMode](/windows/client-management/mdm/sharedpc-csp#enablesharedpcmode) |
  | **Restrict Local Storage** | FALSE | | [SharedPC/RestrictLocalStorage](/windows/client-management/mdm/sharedpc-csp#restrictlocalstorage) |
  | **Allow End Task** | Block | | [TaskManager/AllowEndTask](/windows/client-management/mdm/policy-csp-taskmanager#allowendtask) |
  | **Allow Auto Connect To Wi Fi Sense Hotspots** | Block | | [Wifi/AllowAutoConnectToWiFiSenseHotspots](/windows/client-management/mdm/policy-csp-wifi#allowautoconnecttowifisensehotspots) |
  | **Allow Internet Sharing** | Block | | [Wifi/AllowInternetSharing](/windows/client-management/mdm/policy-csp-wifi#allowinternetsharing) |
  | **Hide Fast User Switching** | Enabled | | [WindowsLogon/HideFastUserSwitching](/windows/client-management/mdm/policy-csp-windowslogon#hidefastuserswitching) |
  | **Disable Automatic Re Deployment Credentials** | Disabled | Enables local Autopilot Reset | [CredentialProviders/DisableAutomaticReDeploymentCredentials](/en-us/windows/client-management/mdm/policy-csp-credentialproviders#disableautomaticredeploymentcredentials) |
  | **Configure Chat Icon** | Disabled | Configures the Teams Chat icon on the taskbar for Windows 11 | [Experience/ConfigureChatIcon](/en-us/windows/client-management/mdm/policy-csp-experience#configurechaticon) |
