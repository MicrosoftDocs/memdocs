---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 2 of 11 - Install the Intune Connector
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 2 of 11 - Install the Intune Connector(ESP).
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
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2022</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2019</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2016</a>
---

# Pre-provision Microsoft Entra hybrid join: Install the Intune Connector

Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)

> [!div class="checklist"]
>
> - **Step 2: Install the Intune Connector**

- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If the Intune Connector is already installed and configured, skip this step and move on to [Step 3: Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md).

## Install the Intune Connector

[!INCLUDE [Install the Intune Connector](../includes/intune-connector.md)]

## Next step: Increase the computer account limit in the Organizational Unit (OU)

> [!div class="nextstepaction"]
> [Step 3: Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)

## Related content

For more information on the Intune connector, see the following article:

- [Install the Intune Connector](../../windows-autopilot-hybrid.md#install-the-intune-connector).
