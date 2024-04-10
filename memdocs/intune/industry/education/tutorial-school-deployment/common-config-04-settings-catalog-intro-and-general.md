---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
## Settings Catalog Summary

Tables below represent a list of device restrictions and configurations as used commonly by education organizations throughout the world.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)

### Organization-specific settings

Configure these settings to personalize user experience and simplify the Windows sign-in process. Values for these settings should be defined by an Intune administrator according to the environment.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Preferred Aad Tenant Domain Name** | _domain_ | Simplifies the sign-in to Windows by automatically appending the domain to the username | [Authentication/PreferredAadTenantDomainName](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-authentication) |
  | **Desktop Image** **Url** | _url_ | An http or https Url to a jpg, jpeg or png image that needs to be downloaded and used as the Desktop Image or a file Url to a local image on the file system that needs to be used as the Desktop Image. | [Personalization/DesktopImageUrl](https://learn.microsoft.com/windows/client-management/mdm/personalization-csp) |
  | **Lock Screen Image** **Url** | _url_ | An http or https URL to a jpg, jpeg or png image that needs to be downloaded and used as the Lock Screen Image. | [Personalization/LockScreenImageUrl](https://learn.microsoft.com/windows/client-management/mdm/personalization-csp) |
  | **Configure Time Zone** | _timezone_ | Use Timezone column from [Default Time Zones](https://learn.microsoft.com/windows-hardware/manufacture/desktop/default-time-zones) | [TimeLanguageSettings/ConfigureTimeZone](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-timelanguagesettings) |

### General restrictions

These restrictions are commonly applied to most devices in educational organizations.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Allow Cortana Above Lock** | Block | The system will need to be unlocked for the user to interact with Cortana using speech. | [AboveLock/AllowCortanaAboveLock](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-abovelock) |
  | **Allow Toasts** | Block | Block toast notifications above the device lock screen | [AboveLock/AllowToasts](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-abovelock) |
  | **Allow Adding Non Microsoft Accounts Manually** | Block | Block users from adding non-MSA email account. | [Accounts/AllowAddingNonMicrosoftAccountsManually](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-accounts) |
  | **Allow Microsoft Account Connection** | Block | Block users from using an MSA account for non-email related connection authentication and services. | [Accounts/AllowMicrosoftAccountConnection](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-accounts) |
  | **Specify the system hibernate timeout (on battery)** | Disabled | | [Power/HibernateTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Specify the system sleep timeout (on battery)** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **System Sleep Timeout (seconds):** | 3600 | | [Power/StandbyTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Specify the system sleep timeout (plugged in)** | Enabled | Only enables the setting configuration. | [Power/StandbyTimeoutPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **System Sleep Timeout (seconds):** | 3600 | | [Power/StandbyTimeoutPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Turn off the display (on battery)** | Enabled | | [Power/DisplayOffTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **On battery power, turn display off after (seconds)** | 300 | | [Power/DisplayOffTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Turn off the display (plugged in)** | Enabled | | [Power/DisplayOffTimeoutPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **When plugged in, turn display off after (seconds)** | 300 | | [Power/DisplayOffTimeoutPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **All Removable Storage classes: Deny all access** | Disabled | Do not block access to removable storage | [ADMX_RemovableStorage/RemovableStorageClasses_DenyAll_Access_2](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-admx-removablestorage) |
  | **Allow Advertising** | Block | Blocks the device from sending out Bluetooth advertisements. | [Bluetooth/AllowAdvertising](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth) |
  | **Allow Discoverable Mode** | Allow | Allow other Bluetooth-enabled devices discover the device. | [Bluetooth/AllowDiscoverableMode](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth) |
  | **Allow Prompted Proximal Connections** | Block | Block users on these managed devices from using Swift Pair and other proximity based scenarios. | [Bluetooth/AllowPromptedProximalConnections](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth) |
  | **Allow Camera** | Allowed | | [Camera/AllowCamera](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-camera) |
  | **Allow Bluetooth** | Allow Bluetooth. The radio in the Bluetooth control panel will be functional and the user will be able to turn Bluetooth on. | | [Connectivity/AllowBluetooth](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) |
  | **Allow Cellular Data Roaming** | Do not allow cellular data roaming. The user cannot turn it on. This value is not supported in Windows 10, version 1511. | | [Connectivity/AllowCellularDataRoaming](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) |
  | **Allow Cortana** | Block | | [Experience/AllowCortana](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-experience) |
  | **Allow Manual MDM Unenrollment** | Block | Block the user from deleting the workplace account using the workplace control panel. | [Experience/AllowManualMDMUnenrollment](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-experience) |
  | **Allow Widgets** | Not allowed. | This policy applies to the entire widgets experience, including content on the taskbar. | [AllowNewsAndInterests](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-newsandinterests) |
  | **Allow Windows Spotlight (User)** | Block | Turn off Windows spotlight on lock screen, Windows Tips, Microsoft consumer features and other related features. | [Experience/AllowWindowsSpotlight](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-experience) |
  | **Allow All Trusted Apps** | Explicit allow unlock. | Allow install of any LOB or developer-signed Windows Store app (which must be signed with a certificate chain that can be successfully validated by the local computer) | [ApplicationManagement/AllowAllTrustedApps](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement) |
  | **Allow Developer Unlock** | Explicit deny. | Block developing Microsoft Store apps or installing them directly from an IDE. | [ApplicationManagement/AllowDeveloperUnlock](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement) |
  | **Allow Shared User App Data** | Block | Windows app can't share app data with other instances of that app. | [ApplicationManagement/AllowSharedUserAppData](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement) |
  | **Turn off the Store application** | Enabled | Access to the Store application is denied. | [ADMX_WindowsStore/RemoveWindowsStore_2](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-admx-windowsstore?WT.mc_id=Portal-Microsoft_Intune_Workflows) |
  | **Allow Hibernate** | Block | Windows 11 only | [Power/AllowHibernate](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Energy Saver Battery Threshold On Battery** | 50 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Energy Saver Battery Threshold Plugged In** | 40 | Energy Saver will be automatically turned on at (and below) the specified level. | [Power/EnergySaverBatteryThresholdPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Lid Close Action On Battery** | Sleep | | [Power/SelectLidCloseActionOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Lid Close Action Plugged In** | Sleep | | [Power/SelectLidCloseActionPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Power Button Action On Battery** | Sleep | | [Power/SelectPowerButtonActionOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Power Button Action Plugged In** | Sleep | | [Power/SelectPowerButtonActionPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Sleep Button Action On Battery** | Sleep | | [Power/SelectSleepButtonActionOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Select Sleep Button Action Plugged In** | Sleep | | [Power/SelectSleepButtonActionPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Turn Off Hybrid Sleep On Battery** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Turn Off Hybrid Sleep Plugged In** | hybrid sleep | A hiberfile isn't generated when the system transitions to sleep (Stand By). | [Power/TurnOffHybridSleepPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Unattended Sleep Timeout On Battery** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutOnBattery](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Unattended Sleep Timeout Plugged In** | 3600 | How much idle time (seconds) should elapse before Windows automatically transitions to sleep when left unattended. | [Power/UnattendedSleepTimeoutPluggedIn](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-power) |
  | **Allow Add Provisioning Package** | Allow | Allow the runtime configuration agent to install provisioning packages. | [Security/AllowAddProvisioningPackage](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-security) |
  | **Allow Remove Provisioning Package** | Allow | Allow the runtime configuration agent to remove provisioning packages. | [Security/AllowRemoveProvisioningPackage](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-security) |
  | **Allow Date Time** | Block | Block the user from changing date and time settings. | [Settings/AllowDateTime](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-settings) |
  | **Allow Language** | Block | Block the user from changing the language settings. | [Settings/AllowLanguage](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-settings) |
  | **Allow Power Sleep** | Block | Block the user from changing power and sleep settings. | [Settings/AllowPowerSleep](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-settings) |
  | **Allow Region** | Block | Block the user from changing the region settings. | [Settings/AllowRegion](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-settings) |
  | **Enable Shared PC Mode** | FALSE | | [SharedPC/EnableSharedPCMode](https://learn.microsoft.com/windows/client-management/mdm/sharedpc-csp) |
  | **Restrict Local Storage** | FALSE | | [SharedPC/RestrictLocalStorage](https://learn.microsoft.com/windows/client-management/mdm/sharedpc-csp) |
  | **Allow End Task** | Block | | [TaskManager/AllowEndTask](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager) |
  | **Allow Auto Connect To Wi Fi Sense Hotspots** | Block | | [Wifi/AllowAutoConnectToWiFiSenseHotspots](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-wifi) |
  | **Allow Internet Sharing** | Block | | [Wifi/AllowInternetSharing](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-wifi) |
  | **Hide Fast User Switching** | Enabled | | [WindowsLogon/HideFastUserSwitching](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-windowslogon) |
  | **Disable Automatic Re Deployment Credentials** | Disabled | Enables local Autopilot Reset | [CredentialProviders/ DisableAutomaticReDeploymentCredentials](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-credentialproviders) |
  | **Configure Chat Icon** | Disabled | Configures the Teams Chat icon on the taskbar for Windows 11 | [Experience/ConfigureChatIcon](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-experience) |

