---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning\hybrid-azure-ad-join-user-flow.md
user-driven\hybrid-azure-ad-join-deploy-device.md

Headings are driven by article context. -->

- If the device is left alone with no interaction during the **Account setup** phase of the ESP, the device might enter the Windows lock screen. If the device does enter the Windows lock screen during **Account setup** of the ESP, unlock the device by entering the keystroke <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd>, entering the on-premises domain credentials for the end-user, and then selecting <kbd>ENTER</kbd> on the keyboard. Unlocking the device should go back to the Enrollment Status Page (ESP) and display the current progress of **Account setup**.
