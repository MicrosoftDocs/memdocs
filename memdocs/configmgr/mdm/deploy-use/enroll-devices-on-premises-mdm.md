---
title: Enroll devices for on-premises MDM
titleSuffix: Configuration Manager
description: Learn about methods to enroll devices for on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Enroll devices for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

To manage devices with Configuration Manager on-premises mobile device management (MDM), you first need to enroll them. Then Configuration Manager can communicate with the devices for management tasks. Configuration Manager provides two methods to enroll devices:

- **User enrollment**: Users start the enrollment process on their device. For user enrollment to succeed, install the trusted root certificate on the device, and provision the user for enrollment in client settings. To enroll a device, the user only needs to enter their credentials.

    For more information, see [How users enroll devices](user-enroll-devices-on-premises-mdm.md).

- **Bulk enrollment**: The user of the device doesn't start enrollment. You create a bulk enrollment package in Configuration Manager. When you open it on the device, the package provides the information required to enroll the device.

    For more information, see [How to bulk-enroll devices](bulk-enroll-devices-on-premises-mdm.md).

For more information on the OS versions that Configuration Manager supports for device enrollment in on-premises MDM, see [Supported configurations](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
