---
# required metadata

title: Using Windows 10 virtual machines with Microsoft Intune
titleSuffix: Microsoft Intune
description: This article describes the general guidelines for using Windows 10 virtual machines with Microsoft Intune
keywords:
author: Smritib17  
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/23/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata
# CustomerIntent: As an  IT admin, I want to understand the guidelines for virtual machines running on Windows 10 enterprise so that I can manage the virtual machines running on Windows 10 Enterprise.

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Using Windows 10/11 virtual machines with Intune

Intune supports managing virtual machines running Windows 10 Enterprise with certain limitations. Intune management doesn't depend on, or interfere with Azure Virtual Desktop management of the same virtual machine.

## Enrollment

- We recommend that you don't use Intune to manage on-demand, session-host virtual machines, also known as non-persistent virtual desktop infrastructure (VDI). Each VM must be enrolled when it's created. Also, regularly deleting VMs creates orphaned device records in Intune until they're [cleaned up](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules).

- Windows Autopilot Self-deploying and pre-provisioning deployment types aren't supported because they require a physical Trusted Platform Module (TPM).

- Out of Box Experience (OOBE) enrollment isn't supported on non-persistent VMs that can only be accessed by using RDP (such as VMs that are hosted on Azure).
This restriction means:
- Windows Autopilot and Commercial OOBE aren't supported.
  - Enrollment Status Page isn't supported.

## Configuration

Intune doesn't support any configuration that utilizes a Trusted Platform Module or hardware management, including:

- [BitLocker settings](../configuration/device-profiles.md#endpoint-protection)
- [Device Firmware Configuration Interface settings](../configuration/device-profiles.md#bios-configuration-and-dfci)

## Reporting

Intune automatically detects virtual machines and reports them as "Virtual Machine" in **Devices** > **All devices** > choose a device > **Overview** > **Model** field.

Deallocated virtual machines may contribute to noncompliant device reports because they're unable to [check in with the Intune service](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

## Retirement

If you only have RDP access, don't use the [Wipe action](../remote-actions/devices-wipe.md#wipe). The Wipe action deletes the virtual machine's RDP settings and prevents you from ever connecting again.

## Limitations

Intune does not support using a cloned image of a computer that is already enrolled. This includes both physical and virtual devices such as Azure Virtual Desktop (AVD). When device enrollment or identity tokens are replicated between devices, Intune device enrollment or synchronization failures will occur.

- For more information, see [Mobile device enrollment - Windows Client Management](/windows/client-management/mobile-device-enrollment) and [Certificate authentication device enrollment - Windows Client Management](/windows/client-management/certificate-authentication-device-enrollment).
- For information on disabling token roaming in AVD, see [Using Azure Virtual Desktop multi-session with Microsoft Intune](azure-virtual-desktop-multi-session.md#prerequisites).
- For information on troubleshooting issues related to image cloning, see [Error hr 0x8007064c: The machine is already enrolled](/troubleshoot/mem/intune/troubleshoot-windows-enrollment-errors#error-hr-0x8007064c-the-machine-is-already-enrolled).

## Next steps

[Learn about using Azure Virtual Desktop with Intune](azure-virtual-desktop.md)
