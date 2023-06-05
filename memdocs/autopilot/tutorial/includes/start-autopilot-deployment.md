---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 06/05/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

self-deploying/self-deploying-deploy-device.md
user-driven/azure-ad-join-deploy-device.md
user-driven/hybrid-azure-ad-join-deploy-device.md

Headings are driven by article context. -->

To start the Autopilot deployment process on the device, follow these steps:

1. Select a device that is part of the device group created in the previous **Create a device group** step.

2. If a wired network connection is available, connect the device to the wired network connection.

3. Power on the device.

4. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the device may reboot one time to apply critical security updates followed by the Azure AD sign-in page appearing.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity, it prompts to connect to a network. Connectivity to the Internet is required:

     1. OOBE (out of box experience) begins and a screen asking for a country or region appears. Select the appropriate country or region, and then select **Yes**.

     2. The keyboard screen appears to select a keyboard layout. Select the appropriate keyboard layout, and then select **Yes**.

     3. An additional keyboard layouts screen appears. If needed, select additional keyboard layouts via **Add layout**, or select **Skip** if no additional keyboard layouts are needed.

         > [!NOTE]
         >
         > When there's no network connectivity, the country/region and keyboard screens appear even if these screens have been set to hidden in the Autopilot profile. Because there was no network connectivity at this point, the device hasn't downloaded the Autopilot profile to know that these screens should have been hidden.

     4. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     5. Once network connectivity is established, the **Next** button should become available. Select **Next**.

     6. At this point, the device may reboot to apply critical security updates. After it reboots, the Azure AD sign-in page should appear.

    > [!NOTE]
    >
    > Additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Azure AD sign-in page depending on how the Autopilot profile was configured at the **Create and assign Autopilot profile** step.
