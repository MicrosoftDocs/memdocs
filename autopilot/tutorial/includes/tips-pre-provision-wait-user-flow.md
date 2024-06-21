---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-user-flow.md
pre-provisioning/hybrid-azure-ad-join-user-flow.md

Headings are driven by article context. -->

- For tokens to refresh properly between the Technician flow and the User flow, wait at least 90 minutes after running the Technician flow before running the User flow. This scenario mainly affects lab and testing scenarios, such as this tutorial, when the User flow is run within 90 minutes after the Technician flow completes.
