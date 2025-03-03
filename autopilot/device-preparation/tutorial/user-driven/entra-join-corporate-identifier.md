---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 7 of 7 - Add Windows corporate identifier to device
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 7 of 7 - Add Windows corporate identifier to device.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 01/14/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Add Windows corporate identifier to device

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)

> [!div class="checklist"]
>
> - **Step 7: Add Windows corporate identifier to device**

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

## Add Windows corporate identifier for devices

Corporate identifiers in Intune allows pre-uploading of Windows device identifiers (serial number, manufacturer, model) and ensures only trusted Windows devices can be enrolled in Intune. If Intune enrollment restrictions are being used to block personal device enrollments, corporate identifiers need to be uploaded for all devices that are enrolled through Windows Autopilot device preparation before deployment. To add corporate identifier for devices in Intune, see [Add Windows corporate identifiers](/mem/intune-service/enrollment/corporate-identifiers-add#add-windows-corporate-identifiers).

> [!IMPORTANT]
>
> This step of adding Windows corporate identifiers for devices is specific to Intune enrollments and isn't required if personal devices aren't being blocked in the environment. If personal devices aren't being blocked in the environment, this step can be skipped. The next step would instead be to deploy the device. 

For more information, see:

- [Identify devices as corporate-owned](/mem/intune-service/enrollment/corporate-identifiers-add).
- [What are enrollment restrictions?](/mem/intune-service/enrollment/enrollment-restrictions-set).
- [Create device platform restrictions](/mem/intune-service/enrollment/create-device-platform-restrictions).

Once the corporate identifier is added for the device, then proceed with deploying the device.
