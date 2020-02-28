---
# required metadata

title: Windows 8.1 device restriction settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Learn the Intune settings you can use to control device settings and functionality on devices running Windows 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Intune Windows 8.1 device restriction settings

This article shows you the Microsoft Intune device restrictions settings that you can configure for devices running Windows 8.1.

## General

- **Diagnostic data submission** - Enables the device to submit diagnostic information to Microsoft.
- **Firewall** - Requires that the Windows Firewall is turned on.
- **User Account Control** - Requires the use of User Account Control (UAC) on devices.

## Password
- **Required password type** - Require the end user to enter a password to access the device.
- **Minimum password length** - Configures the minimum required length (in characters) for the password.
- **Number of sign-in failures before wiping device** - Wipes the device if the sign-in attempts fail this number of times.
- **Maximum minutes of inactivity until screen locks** - Specifies the number of minutes a device must be idle before a password is required to unlock it.
- **Password expiration (days)** - Specifies the number of days before the device password must be changed.
- **Prevent reuse of previous passwords** - Specifies whether the user can configure previously used passwords.
- **Picture password and PIN** - Enables the use of a picture password and PIN. A picture password lets the user sign in with gestures on a picture. A PIN lets users quickly sign in with a four-digit code.
- **Encryption** - Requires that files on the device are encrypted.<br>To enforce encryption on devices that run Windows 8.1, you must install the [December 2014 MDM client update for Windows](https://support.microsoft.com/kb/3013816) on each device.
If you enable this setting for Windows 8.1 devices, all users of the device must have a Microsoft account.
For encryption to work, the device must meet the [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) hardware certification requirements.
When you enforce encryption on a device, the recovery key is only accessible from the user's Microsoft account, which is accessed from their OneDrive account. You cannot recover this key on behalf of a user. 

## Browser
- **Autofill** - Enables users to change autocomplete settings in the browser.
- **Fraud warnings** - Enables or disables warnings for potential fraudulent websites.
- **SmartScreen** - Enables or disables warnings for potential fraudulent websites.
- **JavaScript** - Enables the browser to run scripts, such as Java script.
- **Pop-ups** - Enables or disables the browser pop-up blocker.
- **Send do-not-track headers** - Sends a do-not-track header to visited sites in Internet Explorer.
- **Plugins** - Enables users to add plug-ins to Internet Explorer.
- **Single word entry on intranet site** - Enables use of a single word to direct Internet Explorer to a web site, such as Bing.
- **Auto detect of intranet site** - Helps configure security for intranet sites in Internet Explorer.
- **Internet security level** - Sets the Internet Explorer security level for Internet sites.
- **Intranet security level** - Sets the Internet Explorer security level for intranet sites.
- **Trusted sites security level** - Configures the security level for the trusted sites zone.
- **High security for restricted sites** - Configures the security level for the restricted sites zone.
- **Enterprise mode menu access** - Lets users access the Enterprise Mode menu options from Internet Explorer.
If you select this setting, you can also specify a **Logging report location**, which contains a URL to a report that shows websites for which users have turned on Enterprise Mode access.
- **Enterprise mode site list location** - Specifies the location of the list of websites that use Enterprise Mode when it is active.

## Cellular
- **Data roaming** - Enables data roaming when the device is on a cellular network.

## Cloud and Storage
- **Work folders URL** - Sets the URL of the work folder to allow documents to be synchronized across devices.
- **Access to Windows Mail app without a Microsoft account** - Enables access to the Windows Mail application without a Microsoft account.

## Next steps

Create a device restrictions profile on [Windows 10 and newer](device-restrictions-windows-10.md).
