---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 9 of 11 - Technician flow
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 9 of 11 - Technician flow.
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

# Pre-provision Microsoft Entra hybrid join: Technician flow

Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)

> [!div class="checklist"]
>
> - **Step 10: Technician flow**

- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

## Technician flow

> [!IMPORTANT]
>
> The technician flow portion of the Microsoft Entra hybrid join process only requires connectivity to the Internet. It doesn't require connectivity to a domain controller. Connectivity to a domain controller to perform an on-premises domain join isn't needed until the next step of [User flow](hybrid-azure-ad-join-user-flow.md) runs.

[!INCLUDE [Technician flow](../includes/technician-flow.md)]

## Technician flow tips

[!INCLUDE [Tips assignments](../includes/tips-assignments.md)]

[!INCLUDE [Tips technician flow screens](../includes/tips-technician-flow-screens.md)]

[!INCLUDE [Tips QR codes](../includes/tips-qr-codes.md)]

[!INCLUDE [Tips ESP progress](../includes/tips-esp-progress.md)]

[!INCLUDE [Tips technician flow inherit](../includes/tips-technician-flow-inherit.md)]

## Next step: User flow

> [!div class="nextstepaction"]
> [Step 11: User flow](hybrid-azure-ad-join-user-flow.md)

## Related content

[!INCLUDE [More information technician flow](../includes/more-info-technician-flow.md)]
