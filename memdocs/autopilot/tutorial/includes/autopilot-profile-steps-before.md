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

azure-ad-join-autopilot-profile.md
hybrid-azure-ad-join-autopilot-profile.md
self-deploying-autopilot-profile.md

Headings are driven by article context. -->

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left hand pane.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot Deployment Program**, select **Deployment Profiles**.

6. In the **Windows Autopilot deployment profiles** screen, select **Create Profile** > **Windows PC**.

7. The **Create profile** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the Autopilot profile.

   1. Next to **Description**, enter a description.

   1. Select **Next**.

    > [!NOTE]
    >
    > Set the option **Convert all targeted devices to Autopilot** to **Yes**. While this tutorial concentrates on new devices where the device is manually imported as an Autopilot device using the hardware hash, this option can be helpful when assigning Autopilot profiles to device groups that contain existing devices. For example, this option is very helpful when using the [Windows Autopilot for existing devices](../existing-devices/existing-devices-workflow.md) scenario where existing devices may need to be registered as an Autopilot device after the Autopilot deployment is finished.
