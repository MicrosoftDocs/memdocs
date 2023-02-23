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

A device that has been registered as an Autopilot device can be also be assigned to a user. If an Autopilot device is assigned to a user, then any user policies and application installs assigned to that user will be applied to the device during the Autopilot process.

To assign an Autopilot device to a user, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot Deployment Program**, select **Devices**.

6. In the **Windows Autopilot devices** screen, locate the device to assign a user to.

7. Once the desired device has been located, select the box to the left of the device, making sure that there is check mark in the box, and then select **Assign user** in the toolbar above.

8. In the **Select user** page, find and select a user for the device, and then select **Select**. If necessary, use the **Search** box to find the desired user.

    > [!NOTE]
    >
    > The selected user must be an Azure user licensed to use Intune.

9. In the Autopilot device's property page that automatically opens on the right hand side, under **User friendly name**, verify the default value. If the value is empty or a different friendly name is desired, enter the desired friendly name for the user under **User friendly name** and then select **Save**.

10. The user assignment can be verified by selecting the Autopilot device in the **Windows Autopilot devices** screen. Once the Autopilot device is selected, it will highlight and the Autopilot device's property page will automatically open on the right hand side. The assigned user will be listed under **User** and **User friendly name**.

> [!TIP]
>
> For Configuration Manager admins, assigning a user to a device is similar to user device affinity in Configuration Manager.

For more information on assigning a user to an Autopilot device, see the following articles:

- [Assign a user to a specific Autopilot device](/mem/autopilot/enrollment-autopilot#assign-a-user-to-a-specific-autopilot-device)
