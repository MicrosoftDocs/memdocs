---
title: Windows Autopilot user-driven Microsoft Entra hybrid join - Step 3 of 10 - Increase the computer account limit in the Organizational Unit (OU)
description: How to - Windows Autopilot user-driven Microsoft Entra hybrid join - Step 3 of 10 - Increase the computer account limit in the Organizational Unit (OU).
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 01/31/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra hybrid join: Increase the computer account limit in the Organizational Unit (OU)

Windows Autopilot user-driven Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)

> [!div class="checklist"]
>
> - **Step 3: Increase the computer account limit in the Organizational Unit (OU)**

- Step 4: [Register devices as Windows Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Windows Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign Microsoft Entra hybrid join Windows Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Windows Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Deploy the device](hybrid-azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra hybrid join workflow, see [Windows Autopilot user-driven Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If the computer account limit for the proper Organizational Unit (OU) is already increased, skip this step and move on to [Step 4: Register devices as Windows Autopilot devices](hybrid-azure-ad-join-register-device.md).

## Increase the computer account limit in the Organizational Unit (OU)

[!INCLUDE [Increase the computer account limit in the Organizational Unit (OU)](../../includes/computer-account-limit.md)]

## Next step: Register devices as Windows Autopilot devices

> [!div class="nextstepaction"]
> [Step 4: Register devices as Windows Autopilot devices](hybrid-azure-ad-join-register-device.md)

## Related content

[!INCLUDE [Increase the computer account limit in the Organizational Unit (OU)](../includes/more-info-computer-account-limit.md)]
