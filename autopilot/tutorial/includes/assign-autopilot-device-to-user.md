---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-assign-device-to-user.md
pre-provisioning/hybrid-azure-ad-join-assign-device-to-user.md
user-driven/hybrid-azure-ad-join-assign-device-to-user.md
user-driven/hybrid-azure-ad-join-assign-device-to-user.md

Headings are driven by article context. -->

A device that is registered as an Autopilot device can also be assigned to a user. If an Autopilot device is assigned to a user, then any user policies and application installs assigned to that user is applied to the device during the Autopilot process.

> [!TIP]
>
> For testing purposes, especially for hybrid Microsoft Entra scenarios, it might be better to first test an Autopilot deployment before assigning the device to a user. Not assigning a user limits the scope of applications, policies, and configurations processed during the Autopilot process.

> [!TIP]
>
> For Configuration Manager admins, assigning a user to a device is similar to user device affinity in Configuration Manager.

To assign an Autopilot device to a user, follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens, locate the device to assign a user to.

1. Once the desired device is located, select the box to the left of the device, making sure that there's check mark in the box, and then select **Assign user** in the toolbar at the top of page.

1. In the **Select user** window that opens, find and select a user for the device, and then select **Select** to close the window. If necessary, use the **Search** box to find the desired user.

    > [!NOTE]
    >
    > The selected user must be an Azure user licensed to use Intune.

1. In the Autopilot device's property window that automatically opens on the right hand side, under **User friendly name**, verify the default value. If the value is empty or a different friendly name is desired, enter the desired friendly name for the user under **User friendly name**, and then select **Save** to close the property window.

1. The user assignment can be verified by selecting the Autopilot device in the **Windows Autopilot devices** screen. Once the Autopilot device is selected, it highlights and the Autopilot device's property window automatically opens on the right hand side. The assigned user is listed under **User** and **User friendly name**.
