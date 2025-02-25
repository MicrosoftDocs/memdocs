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

pre-provisioning/azure-ad-join-user-flow.md
pre-provisioning/hybrid-azure-ad-join-user-flow.md

Headings are driven by article context. -->

- Compliance in Microsoft Entra ID is reset during the User flow. Devices might show as compliant in Microsoft Entra ID after the Technician flow completes, but then show as noncompliant once the User flow starts. Allow enough time after the User flow completes for compliance to reevaluate and update.
