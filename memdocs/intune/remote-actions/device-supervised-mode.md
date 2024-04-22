---
# required metadata

title: Turn on iOS/iPadOS supervised mode with Microsoft Intune 
titleSuffix: 
description: Learn how to turn on iOS/iPadOS supervised mode with Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 11/23/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Turn on iOS/iPadOS supervised mode

Apple iOS/iPadOS supervised mode gives administrators more options when managing Apple devices, making it useful for corporate-owned devices deployed at scale. For example, you can restrict AirDrop or prevent users from changing the name of the device. For a list of settings which require supervised mode, see [iOS device restriction settings in Intune](../configuration/device-restrictions-ios.md).

Intune supports supervised mode as part of the Apple [Device Enrollment Program (DEP)](../enrollment/device-enrollment-program-enroll-ios.md).

For a list of Apple controls that require supervision, see Apple's [Payload settings reference](https://support.apple.com/guide/deployment/depcdc2bfa19/web).

## Turn on supervised mode during enrollment

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can turn on supervised mode for devices when you [create an Apple enrollment profile in DEP](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile). Under **Device Management Settings**, check the **Supervised** box.

## Turn on supervised mode after enrollment

After enrollment, the only way to turn on supervised mode is to connect an iOS/iPadOS device to a Mac and [use the Apple Configurator](../enrollment/apple-configurator-enroll-ios.md) (which will reset the device). You can't configure a device for Supervised mode in Intune after enrollment.

Apple Configurator for iPhone can also be used to supervise devices.
For more information, see the [Apple support doc](https://support.apple.com/guide/apple-configurator/intro-apd4015ec300/1.1/ios/17.0).

## Identify a supervised device

To determine if a device is supervised, check the **Settings** app:

Users are notified that their devices are supervised in the **Settings** app. In the app at the top of the screen, a static message shows the message **This iPhone is supervised and managed by *`<your organization>`***.  

## Next steps

For other device management options, see [What is Microsoft Intune device management?](device-management.md)
