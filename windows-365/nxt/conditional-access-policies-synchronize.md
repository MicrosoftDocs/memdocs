---
# required metadata
title: Synchronize Conditional Access policies for NXT
titleSuffix:
description: Learn about synchronizing Conditional Access policies for NXT
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
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

# Synchronize Conditional Access policies for NXT

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

As part of [setting up your organization's environment to support NXT devices](deployment-overview.md), you must make sure that your organization's sign-in and connection (if any) Conditional Access (CA) policies are synchronized. If CA is used to protect the resources used to access Windows 365 Cloud PCs, a matching policy must also be used to protect the user action to register or join devices.

## Authentication process for NXT devices

NXT sign-ins have two distinct authentication stages:

1. At the **Sign in** screen.
2. When the NXT connects to the Windows 365 Cloud PC.

Authentication proceeds as follows:

1. The user signs in on the NXT device's interactive Login screen, beginning authentication.
    1. The authentication triggers CA policies on the user action to register or join devices.
    2. If CA policies require stronger authentication, the user completes the extra challenges.
    3. An authentication token is issued with the resulting claims.
2. A non-interactive connection to Windows 365 resources is attempted using the same token issued at sign in.
    1. The connection triggers CA policies on Windows 365 resources.
    2. If CA policies require stronger authentication, the process is interrupted, and the connection fails.
    3. If the token satisfies the conditions of the policy, the connection attempt continues.

CA polices 1a and 2a work together. The interactive sign in triggers the user action policy to obtain the authentication token. Then the non-interactive connection triggers the resource policy which uses that same authentication token.

## Create CA policies to synchronize sign in and connection authentication

If CA is used to protect the resources used to access Windows 365 Cloud PCs, you must create a matching policy to protect the user action to register or join devices.

Also review any existing CA policies that apply to **All resources**. These policies trigger when connecting but not at sign in. Use the [What If tool](/entra/identity/conditional-access/what-if-tool) to help determine what CA policies are applied.

For more information about creating CA policies for user actions to register or join devices, see [Create a Conditional Access policy](/en-us/entra/identity/conditional-access/policy-all-users-device-registration#create-a-conditional-access-policy).

For more information about creating CA policies for resources used for Windows 365, see [Set Conditional Access policies](../enterprise/set-conditional-access-policies.md).

<!-- ########################## -->
## Next steps

[Suppress single sign-on consent prompt](single-sign-on-suppress.md).
