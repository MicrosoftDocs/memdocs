---
title: Windows Autopilot overview
description: Overview of Windows Autopilot.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/18/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot in Intune overview

Windows Autopilot is a technology that allows configuration of a device upon first use. Normally this would be when a new device is first delivered to an end-user via an OEM, reseller, or IT organization. However, it can also be used to reset an existing devices. After the reset, the existing device can then be configured by going through the Windows Autopilot process. Windows Autopilot is a key component of the Windows modern deployment strategy.

Configurations that can be performed by Windows Autopilot include:

- Applying of settings and policies.
- Installation of applications.
- Changing of Windows edition, for example Windows Pro to Windows Enterprise.
- Automatically joining of devices into Azure Active Directory (Azure AD) or Active Directory (via hybrid Azure AD join).
- Auto-enrollment into MDM solutions such as Microsoft Intune.

Windows Autopilot is a separate technology from Intune and can be used with various MDM solutions other than Intune. However, for the purposes of this tutorial, the tutorial will focus on using Windows Autopilot with Intune.

> [!VIDEO https://www.youtube.com/watch?v=zqwkaWTzsRo]

## Benefits of Windows Autopilot

Windows Autopilot simplifies the Windows device lifecycle, for both IT and end-users, from initial deployment to end of life. Using cloud-based services instead of on-premises infrastructure, Windows Autopilot can:

- Reduce the time IT spends on deploying, managing, and retiring devices.
- Reduce the infrastructure required to maintain the devices.
- Maximizes ease of use for all types of end-users.

## Differences between Windows Autopilot and traditional deployment methods

When compared to traditional deployment methods, such as Microsoft Configuration Manager Operating System Deployment or Microsoft Deployment Toolkit, Windows Autopilot offers several advantages:

- Reduces the on-premises infrastructure required to deploy devices by using cloud services.
- Eliminates the need to create and maintain operating system images.
- Eliminates the need to manage drivers.
- Simplifies the process of deploying devices to end-users that are remote.
- Autopilot is built into Windows. An additional client or agent isn't required and doesn't need to be installed. Additionally, if needed the Autopilot service will automatically update itself during the Autopilot process.

Unlike traditional Windows deployment methods that apply Windows images to devices during the deployment process, Windows Autopilot normally uses the preinstalled OEM image and drivers.

## Windows Autopilot scenarios

Due to different environments, different configurations, and different needs, Windows Autopilot supports several different scenarios. The following scenarios are available in Windows Autopilot:

| Scenario | Purpose | Description |
| --- | --- |
| Windows Autopilot user-driven mode | Device for a single user | Windows is setup and configured |
| Windows Autopilot for pre-provisioned | Device for a single user | |
| Windows Autopilot self-deploying mode | | |
| Windows Autopilot for existing devices | | |
| Windows Autopilot Reset | | |



## More information

For more information, see the following article(s):
