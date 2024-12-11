---
# required metadata
title: Configure single sign-on for Windows 365
titleSuffix:
description: How to configure single sign-on for Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/26/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidbel
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Configure single sign-on for Windows 365 using Microsoft Entra authentication

This article explains the process of configuring single sign-on (SSO) for Windows 365 by using Microsoft Entra authentication. When you enable SSO, you can use passwordless authentication and third-party Identity Providers that federate with Microsoft Entra ID to sign in to your Cloud PC. When enabled, this feature provides a single sign-on experience both when authenticating to the Cloud PC and inside the session when accessing Microsoft Entra ID-based apps and websites.

For information on using passwordless authentication within the session, see [In-session passwordless authentication](identity-authentication.md#in-session-passwordless-authentication).

To get started, following the steps to [Configure single sign-on](/azure/virtual-desktop/configure-single-sign-on) for Azure Virtual Desktop with the following caveats:

- If the Kerberos Server object isn't present for Microsoft Entra hybrid joined provisioning policies, a new error appears in your Azure Network Connection (ANC) [health check for single sign-on](health-checks.md#supported-checks).
- If you have conditional access policies that apply when accessing Windows 365, review the recommendations to [set conditional access policies](set-conditional-access-policies.md) for Windows 365 to make sure users have the expected experience.
- SSO can be enabled on any provisioning policies. You can find the **Use Microsoft Entra single sign-on** option under the **Join type** on the **General** page. This can be done when [creating a new provisioning policy](create-provisioning-policy.md#continue-creating-a-provisioning-policy) or when [editing an existing provisioning policy](edit-provisioning-policy.md), with an option to apply SSO to existing Cloud PCs.
- When provisioning Frontline Cloud PCs in shared mode, [hide the consent prompt](/azure/virtual-desktop/configure-single-sign-on#hide-the-consent-prompt-dialog) so that users don't see it with each shared device. You can use a dynamic device group based on the provisioning policy name to scope this configuration.

## Next steps

- Check out [In-session passwordless authentication](identity-authentication.md#in-session-passwordless-authentication) to learn how to enable passwordless authentication.
