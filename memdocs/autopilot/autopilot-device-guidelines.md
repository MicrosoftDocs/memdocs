---
title: Windows Autopilot device guidelines
description: Learn all about hardware, firmware, and software best practices for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 2/1/2022
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---

# Windows Autopilot device guidelines

**Applies to**

- Windows 11
- Windows 10

## Hardware and firmware best practice guidelines for Windows Autopilot

All devices using Windows Autopilot should meet the [minimum hardware requirements](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) for Windows.

The following best practices ensure that devices can easily be provisioned as part of the Windows Autopilot deployment process: 
- TPM 2.0 is enabled and in a good state (not in **Reduced Functionality Mode**) on devices intended for Windows Autopilot self-deploying mode.
- The OEM should provision either of the following information into the [SMBIOS fields](/windows-hardware/drivers/bringup/smbios). The information should follow Microsoft specifications (Manufacturer, Product Name, and Serial Number stored in SMBIOS Type 1 04h, Type 1 05h and Type 1 07h).
    - Unique tuple info (SmbiosSystemManufacturer, SmbiosSystemProductName, SmbiosSystemSerialNumber)
    - PKID + SmbiosSystemSerialNumber
- Before shipping devices to an Autopilot customer or channel partner, the OEM should upload 4K Hardware Hashes to Microsoft by using the CBR report. The hashes should be collected using the OA3 Tool RS3+ run in Audit mode on full OS.
- Microsoft requires that OEM shipping drivers get published to Windows Update within 30 days of the CBR submission date. System firmware and driver updates are published to Windows Update within 14 days.
- The OEM ensures that the PKID provisioned in the SMBIOS is passed on to the channel.
- When using a VM for Autopilot testing, assign at least 2 processors and 4gb of memory. *Note: The [minimum system requirements](/windows/whats-new/windows-11-requirements#virtual-machine-support) for Windows 11 are 2 processors and 4gb memory.

## Software best practice guidelines for Windows Autopilot

- The Windows Autopilot device should be preinstalled with only a Windows base image plus drivers.
- You can preinstall your licensed version of Office, such as [Microsoft 365 Apps for enterprise](/deployoffice/about-office-365-proplus-in-the-enterprise).
- Unless explicitly requested by the customer, no other preinstalled software should be included.
  - Per OEM Policy, Windows features, including built-in apps, shouldn't be disabled or removed.

## Next steps

[Windows Autopilot customer consent](registration-auth.md)<br>
[Motherboard replacement scenario guidance](autopilot-mbr.md)<br>
