---
title: Windows Autopilot self-deploying mode - Step 3 of 6 - Register devices as Autopilot devices
description: How to - Windows Autopilot self-deploying mode - Step 3 of 6 - Register devices as Autopilot devices.
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

# Self-deploying mode: Register devices as Autopilot devices

Autopilot self-deploying mode steps:
- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Register devices as Autopilot devices**
- Step 3: [Create a device group](self-deploying-device-group.md)
- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
- Step 5: [Create and assign Autopilot profile](self-deploying-autopilot-profile.md)

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow)

> [!NOTE]
>
> If you have already registered devices as Autopilot devices from another Autopilot scenario, you can skip this step and move on to [Step 3: Create a device group](self-deploying-device-group.md). However, if you're deploying multiple different Autopilot scenarios to different devices, separate device groups are required for each Autopilot scenario.

## Register devices as Autopilot devices

[!INCLUDE [How to register a device as an Autopilot device in Intune](../includes/register-autopilot-device.md)]

## Next step: Create a device group

> [!div class="nextstepaction"]
> [Step 3: Create a device group](self-deploying-device-group.md)

## More information

[!INCLUDE [More information register Autopilot device](../includes/more-info-register-device.md)]
