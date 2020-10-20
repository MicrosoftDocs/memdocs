---
title: Windows Autopilot enrollment overview
ms.reviewer: 
manager: laurawi
description: High-level overview of the Windows Autopilot enrollment process.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: erikjeMS
ms.author: erikje
ms.topic: article
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---


# Windows Autopilot enrollment overview

The enrollment process for Windows Autopilot devices includes setting up your Intune profiles and policies to deploy the devices with the configuration and apps that you define. At a high level, the process goes like this:

1. Add devices to the Windows Autopilot service. Before you can enroll Autopilot devices, those devices must be [registered](add-devices.md). To register the devices, data about those devices must first be added to your Mobile Device Management (MDM) service. The instructions in this section assume you’ll be using Intune for your MDM. You have two primary ways to add devices:
    - You can grant your OEM or other hardware partner permission to add devices to Intune. They’ll add pertinent data about each device, including a hardware hash that uniquely identifies each device.
    - If your OEM/partner doesn’t add the devices, you can [add devices](enrollment-autopilot.md#add-devices) to Intune by importing a CSV file that lists the pertinent data. 
2. Intune communicates with the Autopilot service which uses the hardware hashes to register each device.
3. You [create an Autopilot device group](enrollment-autopilot.md#create-an-autopilot-device-group) to identify the devices that you want to enroll. You’ll use a special Advanced rule code to include Autopilot devices in this group.
4. You [create an Autopilot deployment profile](enrollment-autopilot.md#create-an-autopilot-deployment-profile) to define how the Autopilot devices are configured. This includes the Out of Box Experience (OOBE) like deployment mode (user-drive or self-deploying), the directory service to join, which screens to show the user during setup, and so on.
5. Intune periodically checks for new devices in the assigned groups and assigns the profiles to those devices. You can check the profile assignment status by going to Devices > Windows > Windows enrollment > Devices (under Windows Autopilot Deployment Program). The device is ready to deploy when the status says Assigned.
6. After the profile has been assigned, you can start deploying the devices.
    a. Send the devices to the end users.
    b. Each end user starts up the device and signs in, which starts the Autopilot configuration of the device

## Next steps

Learn more about [adding devices](add-devices.md).
