---
# required metadata

title: Reset device passcodes with Microsoft Intune - Azure | Microsoft Docs
description: Remove or reset the passcode by using the remove passcode action on devices you manage or monitor with Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 47181d19-4049-4c7a-a8de-422206c4027e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
#SME:ileanawu
ms.collection: M365-identity-device-management
---

# Reset or remove a device passcode in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

This document discusses both device level passcode reset and work profile passcode reset on Android enterprise (formerly called Android for Work, or AfW) devices. It's important to note this distinction as requirements for each can vary. A device level passcode reset resets the passcode for the entire device. A work profile passcode reset resets the passcode only for the user’s work profile on Android enterprise devices.

## Supported platforms for device level passcode reset

| Platform | Supported? |
| ---- | ---- |
| Android devices on version 6.x or earlier | Yes |
| Android enterprise devices enrolled as Device Owner | Yes |
| iOS/iPadOS devices | Yes |
| iOS/iPadOS devices enrolled with User Enrollment | No |
| Android devices enrolled with a work profile | No |
| Android devices on version 7.0 or later | No |
| macOS | No |
| Windows | No |

For Android devices, this means that device level passcode reset is only supported on devices running 6.x or earlier, or on Android enterprise devices running in Kiosk mode. This is because Google removed support for resetting an Android 7 device’s passcode/password from within a Device Administrator granted app and applies to all MDM vendors.

## Supported platforms for Android enterprise work profile passcode reset

| Platform | Supported? |
| ---- | ---- |
| Android enterprise devices enrolled with a work profile and running version 8.0 and later | Yes |
| Android enterprise devices enrolled with a work profile and running version 7.x and earlier | No |
| Android devices running version 7.x and earlier | No |

To create a new work profile passcode, use the Reset Passcode action. This action prompts a passcode reset and creates a new, temporary passcode for the work profile only. 

## Reset a passcode


1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) with any of the following roles: Azure Active Directory Global Admin, Azure Active Directory Intune Service Admin, Helpdesk Operator, or Role Administrator.
2. Select **Devices**, and then select **All devices**.
3. From the list of devices you manage, select a device, and choose **Remove passcode**.

## Reset Android work profile passcodes

Supported Android Enterprise devices enrolled with a work profile receive a new managed profile unlock password or a managed profile challenge for the end user.

For Android Enterprise devices running version 8.x or later and enrolled with a work profile, end users get notified to activate their reset passcode right after enrollment is completed. The notification is displayed if a work profile password is required and set. Once their passcode is entered, the notification is dismissed.


## Remove iOS/iPadOS passcodes

Instead of being reset, passcodes are removed from iOS/iPadOS devices. If there's a passcode compliance policy set, the device will prompt the user to set a new passcode in Settings.

## Next steps

To see the status of the action you just took, in **Devices**, select **Device actions**.
