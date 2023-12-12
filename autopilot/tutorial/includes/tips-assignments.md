---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 06/26/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning\azure-ad-join-technician-flow.md
pre-provisioning\hybrid-azure-ad-join-technician-flow.md
user-driven\azure-ad-join-deploy-device.md
user-driven\hybrid-azure-ad-join-deploy-device.md

Headings are driven by article context. -->

- Before starting the Autopilot deployment, you may want to have:<br>
<br>
  - At least one type of policy and at least one application assigned to the device(s).
  - At least one type of policy and at least one application assigned to the user(s).

  These assignments ensure proper testing of the Autopilot deployment during both the device ESP phase and user ESP phase of the ESP. It may also prevent possible issues when there are either no policies or no applications assigned to the device(s) or the user(s).
