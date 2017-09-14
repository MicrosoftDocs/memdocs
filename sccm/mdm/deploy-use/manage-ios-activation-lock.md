---
title: "Manage iOS Activation Lock | Microsoft Docs"
description: "Manage iOS Activation Lock with System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe

---
# Manage iOS Activation Lock with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. When Activation Lock is enabled, the user's Apple ID and password must be entered before anyone can:

- Turn off Find My iPhone
- Erase the device
- Reactivate the device

On **unsupervised** devices, Activation Lock is enabled automatically when the Find My Iphone app is used.

On **supervised** devices, you must activate Activation Lock by using Configuration Manager compliance settings.

> [!TIP]
> Supervised mode for iOS devices lets you use the Apple Configurator Tool to lock down a device to limit functionality to specific business purposes. Supervised mode is generally only for corporate-owned devices.

While Activation Lock helps secure iOS devices and improves the chances of recovery if they are lost and stolen, this capability can present you, as an IT admin, with a number of challenges. For example:

- One of your users sets up Activation Lock on a device. The user then leaves the company and returns the device. Without the user's Apple ID and password, there is no way to reactivate the device, even if you wipe it.
- You need a report of all devices that have Activation Lock enabled.
- During a device refresh in your organization, you want to reassign some devices to a different department. You can only reassign devices that do not have Activation Lock enabled.


To help solve these problems, Apple introduced Activation Lock bypass in iOS 7.1. This lets you remove the Activation Lock from supervised devices without the user's Apple ID and password. Supervised devices can generate a device-specific Activation Lock bypass code, which is stored on Apple's activation server.

You can read more about Activation Lock [here](https://support.apple.com/HT201365).

## How Configuration Manager helps you manage Activation Lock

Configuration Manager can help you manage Activation Lock in two ways:

1. Enable Activation Lock on supervised devices.
2. Bypass Activation Lock on supervised devices.

> [!IMPORTANT]
> You cannot bypass Activation Lock on unsupervised devices.

The business benefits of this for corporate-owned devices are:



- The user gets the security benefits of the Find My iPhone app
- You can enable the user to do their work knowing that when the device needs to be repurposed, you can retire or unlock it


## Enable Activation Lock on supervised devices

You use Configuration Manager compliance settings to create and deploy a configuration item of the type **iOS and Mac OS X** to enable Activation Lock on supervised devices:

1. Use the information in the topic [How to create configuration items for iOS and Mac OS X devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) to create a configuration item of the type **iOS and Mac OS X**.
2. On the **System Security** page of the Create Configuration Item Wizard, configure the setting **Allow Activation Lock (supervised mode only)** to **Allowed**.
3. [Add the configuration item to a configuration baseline](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Deploy this configuration baseline](/sccm/compliance/deploy-use/deploy-configuration-baselines) to a collection containing the iOS devices for which you want to enable Activation Lock.

> [!IMPORTANT]
> Ensure you are in physical possession of the device before you follow this procedure. If you do not, the Activation Lock will be bypassed and whoever is in possession of the device will have full access to it, allowing them to turn off Find My iPhone, erase the device, or reactivate it.

You can only bypass Activation Lock or retrieve the Activation Lock bypass code on supervised devices; trying to bypass activation lock on an unsupervised device or view the bypass code results in an error.



## View the Activation Lock bypass code

1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, click **Devices**.
3. Select an enrolled device that is in supervised mode that has Activation Lock enabled.
4. On the **Home** tab, in the **Device** group, click **Remote Device Actions** > **View Activation Lock Bypass Code**.
5. The **Activation Lock Bypass Code** dialog box displays the bypass code for the selected device.

## Bypass Activation Lock

1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, click **Devices**.
3. Select an enrolled device that is in supervised mode that has Activation Lock enabled.
3. On the **Home** tab, in the **Devices** group, click **Remote Device Actions** > **Bypass Activation Lock**.
5. Read the messages in the warning dialog box, and click **Yes** when you are ready to proceed.
6. You can examine the status of the unlock request from:

	- The discovery data for the device in the device properties dialog box.
	- The **Activation Lock Bypass State** column in the **Devices** view (this column is hidden by default).
	- The **Remote Device Actions Information** section in the **Summary** tab of the details pane (when a device is selected).
