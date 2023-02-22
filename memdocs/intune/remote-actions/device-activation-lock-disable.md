---
# required metadata

title: Bypass iOS/iPadOS Activation Lock with Intune
titleSuffix: Microsoft Intune
description: Learn how to use Intune to bypass iOS/iPadOS Activation Lock to access locked devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 9ca3b0ba-e41c-45fb-af28-119dff47c59f

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Disable Activation Lock on Supervised iOS/iPadOS devices with Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune can help you manage iOS/iPadOS Activation Lock, a feature of the Find My iPhone app for iOS/iPadOS 8.0 and later devices. Activation Lock is enabled automatically when a user opens the Find My iPhone app on a device. After it is enabled, the user's Apple ID and password must be entered before anyone can:

- Turn off Find My iPhone
- Erase the device
- Reactivate the device

## How Activation Lock affects you

While Activation Lock helps secure iOS/iPadOS devices and improves the chances of recovering a lost or stolen device, this capability can present you, as an IT admin, with a number of challenges. For example:

- A user sets up Activation Lock on a device. The user then leaves the company and returns the device. Without the user's Apple ID and password, there is no way to reactivate the device.
- You need a report of all devices that have Activation Lock enabled.
- You want to reassign some devices to a different department during a device refresh in your organization. You can only reassign devices that do not have Activation Lock enabled.

To help solve these problems, Apple introduced Activation Lock disable in iOS/iPadOS 7.1. Disable Activation Lock lets you remove the Activation Lock from supervised devices without the user's Apple ID and password. Supervised devices can generate a device-specific Activation Lock bypass code, which is stored on Apple's activation server.

>[!TIP]
>Supervised mode for iOS/iPadOS devices lets you use Apple Configurator to lock down a device and limit functionality to specific business purposes. Supervised mode is used only for corporate-owned devices.

You can read more about Activation Lock on [Apple's web site](https://support.apple.com/HT201365).

## How Intune helps you manage Activation Lock
Intune can request the Activation Lock status of supervised devices that run iOS/iPadOS 8.0 and later. For supervised devices only, Intune can retrieve the Disable Activation Lock code and directly issue it to the device. If the device has been wiped, you can directly access the device by using a blank user name and the code as the password.

**The business benefits of using Intune to manage Activation Lock are:**

- The user gets the security benefits of the Find My iPhone app.
- You can enable users to do their work and know that when a device needs to be repurposed, you can retire or unlock it.

## Before you start
Before you can disable Activation Lock on devices, you must enable it by following these instructions:

1. Configure an Intune device restriction profile for iOS/iPadOS using the information in [How to configure device restriction settings](../configuration/device-restrictions-configure.md).
2. In the [device restriction settings for iOS/iPadOS](../configuration/device-restrictions-ios.md), under the **General** settings, enable the option **Activation Lock**.
3. Save the profile, and then [assign it](../configuration/device-profile-assign.md) to the devices on which you want to manage Disable Activation Lock.


## How to use Disable Activation Lock

>[!IMPORTANT]
>After you disable the Activation Lock on a device, if the Find My iPhone app is started, a new Activation Lock is automatically applied. Because of this, **you should be in physical possession of the device before you follow this procedure**.

The Intune **Disable Activation Lock** remote device action removes the Activation Lock from an iOS/iPadOS device without requiring the user's Apple ID and password. After you disable the Activation Lock, the device turns on Activation Lock again when the Find My iPhone app starts. Disable the Activation Lock only if you have physical access to the device.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. On the **Intune** blade, select **Devices**.
3. On the **Devices** blade, select **All devices**.
4. Go to the device's "Hardware" section, and then copy the **Activation Lock bypass code** value under **Conditional Access**.

    >[!NOTE]
    >Copy the bypass code before you wipe the device. If you reset the device settings before you copy the code, the code is removed from Azure.

5. Go to the **Overview** blade for the device, and then select **Wipe**.
6. After the device is reset, you are prompted for the *Apple ID* and *password*. Leave the *ID* field blank, and then enter the **bypass code** for the *password*. This removes the account from the device. 

>[!NOTE]
>In order to return activationLockBypassCode property using graph, it needs to explicitly included in the request. 
>If you send an unfiltered query to Graph API for the device object, a set of default values is returned and activationLockBypassCode will be null.

## Next steps

You can examine the status of the unlock request on the details page for the device in the **Manage devices** workload.
