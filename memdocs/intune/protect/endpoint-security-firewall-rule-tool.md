---
# required metadata

title: Endpoint security firewall rule migration tool for Microsoft Intune
description: Learn about the endpoint security firewall rule migration tool for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/07/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

ROBOTS: NOINDEX
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- ContentEnagagementFY24 
- sub-secure-endpoints

ms.reviewer: 
---

# Endpoint security firewall rule migration tool overview

> [!IMPORTANT]
>
> In June 2024, a change to MSGraph affected the operation of the Intune endpoint security Firewall Rule migration tool. With this change, the tool is unable to successfully create new firewall rule profiles and is therefore no longer supported or offered for download. Compounding the issue, the tool was capable of creating profiles for only the *Windows 10 and later* platform, a platform that has deprecated and [replaced by a new platform for firewall rule profiles](../protect/endpoint-security-firewall-policy.md) that supports the current Intune settings format.
>
>The challenges affecting the tool are not issues that can be resolved in the short term.
>
> We are evaluating options to offer a new tool for firewall rule migration. However, it is not yet known if or when a new tool could be available. Should we be able to provide a new tool, we will announce its availability in the [What’s New in Microsoft Intune](../fundamentals/whats-new.md) article at that time.
