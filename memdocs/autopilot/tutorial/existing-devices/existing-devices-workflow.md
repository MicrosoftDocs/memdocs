---
title: Overview for Windows Autopilot deployment for existing devices in Intune and Configuration Manager
description: Overview for Windows Autopilot deployment for existing devices in Intune and Configuration Manager.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot deployment for existing devices in Intune and Configuration Manager

This step by step tutorial guides you through using Intune and Microsoft Configuration Manager to perform a Windows Autopilot deployment for existing devices.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Autopilot deployment for existing devices using Intune and Microsoft Configuration Manager. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment. This tutorial assumes familiarity with Microsoft Configuration Manager and that Microsoft Configuration Manager is already set up and configured to support operating system deployments.

## Windows Autopilot deployment for existing devices overview

The main use case scenario for Windows Autopilot is to automate the configuration of Windows on a new device delivered directly from an IT department, OEM, or reseller. However, sometimes existing devices in an environment need to be repurposed, fixed, or updated to a newer version of Windows by reinstalling Windows on the device. Reinstalling of Windows is usually performed via a reimage of the device, which is outside the capabilities of Windows Autopilot. Windows Autopilot also isn't able to perform a fresh install of Windows if the version of Windows is different than the one that is currently installed on the device. There may also be other conditions that prevent Windows Autopilot from performing a fresh install of Windows on the device. For example, corruption of the current Windows install or a hard drive failure.

For scenarios where Windows needs to be reinstalled or updated to a newer version of Windows using a fresh installation of Windows, Windows Autopilot can utilize Microsoft Configuration Manager task sequences. Microsoft Configuration Manager task sequences can reimage a device and perform a fresh installation of Windows. The Configuration Manager task sequence can also pre-install a Windows Autopilot profile on the device via a JSON file. Once the Configuration Manager task sequence is done, the device can then automatically run the Windows Autopilot deployment defined in the Windows Autopilot profile JSON file. When the Windows Autopilot profile JSON file is pre-installed on the device, the Windows Autopilot deployment can run on the device without having to first perform the following actions:

- Import the device into Intune as an Autopilot device.
- Assign an Autopilot profile to the device.

Windows Autopilot deployment for existing devices is useful for the following scenarios:

- Repurpose an existing device that isn't yet an Autopilot device.
- Migrate an on-premises domain joined device that isn't part of Azure AD to an Azure AD join device.
- Convert an on-premises domain joined device that is hybrid Azure AD joined to an Azure AD join device.
- Reinstall Windows on devices that need to be repaired. For example, a device that has a corrupted Windows installation or where the hard drive was replaced.
- Upgrade older versions of Windows that don't support Azure AD (Windows 8.1) to a version of Windows that does support Azure AD (Windows 10/Windows 11).
- Using custom Windows images instead of the OEM provided Windows installation.

Windows Autopilot deployment for existing devices can be viewed as a method to prepare an existing device for an Autopilot deployment.

> [!NOTE]
>
> The JSON file for Windows Autopilot for existing devices only supports user-driven Azure AD and user-driven hybrid Azure AD Autopilot profiles. Self-deploying and pre-provisioning Autopilot profiles aren't supported with JSON files due to these scenarios requiring TPM attestation. TPM attestation only works where there's an existing Autopilot device since the TPM attestation information is stored in the Autopilot device object.
>
> However, during the Windows Autopilot for existing devices deployment, if the following conditions are true:
>
> - Device is already a Windows Autopilot device before the deployment begins
> - Device has an Autopilot profile assigned to it
>
> then the assigned Autopilot profile takes precedence over the JSON file installed by the task sequence. In this scenario, if the assigned Autopilot profile is either a self-deploying or pre-provisioning Autopilot profile, then the self-deploying and pre-provisioning scenarios are supported.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot deployment for existing devices deployment using Intune and Microsoft Configuration Manager:

> [!div class="checklist"]
> - Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
> - Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
> - Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
> - Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
> - Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
> - Step 6: [Create collection in Configuration Manager](create-collection.md)
> - Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
> - Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
> - Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
> - Step 10: [Register device for Windows Autopilot](register-device.md)

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up a Windows Autopilot profile](setup-autopilot-profile.md)

## More information

For more information on Windows Autopilot deployment for existing devices, see the following article(s):

- [Windows Autopilot deployment for existing devices](/mem/autopilot/existing-devices)
