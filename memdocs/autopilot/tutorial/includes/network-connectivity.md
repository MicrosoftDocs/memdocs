---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 06/07/2023
ms.localizationpriority: medium
---

     1. OOBE (out of box experience) begins and a screen asking for a country or region appears. Select the appropriate country or region, and then select **Yes**.

     1. The keyboard screen appears to select a keyboard layout. Select the appropriate keyboard layout, and then select **Yes**.

     1. An additional keyboard layouts screen appears. If needed, select additional keyboard layouts via **Add layout**, or select **Skip** if no additional keyboard layouts are needed.

         > [!NOTE]
         >
         > When there's no network connectivity, the country/region and keyboard screens appear even if these screens have been set to hidden in the Autopilot profile. Because there was no network connectivity at this point, the device hasn't downloaded the Autopilot profile to know what settings to use. These settings need to be specified in order for the following network connectivity screens to work properly.

     1. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     1. Once network connectivity is established, the **Next** button should become available. Select **Next**.

     1. At this point, the device may reboot to apply critical security updates (if available or applicable). After the reboot to apply critical security updates, the Azure AD sign-in page appears.
