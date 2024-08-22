---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 10 of 10 - Register device for Windows Autopilot
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 10 of 10 - Register device for Windows Autopilot.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Register device for Windows Autopilot

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)

> [!div class="checklist"]
>
> - **Step 10: Register device for Windows Autopilot**

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Register device for Windows Autopilot

Running the Autopilot for existing devices task sequence and the Autopilot deployment on a device doesn't automatically register the device for Windows Autopilot. The Autopilot profile JSON makes the Autopilot deployment available to the device and allows the device to run that particular Autopilot deployment, but it doesn't register the device for Windows Autopilot. If the device ever undergoes a reset, when it runs Windows Setup and the out-of-box experience (OOBE) for the first time after the reset, it won't run the Autopilot deployment again even though it has previously run an Autopilot deployment.

To ensure that the device can run a Windows Autopilot deployment after a reset, the device must be registered for Windows Autopilot. The device can be registered as a Windows Autopilot device by using one of the following methods:

1. [Manually register devices with Windows Autopilot](../../add-devices.md): Manually registering a device includes manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

   - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
   - [PowerShell script](../../add-devices.md#powershell)
   - [Diagnostics page hash export](../../add-devices.md#diagnostics-page-hash-export)
   - [Desktop hash export](../../add-devices.md#desktop-hash-export)

1. In an Autopilot profile that is deployed to a device group that the device is a member of, make sure the option **Convert all targeted devices to Autopilot** is set to **Yes**. For more information on creating and assigning Autopilot profiles, see one of the following articles on creating and assigning an Autopilot profile for each of the different Autopilot scenarios:

   - [User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Autopilot profile](../user-driven/azure-ad-join-autopilot-profile.md)
   - [User-driven Microsoft Entra hybrid join: Create and assign user-driven Microsoft Entra hybrid join Autopilot profile](../user-driven/hybrid-azure-ad-join-autopilot-profile.md)
   - [Pre-provisioning Microsoft Entra join: Create and assign a pre-provisioned Microsoft Entra join Autopilot profile](../pre-provisioning/azure-ad-join-autopilot-profile.md)
   - [Pre-provisioning Microsoft Entra hybrid join: Create and assign a pre-provisioned Microsoft Entra hybrid join Autopilot profile](../pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md)
   - [Self-deploying mode: Create and assign self-deploying Autopilot profile](../self-deploying/self-deploying-autopilot-profile.md)

## Importing the hardware hash CSV file for devices into Intune

[!INCLUDE [Importing the hardware hash CSV file for devices into Intune](../includes/import-hardware-hash.md)]

## Ensure domain join profile is assigned to all devices

For Autopilot scenarios that utilize Microsoft Entra hybrid join and run after the Windows Autopilot deployment for existing devices task sequence completes, make sure that the domain join profile is assigned to **All devices**. This modification can be done at the followings steps:

- For the [Windows Autopilot user-driven Microsoft Entra hybrid join](../user-driven/hybrid-azure-ad-join-workflow.md) scenario at [Step 8: Configure and assign domain join profile](../user-driven/hybrid-azure-ad-join-domain-join-profile.md).
- For the [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join](../pre-provisioning/hybrid-azure-ad-join-workflow.md) scenario at [Step 8: Configure and assign domain join profile](../pre-provisioning/hybrid-azure-ad-join-domain-join-profile.md).

 The domain join profile needs to be assigned to **All devices** because:

- If the existing device has never joined Microsoft Entra ID before the Windows Autopilot deployment runs, then there isn't a Microsoft Entra ID device object for the device in Intune. The Microsoft Entra ID device object is created in Intune when the device joins Microsoft Entra ID as part of the Windows Autopilot deployment.

- If the existing device has never registered as a Windows Autopilot device before the Windows Autopilot deployment runs, then there isn't a Windows Autopilot device object for the device in Intune. Normally a device has to be a Windows Autopilot device before the Windows Autopilot deployment can run on it. However, for the Windows Autopilot deployment for existing devices scenario, registering the device as an Autopilot device isn't required since it instead uses the Autopilot profile JSON file. The device is instead registered as an Autopilot device after the Autopilot deployment completes via the methods in the [Register device for Windows Autopilot](#register-device-for-windows-autopilot) section.

In both of the above scenarios, there's no device that can be added to a device group before the Autopilot deployment begins. Since there's no device group that contains the device, there's no device group that the domain join profile can be assigned to before the Autopilot deployment begins. Assigning the domain join profile to **All devices** resolves this problem and ensures that the device can pick up the domain join profile before it's either a Microsoft Entra device or Autopilot device.

## Related content

For more information on registering the device for Windows Autopilot, see the following articles:

- [Register the device for Windows Autopilot](../../existing-devices.md#register-the-device-for-windows-autopilot).
- [Manually register devices with Windows Autopilot](../../add-devices.md).
- [Create an Autopilot deployment profile](../../profiles.md#create-an-autopilot-deployment-profile).
