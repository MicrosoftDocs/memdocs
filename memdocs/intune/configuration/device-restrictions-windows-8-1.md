---
# required metadata

title: Windows 8.1 device restriction settings in Microsoft Intune
titleSuffix:
description: Learn the Intune settings you can use to control device settings and functionality on devices running Windows 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/16/2024
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
- tier3
- M365-identity-device-management
---

# Microsoft Intune Windows 8.1 device restriction settings

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

This article shows you the Microsoft Intune device restrictions settings that you can configure for devices running Windows 8.1.

## Before you begin

- [Create a Windows 8.1 device restrictions configuration profile](device-restrictions-configure.md#create-the-profile).

## General

- **Share usage data**: **Block** prevents devices from submitting diagnostic and usage information to Microsoft. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Firewall**: **Require** the Windows Firewall be turned on. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **User Account Control**: Configures User Account Control (UAC). Choose how users are notified of changes on devices. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Always notify**
  - **Notify on app changes**
  - **Notify on app changes (but do not dim desktop)**
  - **Never notify**

## Password

- **Required password type**: Choose if user must enter a password to access the device. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Alphanumeric**: Password must be a mix of numbers and letters.
  - **Numeric**: Password must only be numbers.
- **Minimum password length**: Enter the minimum number of characters required, from 6-16. For example, enter `6` to require at least six numbers or characters in the password length.
- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 1-14.
- **Maximum minutes of inactivity until screen locks**: Enter the length of time a device must be idle before the screen is automatically locked, from 1-60 minutes. For example, select `5 minutes` to lock the device after 5 minutes of being idle. When set to **Not configured**, Intune doesn't change or update this setting.
- **Password expiration (days)**: Enter the length of time in days when the device password must be changed, from 1-255. For example, enter `90` to expire the password after 90 days. When the value is blank, Intune doesn't change or update this setting.
- **Prevent reuse of previous passwords**: Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Picture password and PIN**: A picture password lets the user sign in with gestures on a picture. A PIN lets users quickly sign in with a four-digit code.

  **Block** prevents using a picture or PIN as the password. When set to **Not configured** (default), Intune doesn't change or update this setting.

- **Encryption**: **Require** encryption on devices, including files. Not all devices support encryption. When set to **Not configured**, Intune doesn't change or update this setting.

  To configure this setting, and correctly report compliance, also configure:

  - **Required password type**: Set to at least **Numeric**.
  - **Minimum password length**: Set to at least `6`.

  To enforce encryption on devices that run Windows 8.1, you must install the [December 2014 MDM client update for Windows](https://support.microsoft.com/kb/3013816) on each device.

  If you enable this setting for Windows 8.1 devices, all users of the device must have a Microsoft account.

  For encryption to work, devices must meet the [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) hardware certification requirements.

  When you enforce encryption on a device, the recovery key is only accessible from the user's Microsoft account, which is accessed from their OneDrive account. You can't recover this key for a user.

## Browser

- **Autofill**: **Block** prevents users from changing autocomplete settings in the browser, and from populating form fields automatically. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Autofill.
- **Fraud warnings**: **Require** shows fraud warnings in the browser for potential fraudulent websites. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **SmartScreen for Microsoft Edge Legacy**: **Block** turns off Microsoft Defender SmartScreen. SmartScreen look for potential phishing scams and malicious software when accessing sites and file downloads. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn on SmartScreen.
- **Allow JavaScript**: **Block** prevents scripts, like JavaScript, to run in the browser. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow JavaScript.
- **Pop-ups**: **Block** turns on Pop-up Blocker to prevent pop-ups in the web browser. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Do-not-track headers**: **Block** prevents devices from sending do-not-track headers to websites requesting tracking info. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Plugins**: **Block** prevents users from adding plug-ins in Internet Explorer. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Single word entry on intranet site**: Single word entry lets users go to an intranet site by entering a single word, like `hr` or `benefits`. **Block** prevents this feature. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Auto detect of intranet site**: **Block** prevents the browser from automatically detecting intranet sites. Intranet mapping rules are blocked. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Internet security level**: Sets the security level for Internet sites. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **High**
  - **Medium-high**
  - **Medium**
- **Intranet security level**: Sets the security level for intranet sites. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **High**
  - **Medium-high**
  - **Medium**
  - **Medium-low**
  - **Low**

- **Trusted sites security level**: Configures the security level for the trusted sites zone. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **High**
  - **Medium-high**
  - **Medium**
  - **Medium-low**
  - **Low**
- **High security for restricted sites**: Configures the security level for the restricted sites zone. **Configured** enforces high security for restricted sites. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Enterprise mode menu access**: **Block** prevents users from accessing the Enterprise Mode menu options in Internet Explorer. When set to **Not configured** (default), Intune doesn't change or update this setting.

  When set to **Not configured**, also enter:

  - **Logging report location URL**: Enter a URL location where to get reports that show the websites with Enterprise Mode access turned on.

- **Enterprise mode site list location (Desktop only)**: Enter the location of the websites list that can be opened in Enterprise Mode.

## Cellular

- **Data roaming**: **Block** prevents data roaming when devices are on a cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Cloud and Storage

- **Work folders URL**: Enter the work folder URL to allow documents to be synchronized across devices. When set to **Not configured** (default) or left blank, Intune doesn't change or update this setting.
- **Access to Windows Mail app without a Microsoft account**: **Block** prevents access to the Windows Mail application without a Microsoft account. When set to **Not configured** (default), Intune doesn't change or update this setting.

## Related articles

- Create a device restrictions profile on [Windows 10 and newer](device-restrictions-windows-10.md).
