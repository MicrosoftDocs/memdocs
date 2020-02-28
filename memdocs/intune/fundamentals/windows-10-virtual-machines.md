---
# required metadata

title: Using Windows 10 virtual machines with Microsoft Intune
titleSuffix: 
description: Guidelines for using Windows 10 virtual machines with Microsoft Intune
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Using Windows 10 virtual machines with Intune

Intune supports managing virtual machines running Windows 10 Enterprise with certain limitations. Intune management does not depend on, or interfere with Windows Virtual Desktop management of the same virtual machine.

When managing Windows 10 VMs with Intune, keep the following points in mind:

## Enrollment
- We don't recommend managing on-demand, session-host virtual machines with Intune. Each VM must be enrolled when it's created. Also, regularly deleting VMs will leave orphaned device records in Intune until they're [cleaned up](../intune/remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules). 
- Windows Autopilot Self-deploying and White glove deployment types aren't supported because they require a physical Trusted Platform Module (TPM). 
- Out of Box Experience (OOBE) enrollment isn't supported on VMs that can only be accessed by using RDP (such as VMs that are hosted on Azure). This restriction means:
    - Windows Autopilot and Commercial OOBE aren't supported.
    - Enrollment Status Page options for device-context policies aren't supported.

## Configuration
Intune does not support any configuration that utilizes a Trusted Platform Module or hardware management, including:
- [BitLocker settings](../intune/configuration/device-profiles.md#endpoint-protection)
- [Device Firmware Configuration Interface settings](../intune/configuration/device-profiles.md#device-firmware-configuration-interface)

## Reporting
Intune automatically detects virtual machines and reports them as "Virtual Machine" in **Devices** > **All devices** > choose a device > **Overview** > **Model** field. 

Deallocated virtual machines may contribute to noncompliant device reports because they're unable to [check in with the Intune service](../intune/configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## Retirement
If you only have RDP access, don’t use the [Wipe action](../intune/remote-actions/devices-wipe.md#wipe). The Wipe action will delete the virtual machine's RDP settings and prevent you from ever connecting again.


