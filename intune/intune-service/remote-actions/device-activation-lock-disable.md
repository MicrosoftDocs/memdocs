---
# required metadata

title: Disable Activation Lock on Apple devices with Intune
titleSuffix: Microsoft Intune
description: Learn how to use Intune to disable Activation Lock on Apple devices to access locked devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/27/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 9ca3b0ba-e41c-45fb-af28-119dff47c59f

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Disable Activation Lock on Apple devices with Intune

> [!TIP]
> You can now turn off Activation Lock directly in Apple Business Manager and Apple School Manager. Learn more on [Apple's User Guide site.](https://support.apple.com/guide/apple-business-manager/axm812df1dd8/web)
Microsoft Intune can help you manage Activation Lock, a feature of the Find My iPhone app for iOS/iPadOS and macOS devices. Activation Lock is enabled automatically when a user sets up the Find My iPhone app on a device. After it's enabled, the user's Apple ID and password must be entered before anyone can:

- Turn off Find My iPhone
- Erase the device
- Reactivate the device

Supported platforms:

- iOS/iPadOS 7.1 or later (supervised through ADE)
- macOS 10.15 or later (supervised through ADE)

## How Activation Lock affects you

While Activation Lock helps secure Apple devices and improves the chances of recovering a lost or stolen device, this capability can present you, as an IT admin, with many challenges. For example:

- A user sets up Activation Lock on a device. The user then leaves the company and returns the device. Without the user's Apple ID and password, there's no way to reactivate the device.
- You want to reassign some devices to a different department during a device refresh in your organization. You can only reassign devices that don't have Activation Lock enabled.

To help solve these problems, Apple introduced the ability to disable Activation Lock for supervised devices, without the user's Apple ID and password. Supervised devices generate a device-specific Activation Lock bypass code, which is stored on Apple's activation server.

>[!TIP]
> Supervised mode can be configured through Apple Configurator to lock down a device and limit functionality to specific business purposes. This action is only supported on Supervised devices enrolled using Automated Device Enrollment program. [Apple's web site](https://developer.apple.com/documentation/devicemanagement/clear_the_bypass_code_for_activation_lock).

You can read more about Activation Lock on [Apple's web site](https://support.apple.com/HT201365).

## How Intune helps you manage Activation Lock

There are two methods to disabling Activation Lock on devices:

- Manually entering the Activation Lock bypass code on the device

- Using the Disable Activation Lock device action

For supervised devices, Intune stores the Activation Lock bypass code, which can be entered on the device to manually disable Activation Lock. If the device has been wiped, you can directly access the device by using a blank username and the code as the password.
Additionally, Intune can directly issue the bypass code to Apple's activation server to disable Activation Lock without having to interact with the device.  

**The business benefits of using Intune to manage Activation Lock are:**

- The user gets the security benefits of the Find My app.
- You can enable users to do their work and unlock it when a device needs to be repurposed, without needing the previous username or password.

## Before you start

Before you can disable Activation Lock on Apple devices, you must enable it by following these instructions:

1. Configure an Intune device restriction profile for iOS/iPadOS or macOS devices using the information in [How to configure device restriction settings](../configuration/device-restrictions-configure.md).
2. In the [device restriction settings for iOS/iPadOS](../configuration/device-restrictions-ios.md), or in the [device restrictions settings for macOS](../configuration/device-restrictions-macos.md), under the **General** settings, enable the option **Allow activation lock**.
3. Save the profile, and then [assign it](../configuration/device-profile-assign.md) to the devices on which you want to manage Disable Activation Lock.

## How to use Disable Activation Lock

>[!IMPORTANT]
>After you disable the Activation Lock on a device, if the Find My app is started, a new Activation Lock is automatically applied. So **you should be in physical possession of the device before you follow this procedure**.

The Intune **Disable Activation Lock** remote device action removes the Activation Lock on a device without requiring the current user's Apple ID and password. After you disable the Activation Lock, the device turns on Activation Lock again when the Find My app starts. Disable the Activation Lock only if you have physical access to the device.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. Next, select the device for which you'd like to disable Activation Lock.
4. In the **Overview** pane for the device, select the action **Disable Activation Lock** from the Device action menu.
5. Select **Hardware**, then find and copy the **Activation Lock bypass code** value under **Conditional Access**.

    >[!NOTE]
    >Copy the bypass code before you wipe the device. If you reset the device settings before you copy the code, the code is removed from Intune and is inaccessible.

6. In the **Overview** pane for the device, select **Wipe**.

>[!NOTE]
>In order to return activationLockBypassCode property using graph, it needs to be explicitly included in the request.
>If you send an unfiltered query to Graph API for the device object, a set of default values is returned and the activationLockBypassCode will be null.

## How to use the Activation Lock Bypass Code

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **All devices**.
1. Next, select the device for which you'd like to disable Activation Lock.
1. Select **Hardware**, then find and copy the Activation Lock bypass code value under **Conditional Access**.
1. In the **Overview** pane for the device, select the action **Wipe** in the Device action menu.
1. After the device is reset, you're prompted for the Apple ID and password. Leave the ID field blank, and then enter the **Activation Lock bypass code** for the password. This step removes the account from the device. On a macOS device, select **Recovery Assistant** in the menu bar and then select **Activate with MDM key** option to enter the bypass code.

## Next steps

You can examine the status of the unlock request on the details page for the device in the **Manage devices** workload.
