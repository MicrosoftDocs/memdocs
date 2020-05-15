---
# required metadata

title: Microsoft Intune device restriction settings for Windows Phone 8.1
titleSuffix:
description: Learn the Intune settings you can use to control device settings and functionality on devices running Windows Phone 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Intune Windows Phone 8.1 device restriction settings

This article shows you the Microsoft Intune device restrictions settings that you can configure for devices running Windows Phone 8.1.

## General

- **Camera**: **Block** prevents access to the device camera. When set to **Not configured** (default), Intune doesn't change or update this setting.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

- **Copy and paste**: **Block** prevents using copy-and-paste between apps on the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Removable storage**: **Block** prevents using external storage devices on devices, such as SD cards. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Geolocation**: **Block** prevents turning on location services on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Microsoft account**: **Block** prevents users from associating a Microsoft account with the device. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Screen capture**: **Block** prevents getting screenshots on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Diagnostic data submission**: **Block** blocks devices from sending diagnostic and usage telemetry data to Microsoft. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Custom email accounts sync**: **Block** prevents devices from connecting to non-Microsoft email accounts. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Password

- **Password**: **Require** forces users to enter a password to access devices. When set to **Not configured** (default), Intune doesn't change or update this setting. Applies to local accounts only. Domain account passwords remain configured by Active Directory (AD) and Azure AD.
  - **Required password type**: Choose the type of password. Your options:
    - **Device default**: Password can include numbers and letters.
    - **Alphanumeric**: Password must be a mix of numbers and letters.
    - **Numeric**: Password must only be numbers.
  - **Minimum password length**: Enter the minimum number of characters required, from 4-16. For example, enter `6` to require at least six characters in the password length.
  - **Simple passwords**: **Block** prevents users from creating simple passwords, such as `1234` or `1111`. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before devices are wiped.
  - **Maximum minutes of inactivity until screen locks**: Enter the length of time a device must be idle before the screen is automatically locked. For example, enter `5` to lock devices after 5 minutes of being idle. When set to **Not configured** or left blank, Intune doesn't change or update this setting.
  - **Password expiration (days)**: Enter the length of time in days when the device password must be changed, from 1-255. For example, enter `90` to expire the password after 90 days. When the value is blank, Intune doesn't change or update this setting.
  - **Prevent reuse of previous passwords**: Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Encryption**: **Require** encryption on device, including files. Not all devices support encryption. When set to **Not configured** (default), Intune doesn't change or update this setting. To configure this setting, and correctly report compliance, also configure:
  - **Require password**: Set to **Require**.
  - **Required password type**: Set to at least **Numeric**.
  - **Minimum password length**: Set to at least `4`.

## App Store

- **App store**: **Block** prevents users from accessing the app store. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Restricted apps

In the restricted apps list, you can configure one of the following lists:

- **Blocked apps**: List the apps (not managed by Intune) that users are not allowed to install and run.
- **Allowed apps**: List the apps that users are allowed to install. Apps that are managed by Intune are automatically allowed.

To configure the list, click **Add**, then specify a name of your choice, optionally the app publisher, and the URL to the app in the app store.

### How to specify the URL to an app in the store

To specify an app URL in the allowed and blocked apps list, use the following format:

From the [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) page, search for the app that you want to use.

Open the app's page, and copy the URL to the clipboard. You can now use this URL as the URL in either the allowed or blocked apps list.

Example: Search the store for the Skype app. The URL you use is `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### Additional options

You can also click **Import** to populate the list from a csv file in the format <*app url*>, <*app name*>, <*app publisher*>, or click **Export** to create a csv file containing the contents of the restricted apps list in the same format.

## Browser

- **Web browser**: **Block** turns off the built-in web browser on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Cellular and Connectivity

- **Wi-Fi**: **Block** disables the Wi-Fi functionality on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Wi-Fi tethering**: **Block** prevents using Wi-Fi tethering on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Automatically connect to Wi-Fi hotspots**: Enables devices to automatically connect to free Wi-Fi hotspots and automatically accept any terms of use.
- **Wi-Fi hotspot reporting**: **Block** prevents devices from sending Wi-Fi hotspot connection information. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **NFC**: **Block** disables operations that use near field communication (NFC) on devices that support it. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Bluetooth**: **Block** prevents users from enabling Bluetooth. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Next steps

For a general overview of the device restrictions profile, see [Configure device restriction settings in Microsoft Intune](device-restrictions-configure.md).
