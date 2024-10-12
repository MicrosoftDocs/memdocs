---
title: Windows Autopilot self-deploying mode - Step 1 of 5 - Set up Windows automatic Intune enrollment
description: How to - Windows Autopilot self-deploying mode - Step 1 of 5 - Set up Windows automatic Intune enrollment.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
- tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Self-deploying mode: Set up Windows automatic Intune enrollment

Autopilot self-deploying mode steps:

> [!div class="checklist"]
>
> - **Step 1: Set up Windows automatic Intune enrollment**

- Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
- Step 3: [Create a device group](self-deploying-device-group.md)
- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
- Step 5: [Create and assign Autopilot profile](self-deploying-autopilot-profile.md)
- Step 6: [Deploy the device](self-deploying-deploy-device.md)

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow).

> [!NOTE]
>
> If automatic Intune enrollment is already set up, skip this step and move on to [Step 2: Register devices as Autopilot devices](self-deploying-register-device.md).

## Set up Windows automatic Intune enrollment

In order for Windows Autopilot to work, devices need to be able to enroll in Intune automatically. Enrolling devices in Intune automatically can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Set up Windows automatic enrollment](../../includes/automatic-intune-enrollment.md)]

## Next step: Allow users to join devices to Microsoft Entra ID

> [!div class="nextstepaction"]
> [Step 2: Register devices as Autopilot devices](self-deploying-register-device.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../includes/more-info-automatic-enrollment.md)]
