---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-autopilot-profile.md
pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md
self-deploying/self-deploying-autopilot-profile.md
user-driven/azure-ad-join-autopilot-profile.md
user-driven/hybrid-azure-ad-join-autopilot-profile.md

Headings are driven by article context. -->

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment Profiles**.

1. In the **Windows Autopilot deployment profiles** screen, select the **Create Profile** drop down menu and then select **Windows PC**.

1. The **Create profile** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the Autopilot profile.

   1. Next to **Description**, enter a description.

   1. Select **Next**.

      > [!NOTE]
      >
      > Microsoft recommends setting the option **Convert all targeted devices to Autopilot** to **Yes**. This tutorial concentrates on new devices where the device is manually imported as an Autopilot device using the hardware hash. However, this option can be helpful when assigning Autopilot profiles to device groups that contain existing devices. For example, this option is helpful when using the [Windows Autopilot for existing devices](../existing-devices/existing-devices-workflow.md) scenario. With Windows Autopilot for existing devices, existing devices might need to be registered as an Autopilot device after the Autopilot deployment completes. For more information, see [Register device for Windows Autopilot](../existing-devices/register-device.md).
