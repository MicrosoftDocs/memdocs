---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the azure-ad-join-assign-device-to-user.md articles. Headings are driven by article context. -->

A device that has been registered as an Autopilot device can also be assigned to a user. If an Autopilot device is assigned to a user, then any user policies and application installs assigned to that user will also be applied to the device during the Autopilot process.

> [!TIP]
>
> For Configuration Manager admins, assigning a user to a device is similar to user device affinity in Configuration Manager.

To assign an Autopilot device to a user, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices**.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, select **Windows enrollment**.

1. Under **Windows Autopilot Deployment Program**, select **Devices**.

1. In the **Windows Autopilot devices** screen, locate the device to assign a user to.

1. Once the desired device has been located, select the box to the left of the device, making sure that there's check mark in the box, and then select **Assign user** in the toolbar above.

1. In the **Select user** page, find and select a user for the device, and then select **Select**. If necessary, use the **Search** box to find the desired user.

    > [!NOTE]
    >
    > The selected user must be an Azure user licensed to use Intune.

1. In the Autopilot device's property page that automatically opens on the right hand side, under **User friendly name**, verify the default value. If the value is empty or a different friendly name is desired, enter the desired friendly name for the user under **User friendly name**, and then select **Save**.

1. The user assignment can be verified by selecting the Autopilot device in the **Windows Autopilot devices** screen. Once the Autopilot device is selected, it will highlight and the Autopilot device's property page will automatically open on the right hand side. The assigned user will be listed under **User** and **User friendly name**.