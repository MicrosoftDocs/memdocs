---
# required metadata
title: Conditional Access policies for Windows 365 Link
titleSuffix:
description: Learn about Conditional Access policies for Windows 365 Link
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

# Conditional Access policies for Windows 365 Link

As part of [setting up your organization's environment to support Windows 365 Link](deployment-overview.md), you must make sure that your organization's sign-in and connection (if any) Conditional Access policies are synchronized. If Conditional Access is used to protect the resources used to access Windows 365 Cloud PCs, a matching policy must also be used to protect the user action to register or join devices.

## Authentication process for Windows 365 Link devices

1. When the user signs in on the Windows 365 Link interactive **Sign in** screen, their account is authenticated against the device registration service.
2. Windows 365 Link silently authenticates against the other required cloud resources (like Microsoft Graph and the Windows 365 service by using single sign-on (SSO)).

## Create Conditional Access policies to synchronize sign in and connection authentication

If Conditional Access policies enforcing multifactor authentication (MFA) are used to protect the resources used to access Windows 365 Cloud PCs, you must create a Conditional Access policy enforcing MFA on the user action to register or join devices. This second policy must make sure the user's authentication token has the right MFA claims after the initial sign in to Windows 365 Link.

Also review any existing Conditional Access policies that apply to **All resources**. These policies trigger when connecting but not at sign in. Use the [What If tool](/entra/identity/conditional-access/what-if-tool) to help determine what Conditional Access policies are applied.

For more information about creating Conditional Access policies for user actions to register or join devices, see [Create a Conditional Access policy](/entra/identity/conditional-access/policy-all-users-device-registration#create-a-conditional-access-policy).

For more information about creating Conditional Access policies for resources used for Windows 365, see [Set Conditional Access policies](../enterprise/set-conditional-access-policies.md).

For more information about Conditional Access and user actions, see [User actions](/entra/identity/conditional-access/concept-conditional-access-cloud-apps#user-actions).

<!-- ########################## -->
## Next steps

[Suppress single sign-on consent prompt](single-sign-on-suppress.md).
