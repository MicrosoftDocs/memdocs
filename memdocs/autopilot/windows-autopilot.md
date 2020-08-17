---
title: Overview of Windows Autopilot
description: Windows Autopilot is a collection of technologies used to set up and pre-configure new devices, getting them ready for productive use. 
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
---


# Overview of Windows Autopilot

**Applies to**

-  Windows 10

Windows Autopilot is a collection of technologies used to set up and pre-configure new devices, getting them ready for productive use. You can also use Windows Autopilot to reset, repurpose, and recover devices. This solution enables an IT department to achieve the above with little to no infrastructure to manage, with a process that's easy and simple.

Windows Autopilot simplifies the Windows device lifecycle, for both IT and end users, from initial deployment to end of life. Using cloud-based services, Windows Autopilot:
- reduces the time IT spends on deploying, managing, and retiring devices.
- reduces the infrastructure required to maintain the devices.
- maximizes ease of use for all types of end users.

See the following video and diagram:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Process overview](images/image1.png)

When initially deploying new Windows devices, Windows Autopilot uses the OEM-optimized version of Windows 10. This version is preinstalled on the device, so you don't have to maintain custom images and drivers for every device model. Instead of re-imaging the device, your existing Windows 10 installation can be transformed into a “business-ready” state that can:
- apply settings and policies
- install apps
- change the edition of Windows 10 being used (for example, from Windows 10 Pro to Windows 10 Enterprise) to support advanced features.

Once deployed, you can manage Windows 10 devices with:
- Microsoft Intune
- Windows Update for Business
- Microsoft Endpoint Configuration Manager
- or other similar tools.

With Windows Autopilot, you can quickly prepare a device for a new user with Windows Autopilot Reset. You can also use Reset in break/fix scenarios to quickly bring a device back to a business-ready state.

Windows Autopilot enables you to:
* Automatically join devices to Azure Active Directory (Azure AD) or Active Directory (via Hybrid Azure AD Join). For more information about the differences between these two join options, see [Introduction to device management in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction).
* Auto-enroll devices into MDM services, such as Microsoft Intune ([*Requires an Azure AD Premium subscription for configuration*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Restrict the Administrator account creation.
* Create and auto-assign devices to configuration groups based on a device's profile.
* Customize OOBE content specific to the organization.

## Benefits of Windows Autopilot

Traditionally, IT pros spend significant time building and customizing images that will later be deployed to devices. Windows Autopilot introduces a new approach.

From the user's perspective, it only takes a few simple operations to make their device ready to use.

From the IT pro's perspective, the only interaction required from the end user is to connect to a network and to verify their credentials. Everything beyond that is automated.

## Requirements

A [supported version](https://docs.microsoft.com/windows/release-information/) of Windows 10 semi-annual channel is required to use Windows Autopilot. Windows 10 Enterprise LTSC 2019 is also supported. For more information, see [Windows Autopilot software](software-requirements.md), [networking](networking-requirements.md), [configuration](configuration-requirements.md), and [licensing](licensing-requirements.md) requirements.

## Related topics

[Enroll Windows devices in Intune by using Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Windows Autopilot scenarios and capabilities](windows-autopilot-scenarios.md)
