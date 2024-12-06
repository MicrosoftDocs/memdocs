---
# required metadata
title: Suppress single sign-on consent prompts for Windows 365 Link
titleSuffix:
description: Learn about suppressing single sign-on consent prompts for Windows 365 Link
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365-link
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Suppress single sign-on consent prompts for Windows 365 Link

As part of [setting up your organization's environment to support Windows 365 Link devices](deployment-overview.md), you should consider suppressing single sign-on consent prompts for your Windows 365 Link devices. The Windows 365 Link connection experience doesn’t currently support interacting with the SSO consent prompt.

When connecting to a Cloud PC for the first time after single sign-on (SSO) is enabled, users are prompted for consent to allow the connection. They're also prompted every 30 days or after a Cloud PC is reprovisioned. If a connection to a Cloud PC requires SSO consent, the Windows 365 Link connection will fail. This failure necessitates that the user first connect to the Cloud PC from another device or web browser and grant SSO consent before attempting to connect from a Windows 365 Link device again.  

To avoid this this experience, you must suppress the SSO consent prompt by configuring a property on the SSO service principals in Entra ID.

To suppress the SSO consent prompt, follow these steps:

1. [Create a dynamic device group for all Cloud PCs](../enterprise/create-dynamic-device-group-all-cloudpcs.md#create-a-dynamic-device-group-for-all-cloud-pcs).
2. [Enable Entra authentication for RDP on the SSO service principal](/azure/virtual-desktop/configure-single-sign-on#enable-microsoft-entra-authentication-for-rdp).
3. [Add the group of Cloud PCs to the Service Principal target](/azure/virtual-desktop/configure-single-sign-on#hide-the-consent-prompt-dialog).

After the Cloud PCs are in the target group, the users aren't prompted to consent to use SSO.

## Next steps

[Onboard Windows 365 Link devices](onboarding.md).
