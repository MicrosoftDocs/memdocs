---**:::no-loc text="
title: Common Education device restrictions configuration
description: Learn about common device restrictions configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: conceptual
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows]
---

# Device Restrictions

There are many device restriction settings and configuration options you have available. This article summarizes the configurations that are most commonly used for student and teacher devices.

Intune and Intune for Education includes device restriction policies that help administrators control a wide range of settings and features on Android, iOS/iPadOS, macOS, and Windows devices to protect your organization's resources.

## Organization-specific settings

Configure these settings to personalize user experience and simplify the Windows sign-in process. Values for these settings should be defined according to the environment.

To learn more, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog).

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
|**:::no-loc text="Preferred Aad Tenant Domain Name":::** | _domain_ | Simplifies the sign-in to Windows by automatically appending the domain to the username | [Authentication/PreferredAadTenantDomainName](/windows/client-management/mdm/policy-csp-authentication#preferredaadtenantdomainname) |
|**:::no-loc text="Desktop Image Url":::** | _url_ | An http or https Url to a jpg, jpeg or png image that needs to be downloaded and used as the Desktop Image or a file Url to a local image on the file system that needs to be used as the Desktop Image. | [Personalization/DesktopImageUrl](/windows/client-management/mdm/personalization-csp#desktopimageurl) |
|**:::no-loc text="Lock Screen Image Url":::** | _url_ | An http or https URL to a jpg, jpeg or png image that needs to be downloaded and used as the Lock Screen Image. | [Personalization/LockScreenImageUrl](/windows/client-management/mdm/personalization-csp#lockscreenimageurl) |
|**:::no-loc text="Configure Time Zone":::** | _timezone_ | Use Timezone column from [Default Time Zones](/windows-hardware/manufacture/desktop/default-time-zones) | [TimeLanguageSettings/ConfigureTimeZone](/windows/client-management/mdm/policy-csp-timelanguagesettings#configuretimezone) |

## General restrictions

Commonly applied device restrictions in education.

To learn more, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog).

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
|**:::no-loc text="Allow Cortana Above Lock":::** | Block | The system will need to be unlocked for the user to interact with Cortana using speech. | [AboveLock/AllowCortanaAboveLock](/windows/client-management/mdm/policy-csp-abovelock#allowcortanaabovelock) |
|**:::no-loc text="Allow Toasts":::** | Block | Block toast notifications above the device lock screen | [AboveLock/AllowToasts](/windows/client-management/mdm/policy-csp-abovelock#allowtoasts) |
|**:::no-loc text="Allow Adding Non Microsoft Accounts Manually":::** | Block | Block users from adding non-MSA email account. | [Accounts/AllowAddingNonMicrosoftAccountsManually](/windows/client-management/mdm/policy-csp-accounts#allowaddingnonmicrosoftaccountsmanually) |
|**:::no-loc text="Allow Microsoft Account Connection":::** | Block | Block users from using an MSA account for non-email related connection authentication and services. | [Accounts/AllowMicrosoftAccountConnection](/windows/client-management/mdm/policy-csp-accounts#allowmicrosoftaccountconnection) |
|**:::no-loc text="Specify the system hibernate timeout (on battery)":::** | Disabled | | [Power/HibernateTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#hibernatetimeoutonbattery) |
|**:::no-loc text="Specify the system sleep timeout (on battery)":::** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#standbytimeoutonbattery) |
|**:::no-loc text="System Sleep Timeout (seconds):":::** | 3600 | | [Power/StandbyTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#standbytimeoutonbattery) |
|**:::no-loc text="Specify the system sleep timeout (plugged in)":::** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#standbytimeoutpluggedin) |
|**:::no-loc text="System Sleep Timeout (seconds):":::** | 3600 | | [Power/StandbyTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#standbytimeoutpluggedin) |
|**:::no-loc text="Turn off the display (on battery)":::** | Enabled | | [Power/DisplayOffTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#displayofftimeoutonbattery) |
|**:::no-loc text="On battery power, turn display off after (seconds)":::** | 300 | | [Power/DisplayOffTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#displayofftimeoutonbattery) |
|**:::no-loc text="Turn off the display (plugged in)":::** | Enabled | | [Power/DisplayOffTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#displayofftimeoutpluggedin) |
|**:::no-loc text="When plugged in, turn display off after (seconds)":::** | 300 | | [Power/DisplayOffTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#displayofftimeoutpluggedin) |
|**:::no-loc text="All Removable Storage classes: Deny all access":::** | Disabled | Do not block access to removable storage | [ADMX_RemovableStorage/RemovableStorageClasses_DenyAll_Access_2](/windows/client-management/mdm/policy-csp-admx-removablestorage#removablestorageclasses_denyall_access_2) |
|**:::no-loc text="Allow Advertising":::** | Block | Blocks the device from sending out Bluetooth advertisements. | [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#allowadvertising) |
|**:::no-loc text="Allow Discoverable Mode":::** | Allow | Allow other Bluetooth-enabled devices discover the device. | [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#allowdiscoverablemode) |
|**:::no-loc text="Allow Prompted Proximal Connections":::** | Block | Block users on these managed devices from using Swift Pair and other proximity based scenarios. | [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#allowpromptedproximalconnections) |
|**:::no-loc text="Allow Camera":::** | Allowed | | [Camera/AllowCamera](/windows/client-management/mdm/policy-csp-camera#allowcamera) |
|**:::no-loc text="Allow Bluetooth":::** | Allow Bluetooth. The radio in the Bluetooth control panel will be functional and the user will be able to turn Bluetooth on. | | [Connectivity/AllowBluetooth](/windows/client-management/mdm/policy-csp-connectivity#allowbluetooth) |
|**:::no-loc text="Allow Cellular Data Roaming":::** | Do not allow cellular data roaming. The user cannot turn it on. This value is not supported in Windows 10, version 1511. | | [Connectivity/AllowCellularDataRoaming](/windows/client-management/mdm/policy-csp-connectivity#allowcellulardataroaming) |
|**:::no-loc text="Allow Cortana":::** | Block | | [Experience/AllowCortana](/windows/client-management/mdm/policy-csp-experience#allowcortana) |
|**:::no-loc text="Allow Manual MDM Unenrollment":::** | Block | Block the user from deleting the workplace account using the workplace control panel. | [Experience/AllowManualMDMUnenrollment](/windows/client-management/mdm/policy-csp-experience#allowmanualmdmunenrollment) |
|**:::no-loc text="Allow Widgets":::** | Not allowed. | This policy applies to the entire widgets experience, including content on the taskbar. | [AllowNewsAndInterests](/windows/client-management/mdm/policy-csp-newsandinterests) |
|**:::no-loc text="Allow Windows Spotlight (User)":::** | Block | Turn off Windows spotlight on lock screen, Windows Tips, Microsoft consumer features and other related features. | [Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#allowwindowsspotlight) |
|**:::no-loc text="Allow All Trusted Apps":::** | Explicit allow unlock. | Allow install of any LOB or developer-signed Windows Store app (which must be signed with a certificate chain that can be successfully validated by the local computer) | [ApplicationManagement/AllowAllTrustedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#allowalltrustedapps) |
|**:::no-loc text="Allow Developer Unlock":::** | Explicit deny. | Block developing Microsoft Store apps or installing them directly from an IDE. | [ApplicationManagement/AllowDeveloperUnlock](/windows/client-management/mdm/policy-csp-applicationmanagement#allowdeveloperunlock) |
|**:::no-loc text="Allow Shared User App Data":::** | Block | Windows app can't share app data with other instances of that app. | [ApplicationManagement/AllowSharedUserAppData](/windows/client-management/mdm/policy-csp-applicationmanagement#allowshareduserappdata) |
|**:::no-loc text="Turn off the Store application":::** | Enabled | Access to the Store application is denied. | [ADMX_WindowsStore/RemoveWindowsStore_2](/windows/client-management/mdm/policy-csp-admx-windowsstore#removewindowsstore_2) |
|**:::no-loc text="Allow Hibernate":::** | Block | Windows 11 only | [Power/AllowHibernate](/windows/client-management/mdm/policy-csp-power#allowhibernate) |
|**:::no-loc text="Energy Saver Battery Threshold On Battery":::** | 50 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdOnBattery](/windows/client-management/mdm/policy-csp-power#energysaverbatterythresholdonbattery) |
|**:::no-loc text="Energy Saver Battery Threshold Plugged In":::** | 40 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdPluggedIn](/windows/client-management/mdm/policy-csp-power#energysaverbatterythresholdpluggedin) |
|**:::no-loc text="Select Lid Close Action On Battery":::** | Sleep | | [Power/SelectLidCloseActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectlidcloseactiononbattery) |
|**:::no-loc text="Select Lid Close Action Plugged In":::** | Sleep | | [Power/SelectLidCloseActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectlidcloseactionpluggedin) |
|**:::no-loc text="Select Power Button Action On Battery":::** | Sleep | | [Power/SelectPowerButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectpowerbuttonactiononbattery) |
|**:::no-loc text="Select Power Button Action Plugged In":::** | Sleep | | [Power/SelectPowerButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectpowerbuttonactionpluggedin) |
|**:::no-loc text="Select Sleep Button Action On Battery":::** | Sleep | | [Power/SelectSleepButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#selectsleepbuttonactiononbattery) |
|**:::no-loc text="Select Sleep Button Action Plugged In":::** | Sleep | | [Power/SelectSleepButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#selectsleepbuttonactionpluggedin) |
|**:::no-loc text="Turn Off Hybrid Sleep On Battery":::** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepOnBattery](/windows/client-management/mdm/policy-csp-power#turnoffhybridsleeponbattery) |
|**:::no-loc text="Turn Off Hybrid Sleep Plugged In":::** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepPluggedIn](/windows/client-management/mdm/policy-csp-power#turnoffhybridsleeppluggedin) |
|**:::no-loc text="Unattended Sleep Timeout On Battery":::** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#unattendedsleeptimeoutonbattery) |
|**:::no-loc text="Unattended Sleep Timeout Plugged In":::** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#unattendedsleeptimeoutpluggedin) |
|**:::no-loc text="Allow Add Provisioning Package":::** | Allow | Allow the runtime configuration agent to install provisioning packages. | [Security/AllowAddProvisioningPackage](/windows/client-management/mdm/policy-csp-security#allowaddprovisioningpackage) |
|**:::no-loc text="Allow Remove Provisioning Package":::** | Allow | Allow the runtime configuration agent to remove provisioning packages. | [Security/AllowRemoveProvisioningPackage](/windows/client-management/mdm/policy-csp-security#allowremoveprovisioningpackage) |
|**:::no-loc text="Allow Date Time":::** | Block | Block the user from changing date and time settings. | [Settings/AllowDateTime](/windows/client-management/mdm/policy-csp-settings#allowdatetime) |
|**:::no-loc text="Allow Language":::** | Block | Block the user from changing the language settings. | [Settings/AllowLanguage](/windows/client-management/mdm/policy-csp-settings#allowlanguage) |
|**:::no-loc text="Allow Power Sleep":::** | Block | Block the user from changing power and sleep settings. | [Settings/AllowPowerSleep](/windows/client-management/mdm/policy-csp-settings#allowpowersleep) |
|**:::no-loc text="Allow Region":::** | Block | Block the user from changing the region settings. | [Settings/AllowRegion](/windows/client-management/mdm/policy-csp-settings#allowregion) |
|**:::no-loc text="Enable Shared PC Mode":::** | False | | [SharedPC/EnableSharedPCMode](/windows/client-management/mdm/sharedpc-csp#enablesharedpcmode) |
|**:::no-loc text="Restrict Local Storage":::** | False | | [SharedPC/RestrictLocalStorage](/windows/client-management/mdm/sharedpc-csp#restrictlocalstorage) |
|**:::no-loc text="Set Edu Policies":::** | true | [Windows 10 configuration recommendations for education customers](/education/windows/configure-windows-for-education) | [SharedPC/SetEDUpolicies](/windows/client-management/mdm/sharedpc-csp#setedupolicies) |
|**:::no-loc text="Allow End Task":::** | Block | | [TaskManager/AllowEndTask](/windows/client-management/mdm/policy-csp-taskmanager#allowendtask) |
|**:::no-loc text="Allow Auto Connect To Wi Fi Sense Hotspots":::** | Block | | [Wifi/AllowAutoConnectToWiFiSenseHotspots](/windows/client-management/mdm/policy-csp-wifi#allowautoconnecttowifisensehotspots) |
|**:::no-loc text="Allow Internet Sharing":::** | Block | | [Wifi/AllowInternetSharing](/windows/client-management/mdm/policy-csp-wifi#allowinternetsharing) |
|**:::no-loc text="Hide Fast User Switching":::** | Enabled | | [WindowsLogon/HideFastUserSwitching](/windows/client-management/mdm/policy-csp-windowslogon#hidefastuserswitching) |
|**:::no-loc text="Disable Automatic Re Deployment Credentials":::** | Disabled | Enables local Autopilot Reset | [CredentialProviders/DisableAutomaticReDeploymentCredentials](/en-us/windows/client-management/mdm/policy-csp-credentialproviders#disableautomaticredeploymentcredentials) |
|**:::no-loc text="Configure Chat Icon":::** | Disabled | Configures the Teams Chat icon on the taskbar for Windows 11 | [Experience/ConfigureChatIcon](/en-us/windows/client-management/mdm/policy-csp-experience#configurechaticon) |
