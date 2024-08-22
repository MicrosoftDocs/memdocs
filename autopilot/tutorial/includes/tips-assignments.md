---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning\azure-ad-join-technician-flow.md
pre-provisioning\hybrid-azure-ad-join-technician-flow.md
user-driven\azure-ad-join-deploy-device.md
user-driven\hybrid-azure-ad-join-deploy-device.md

Headings are driven by article context. -->

- Before the Windows Autopilot deployment is started, Microsoft recommends having:<br>
<br>
  - At least one type of policy and at least one application assigned to the devices.
  - At least one type of policy and at least one application assigned to the users.

  These assignments ensure proper testing of the Windows Autopilot deployment during both the device ESP phase and user ESP phase of the ESP. It might also prevent possible issues when there are either no policies or no applications assigned to the devices or the users.