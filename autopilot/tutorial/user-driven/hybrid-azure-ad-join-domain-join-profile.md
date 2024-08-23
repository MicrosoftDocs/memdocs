---
title: Windows Autopilot user-driven Microsoft Entra hybrid join - Step 8 of 10 - Create and assign a domain join profile
description: How to - Windows Autopilot user-driven Microsoft Entra hybrid join - Step 8 of 10 - Create and assign a domain join profile.
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

# User-driven Microsoft Entra hybrid join: Create and assign a domain join profile

Autopilot user-driven Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)

> [!div class="checklist"]
>
> - **Step 8: Configure and assign domain join profile**

- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Deploy the device](hybrid-azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra hybrid join workflow, see [Windows Autopilot user-driven Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If a domain join profile is already created with the desired settings and assignments, move on to the [Next step: Assign Autopilot device to a user (optional)](#next-step-assign-autopilot-device-to-a-user-optional) section.

## Create and assign a domain join profile

[!INCLUDE [Create and assign a domain join profile](../includes/domain-join-profile.md)]

## Next step: Assign Autopilot device to a user (optional)

> [!div class="nextstepaction"]
> [Step 9: Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)

If a user isn't being assigned to the device, then skip to **[Step 10: Deploy the device](hybrid-azure-ad-join-deploy-device.md)**.

> [!div class="nextstepaction"]
> [Step 10: Deploy the device](hybrid-azure-ad-join-deploy-device.md)

## Related content

For more information on domain join profiles, see the following article:

- [Create and assign a Domain Join profile](../../windows-autopilot-hybrid.md#create-and-assign-a-domain-join-profile).
