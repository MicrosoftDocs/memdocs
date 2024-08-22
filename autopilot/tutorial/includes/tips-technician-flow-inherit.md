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

Headings are driven by article context. -->

- The technician flow inherits behavior from [self-deploying mode](../self-deploying/self-deploying-workflow.md). Self-deploying mode uses the Enrollment Status Page (ESP) to hold the device in a provisioning state. It also prevents the user from proceeding to the desktop after enrollment but before applications and configurations are done applying. If the ESP is disabled, the **Reseal** button might appear before applications and configurations are done applying. Disabling the ESP might advertently allow proceeding to the user flow before technician flow provisioning is complete. The success status screen validates that enrollment was successful, not that the technician flow is necessarily complete. For this reason, Microsoft recommends not to disable the ESP. Instead enable the ESP as suggested in the **Configure and assign Autopilot Enrollment Status Page (ESP)** step.
