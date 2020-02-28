---
# required metadata

title: Rename a device with Microsoft Intune - Azure | Microsoft Docs
description: Rename a device by using Microsoft Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Rename a device in Intune

The **Rename device** action lets you rename a device that is enrolled in Intune. The device's name is changed in Intune and on the device.

You can rename the following types of devices:
- corporate-owned Windows 
- iOS/iPadOS supervised
- corporate-owned MacOS 10

This feature doesn't currently support renaming hybrid Azure AD Windows devices.

## Rename a device

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Choose **Devices** > **All devices** > choose a device > **More** > **Rename device**.
4. In the **Rename device** blade, type the new name in the text box. You can use letters, numbers, and hyphens. The name must contain at least one letter or hyphen.
5. If you want to restart the device after renaming it, choose **Yes** next to **Restart after rename**.
6. Choose **Rename**.

## Windows device rename rules
When renaming a Windows device, the new name must follow these rules:
- 15 characters or less (must be less than or equal to 63 bytes, not including trailing NULL)
- Not null or an empty string
- Allowed ASCII: Letters (a-z, A-Z), numbers (0-9), and hyphens
- Allowed Unicode: characters >= 0x80, must be valid UTF8, must be IDN-mappable (that is, RtlIdnToNameprepUnicode succeeds; see RFC 3492)
- Names must not contain only numbers
- No spaces in the name
- Disallowed characters: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)


## Next steps

To see the status of the **Rename** device action, check the **Overview** page for the device.
