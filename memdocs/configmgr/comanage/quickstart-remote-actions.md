---
title: Remote actions with co-management
titleSuffix: Configuration Manager
description: Run remote actions from Intune for co-managed devices
ms.date: 11/08/2021
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Remote actions with co-management

You need to make sure that every device you manage is reachable, no matter where it is, whenever it connects. You also need to provide each user with everything they need to stay productive, while protecting the apps and data. With the device actions supported by Intune, you can remotely solve these critical functions.

In the following video, principal program manager Heidi Cheng and senior program manager Danny Guillory discuss and demo remote actions with co-management:

> [!VIDEO https://aka.ms/docs/player?id=0c095272-87a5-40d3-af67-c420c010c783]

## Benefits

Remote device actions give you management controls on the device without interfering with personal data. These remote device actions allow you to:

- Delete company data on lost or stolen devices
- Rename a device
- Restart a device
- Review device inventory
- Remotely control a device
- Wipe out pre-installed OEM apps with a Fresh Start reboot
- Do a factory reset on any Windows 10 or later device

These functions are an important and simple way to protect corporate data stored on these devices, whether in e-mail or OneDrive.

For more information on these actions, see [Available remote actions](#available-remote-actions).

## Case studies

The global consulting firm Avanade regularly uses remote actions to manage the devices used by their 30,000 employees. In a [blog post](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), the CIO of Avanade noted:

> *Our immediate win from having the Intune functionality was the ability to remotely reset Windows on a machine. This is important to us for lost or stolen machines, which is more common in our highly mobile workforce.*
> *This is functionality that we otherwise would have had to build and maintain in a custom ConfigMgr package.*

For more information on how to use these remote actions, see [Available device actions](../../intune/remote-actions/device-management.md#available-device-actions).

## Value proposition

When a Configuration Manager device is co-managed, it immediately adds these functions that Configuration Manager doesn't natively have. Now you can now do any remote action that's supported by Intune.

With co-management, the Configuration Manager devices are now just like any other Intune-managed device. For example, they have a full presence in the cloud, and you can reach them as long as they have internet access. You can do all of these actions without taking any additional steps beyond enabling co-management.

Since the auto-enrollment process is transparent to the user, there's no impact to their productivity. The user doesn't need to do anything.

### Available remote actions

Use these remote actions from Intune once you [enable co-management](how-to-enable.md) in Configuration Manager.

#### Remove devices

- **Retire**: This action removes managed apps and data (where applicable), settings, and e-mail profiles that were assigned to that device. The device is then removed from Intune management. This process happens the next time the device checks in and receives the remote retire action. The Retire function leaves the user's personal data on the device.

- **Wipe**: This action restores a device to its factory default settings. If you choose the option to **Retain enrollment state and user account**, then the user data is kept. Otherwise the drive is securely erased.

- **Delete**: If you want to remove devices from the Microsoft Intune admin center, delete them from the specific device pane. The next time the device checks in, it removes any organizational data stored on it.

For more information, see [Remove devices by using wipe, retire, or manually unenrolling the device](../../intune/remote-actions/devices-wipe.md).

#### Selective wipe
<!--SCCMDocs issue 973-->

When you choose an **App selective wipe**, it removes company app data without removing personal data. Use this action when a device is reported as lost or stolen.

For more information, see [How to wipe only corporate data from Intune-managed apps](../../intune/apps/apps-selective-wipe.md).

#### Sync

The **Sync** device action forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies that you've assigned to it.

This feature can help you immediately validate and troubleshoot policies you've assigned, without waiting for the next scheduled check-in.

For more information, see [Sync devices to get the latest policies and actions with Intune](../../intune/remote-actions/device-sync.md).

#### Restart

The **Restart** device action causes the device you choose to restart. This action is useful when there's a pending reboot, but the user isn't available to do it.

For more information, see [Remotely restart devices with Intune](../../intune/remote-actions/device-restart.md).

#### Fresh Start

The **Fresh Start** device action removes any apps installed on a device running Windows 10, version 1703 or later. Fresh Start helps remove pre-installed (OEM) apps that are typically installed with a new device.

If you choose not to retain user data, the device restores to its out-of-box state. It unenrolls from Azure AD and MDM.

If you have predetermined standards regarding what apps should be on the device, then this action eliminates the ones that don't meet your criteria.

For more information, see [Use Fresh Start to reset Windows devices with Intune](../../intune/remote-actions/device-fresh-start.md).

#### Remote control

Devices managed by Intune can be administered remotely using [TeamViewer](https://www.teamviewer.com/). TeamViewer is a third-party program that you acquire separately.

For more information, see [Use TeamViewer to remotely administer Intune devices](../../intune/remote-actions/teamviewer-support.md).

## Configure

Other than remote control via TeamViewer, to start using these remote device actions in Intune, no additional setup is required after you [enable co-management](how-to-enable.md).

For more information on using TeamViewer for remote control, see [Use TeamViewer to remotely administer Intune devices](../../intune/remote-actions/teamviewer-support.md).
