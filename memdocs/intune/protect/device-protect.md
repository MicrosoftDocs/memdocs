---
# required metadata

title: Protect devices with Microsoft Intune 
titleSuffix: Microsoft Intune
description: Learn about some of the ways that Intune can help you protect your devices against unauthorized access and other threats.
keywords:
author: brenduns   
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2018
ms.topic: conceptual
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Protect devices with Microsoft Intune

Microsoft Intune helps you protect the devices you manage and the data stored on those devices.

## Device configuration
Intune [configuration policies](../configuration/device-profiles.md) help you protect and configure devices by controlling a multitude of settings and features. For example:

- You can restrict use of hardware features on the device such as the camera, or Bluetooth.
- You can configure compliant and noncompliant apps. You'll get an alert if a noncompliant app is installed (and some platforms can actually block the install).

## Reset passcodes when users are locked out of their devices
Since the first step in protecting company data on mobile devices is to require a passcode to use the device, sometimes you have to [reset a passcode](../remote-actions/device-passcode-reset.md) or help an employee do so, either by removing the passcode or setting a temporary passcode remotely. You can also [lock a device remotely](../remote-actions/device-remote-lock.md) if it's lost or stolen.

## Retire devices and remove data
When a device needs to be [removed from Intune management](../remote-actions/devices-wipe.md) (for example, a user leaves, or the device is lost or stolen), it's likely that you'll want to remove data from that device. Intune provides a range of methods to make sure your company data stays secure.

## Require devices to be compliant
Intune features [device compliance policies](device-compliance-get-started.md) that let you evaluate (and in some cases remediate) devices that aren't compliant with rules that you specify. For example, you can get reports on:
- jailbroken iOS/iPadOS devices
- encrypted or not encrypted devices
- the health of Windows 10 devices (as determined by the Health Attestation Service).

## Protect apps and the data they use
Intune gives you a range of features to help you protect apps and their data. For example, mobile application management (MAM) policies can:
- prevent data from being backed up from a protected app
- restrict copy and paste to other apps
- require a PIN to access an app
For more information, see [Protect apps and data with Microsoft Intune](../apps/app-protection-policy.md)

## Add an additional layer of protection to devices
[Multi-factor authentication (MFA)](../enrollment/multi-factor-authentication.md) is a more secure way of authenticating the users of devices on the network.  With MFA, users need to confirm their identity beyond user name and password, through a phone call, or text message.

## Control Windows Hello for Business settings on Windows devices
Intune lets you integrate with [Windows Hello for Business](windows-hello.md) which is an alternative sign-in method for Windows 10 and later that uses Active Directory, or an Azure Active Directory account to replace a password, smart card, or virtual smart card.

## Disable Activation Lock on iOS devices
Activation Lock is a feature that help protect users' devices. The feature requires users to enter their Apple ID and password before anyone can erase or reactivate the device. However, this feature can lead to problems, for example if the user leaves the company without removing the lock. [Disable iOS/iPadOS Activation Lock](../remote-actions/device-activation-lock-disable.md) can help by removing the lock from supervised iOS/iPadOS devices allowing you to reallocate, or erase them.

## Next steps

Learn about [mobile threat defense](mobile-threat-defense.md)
