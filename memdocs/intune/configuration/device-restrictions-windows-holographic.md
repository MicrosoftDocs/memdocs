---
# required metadata

title: Windows Holographic Business device settings - Microsoft Intune
description: Read about and configure device restriction settings in Microsoft Intune for Windows Holographic for Business. Control unenrollment, geolocation, passwords, install apps from app store, cookies, and pop ups in Microsoft Edge, Microsoft Defender, search, cloud and storage, bluetooth connectivity, system time, and usage data.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/18/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Windows Holographic for Business device settings to allow or restrict features using Intune

This article describes the different settings you can control on Windows Holographic for Business devices, such as Microsoft Hololens. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, control security, and more.

As an Intune administrator, you can create and assign these settings to your devices.

## Before you begin

[Create a Windows 10/11 device restrictions configuration profile](device-restrictions-configure.md#create-the-profile).

When you create a Windows 10/11 device restrictions configuration profile, there are more settings than what's listed in this article. The settings in this article are supported on Windows Holographic for Business devices.

## App Store

- **Auto-update apps from store**: **Block** prevents updates from being automatically installed from the Microsoft Store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps installed from the Microsoft Store to be automatically updated.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Trusted app installation**: Choose if non-Microsoft Store apps can be installed, also known as sideloading. Sideloading is installing, and then running or testing an app that isn't certified by the Microsoft Store. For example, an app that is internal to your company only. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Block**: Prevents sideloading. Non-Microsoft Store apps can't be installed.
  - **Allow**: Allows sideloading. Non-Microsoft Store apps can be installed.

  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Developer unlock**: Allow Windows developer settings, such as allowing sideloaded apps to be modified by users. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Block**: Prevents developer mode and sideloading apps.
  - **Allow**: Allows developer mode and sideloading apps.

  [ApplicationManagement/AllowDeveloperUnlock CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## Cellular and Connectivity

- **Bluetooth**: **Block** prevents users from enabling Bluetooth. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Bluetooth on the device.

  [Connectivity/AllowBluetooth CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Bluetooth discoverability**: **Block** prevents the device from being discoverable by other Bluetooth-enabled devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow other Bluetooth-enabled devices, such as a headset, to discover the device.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth advertising**: **Block** prevents the device from sending out Bluetooth advertisements. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device to send out Bluetooth advertisements.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## Cloud and Storage

- **Microsoft account**: **Block** prevents users from associating a Microsoft account with the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow adding and using a Microsoft account.

  [Accounts/AllowMicrosoftAccountConnection CSP](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## Control Panel and Settings

- **System time modification**: **Block** prevents users from changing the date and time settings on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these settings.

  [Settings/AllowDateTime CSP](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## General

- **Manual unenrollment**: **Block** prevents users from deleting the workplace account using the workplace control panel on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Experience/AllowManualMDMUnenrollment CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geolocation**: **Block** prevents users from turning on location services on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.

  [Experience/AllowFindMyDevice CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Block** disables the Cortana voice assistant on the device. When Cortana is off, users can still search to find items on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Cortana.

  [Experience/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## Microsoft Edge Browser

- **Start experience** > **Allow pop-ups**: **Yes** (default) allows pop-ups in the web browser. **No** prevents pop-up windows in the browser.

  [Browser/AllowPopups CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favorites and search** > **Show search suggestions**: **Yes** (default) allows your search engine to suggest sites as you type search phrases in the address bar. **No** prevents this feature.

  [Browser/AllowSearchSuggestionsinAddressBar CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Privacy and security** > **Allow Password Manager**: **Yes** (default) allows Microsoft Edge to automatically use Password Manager, which allows users to save and manage passwords on the device. **No** prevents Microsoft Edge from using Password Manager.

  [Browser/AllowPasswordManager CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Privacy and security** > **Cookies**: Choose how cookies are handled in the web browser. Your options:
  - **Allow**: Cookies are stored on the device.
  - **Block all cookies**: Cookies aren't stored on the device.
  - **Block only third party cookies**: Third party or partner cookies aren't stored on the device.

  [Browser/AllowCookies CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Privacy and security** > **Send do-not-track headers**: **Yes** sends do-not-track headers to websites requesting tracking info (recommended). **No** (default) doesn't send headers that allow websites to track the user. Users can configure this setting.

  [Browser/AllowDoNotTrack CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## Microsoft Defender SmartScreen

- **SmartScreen for Microsoft Edge**: **Require** turns on Microsoft Defender SmartScreen, and prevents users from turning it off. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on SmartScreen, and allow users to turn it on and off.

  [Browser/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## Password

- **Password**: **Require** forces users to enter a password to access the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to devices without a password. Applies to local accounts only. Domain account passwords remain configured by Active Directory (AD) and Azure AD.

  [DeviceLock/DevicePasswordEnabled CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Require password when device returns from idle state**: **Require** forces users to enter a password to unlock the device after being idle. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require a PIN or password after being idle.

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## Reporting and Telemetry

- **Share usage data**: Choose the level of diagnostic data that's submitted. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. No setting is forced. Users choose the level that's submitted. By default, the OS might not share any data.
  - **Security**: Information that's required to help keep Windows more secure, including data about the Connected User Experience and Telemetry component settings, the Malicious Software Removal Tool, and Microsoft Defender
  - **Basic**: Basic device information, including quality-related data, app compatibility, app usage data, and data from the Security level
  - **Enhanced**: Additional insights, including how Windows, Windows Server, System Center, and apps are used, how they perform, advanced reliability data, and data from both the Basic and the Security levels
  - **Full**: All data necessary to identify and help to fix problems, plus data from the Security, Basic, and Enhanced level.

  [System/AllowTelemetry CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## Search

- **Search location**: **Block** prevents Windows Search from using the location. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).