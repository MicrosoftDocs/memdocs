---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 07/23/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-user-flow.md
pre-provisioning/hybrid-azure-ad-join-user-flow.md

Headings are driven by article context. -->

- For tokens to refresh properly between the Technician flow and the User flow, wait at least 90 minutes after running the Technician flow before running the User flow. This scenario mainly affects lab and testing scenarios, such as this tutorial, when the User flow is run within 90 minutes after the Technician flow completes.

- The User flow should be run within six months after the Technician flow finishes. Waiting more than six months can cause the certificates used by the Intune Management Engine (IME) to no longer be valid leading to errors such as:

    `Error code: [Win32App][DetectionActionHandler] Detection for policy with id: <policy_id> resulted in action status: Failed and detection state: NotComputed.`