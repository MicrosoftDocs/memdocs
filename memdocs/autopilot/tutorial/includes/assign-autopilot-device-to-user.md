---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/11/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning\azure-ad-join-assign-device-to-user.md
pre-provisioning\hybrid-azure-ad-join-assign-device-to-user.md
user-driven\hybrid-azure-ad-join-assign-device-to-user.md
user-driven\hybrid-azure-ad-join-assign-device-to-user.md

Headings are driven by article context. -->

A device that has been registered as an Autopilot device can also be assigned to a user. If an Autopilot device is assigned to a user, then any user policies and application installs assigned to that user is applied to the device during the Autopilot process.

> [!TIP]
>
> For Configuration Manager admins, assigning a user to a device is similar to user device affinity in Configuration Manager.

To assign an Autopilot device to a user, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left pane.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot Deployment Program**, select **Devices**.

6. In the **Windows Autopilot devices** screen that opens, locate the device to assign a user to.

7. Once the desired device has been located, select the box to the left of the device, making sure that there's check mark in the box, and then select **Assign user** in the toolbar at the top of page.

8. In the **Select user** window that opens, find and select a user for the device, and then select **Select** to close the window. If necessary, use the **Search** box to find the desired user.

    > [!NOTE]
    >
    > The selected user must be an Azure user licensed to use Intune.

9. In the Autopilot device's property window that automatically opens on the right hand side, under **User friendly name**, verify the default value. If the value is empty or a different friendly name is desired, enter the desired friendly name for the user under **User friendly name**, and then select **Save** to close the property window.

10. The user assignment can be verified by selecting the Autopilot device in the **Windows Autopilot devices** screen. Once the Autopilot device is selected, it highlights and the Autopilot device's property window automatically opens on the right hand side. The assigned user is listed under **User** and **User friendly name**.