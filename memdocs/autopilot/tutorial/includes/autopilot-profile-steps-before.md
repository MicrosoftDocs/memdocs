---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 03/27/2023
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
    > For the purposes of this tutorial, leave the option **Convert all targeted devices to Autopilot** set to **No**. This tutorial concentrates on new devices while this option mainly covers existing devices.
