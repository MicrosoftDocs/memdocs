---
title: Overview of Windows Autopilot
description: Windows Autopilot is a collection of technologies used to set up and pre-configure new devices, getting them ready for productive use.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.topic: overview
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Overview of Windows Autopilot

Windows Autopilot is a collection of technologies used to set up and pre-configure new devices, getting them ready for productive use. Windows Autopilot can be used to deploy Windows PCs or HoloLens 2 devices. For more information about deploying HoloLens 2 with Autopilot, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

Windows Autopilot can also be used to reset, repurpose, and recover devices. This solution enables an IT department to achieve these goals with little to no infrastructure to manage, with a process that's easy and simple.

Windows Autopilot simplifies the Windows device lifecycle, for both IT and end users, from initial deployment to end of life. Using cloud-based services, Windows Autopilot:

- Reduces the time IT spends on deploying, managing, and retiring devices.
- Reduces the infrastructure required to maintain the devices.
- Maximizes ease of use for all types of end users.

See the following video:

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

> [!NOTE]
>
> This article is for **Windows Autopilot**. For **Windows Autopilot device preparation**, see [Overview of Windows Autopilot device preparation](device-preparation/overview.md).

## Process overview

When new Windows devices are initially deployed, Windows Autopilot uses the OEM-optimized version of Windows client. This version is preinstalled on the device, so custom images and drivers for every device model don't have to be maintained. Instead of re-imaging the device, the existing Windows installation can be transformed into a "business-ready" state that can:

- Apply settings and policies.
- Install apps.
- Change the edition of Windows being used to support advanced features. For example, from Windows Pro to Windows Enterprise.

:::image type="content" source="images/image1.png" alt-text="Process overview.":::

Once deployed, Windows devices can be managed with:

- Microsoft Intune.
- Windows Update for Business.
- Microsoft Configuration Manager.
- Other similar tools from non-Microsoft parties.

## Requirements

A [supported version](/windows/release-information/) of Windows semi-annual channel is required to use Windows Autopilot. For more information, see [Windows Autopilot software](requirements.md?tabs=software), [networking](requirements.md?tabs=networking), [configuration](requirements.md?tabs=configuration), and [licensing](requirements.md?tabs=licensing) requirements.

## Summary

Traditionally, IT pros spend significant time building and customizing images that are later deployed to devices. Windows Autopilot introduces a new approach.

- From the user's perspective, it only takes a few simple operations to make their device ready to use.
- From the IT pro's perspective, the only interaction required from the end user is to connect to a network and to verify their credentials. Everything beyond that is automated.

Windows Autopilot enables the following functionality:

- Automatic joining of devices to Microsoft Entra ID or Active Directory (via Microsoft Entra hybrid join). For more information about the differences between these two join options, see [Introduction to device management in Microsoft Entra ID](/azure/active-directory/device-management-introduction).
- Auto-enrollment of devices into mobile device management (MDM) services, such as Microsoft Intune ([*Requires a Microsoft Entra ID P1 or P2 subscription for configuration*](/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal)).
- Creation and auto-assignment of devices to configuration groups based on a device's profile.
- Customization of the out-of-box experience (OOBE) content specific to the organization.

Existing device can also be quickly prepared for a new user with [Windows Autopilot Reset](windows-autopilot-reset.md). The Reset capability is also useful in break/fix scenarios to quickly bring a device back to a business-ready state.

## Tutorial

For a tutorial with detailed instructions on configuring Windows Autopilot, see [Windows Autopilot scenarios](tutorial/autopilot-scenarios.md).

## Related content

- [Enroll Windows devices in Intune by using Windows Autopilot](enrollment-autopilot).
- [Windows Autopilot scenarios and capabilities](windows-autopilot-scenarios.md).
