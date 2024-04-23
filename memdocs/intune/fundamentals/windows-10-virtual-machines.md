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

# Using Windows 10 virtual machines with Intune

Intune supports managing virtual machines running Windows 10 Enterprise with certain limitations. Intune management doesn't depend on, or interfere with Azure Virtual Desktop management of the same virtual machine.

## Enrollment

- We recommend that you don't use Intune to manage on-demand, session-host virtual machines, also known as non-persistent virtual desktop infrastructure (VDI). Each VM must be enrolled when it's created. Also, regularly deleting VMs creates orphaned device records in Intune until they're [cleaned up](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules).

- Windows Autopilot Self-deploying and pre-provisioning deployment types aren't supported because they require a physical Trusted Platform Module (TPM).

- Out of Box Experience (OOBE) enrollment isn't supported on VMs that can only be accessed by using RDP (such as VMs that are hosted on Azure).
This restriction means:
  - Windows Autopilot and Commercial OOBE aren't supported.
  - Enrollment Status Page isn't supported.

- For cloned scenarios, once Intune detects an existing MDM certificate all devices or clients using the same MDM certificate will no longer be able to check into Intune. Intune can only support one VM instance at a time, and for a cloning scenario only one instance of a device can be up and managed at a time. For more information about the cloning scenario, see [Create an Azure Virtual Desktop golden image](azure/virtual-desktop/set-up-golden-image).  

## Configuration

Intune doesn't support any configuration that utilizes a Trusted Platform Module or hardware management, including:

- [BitLocker settings](../configuration/device-profiles.md#endpoint-protection)
- [Device Firmware Configuration Interface settings](../configuration/device-profiles.md#bios-configuration-and-dfci)

## Reporting

Intune automatically detects virtual machines and reports them as "Virtual Machine" in **Devices** > **All devices** > choose a device > **Overview** > **Model** field.

Deallocated virtual machines may contribute to noncompliant device reports because they're unable to [check in with the Intune service](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

## Retirement

If you only have RDP access, don't use the [Wipe action](../remote-actions/devices-wipe.md#wipe). The Wipe action deletes the virtual machine's RDP settings and prevents you from ever connecting again.

## Next steps

[Learn about using Azure Virtual Desktop with Intune](azure-virtual-desktop.md)
