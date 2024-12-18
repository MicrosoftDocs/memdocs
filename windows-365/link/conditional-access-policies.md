---
# required metadata
title: Conditional Access policies for Windows 365 Link
titleSuffix:
description: Learn about Conditional Access policies for Windows 365 Link
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/13/2024
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

As part of [setting up your organization's environment to support Windows 365 Link](deployment-overview.md), you must make sure that your Conditional Access policies accommodate both the login through and connection from Windows Cloud PC devices. If Conditional Access is used to protect the resources used to access Windows 365 Cloud PCs as described in [Set conditional access policies for Windows 365](/windows-365/enterprise/set-conditional-access-policies), a separate but matching Conditional Access policy must also be used to protect the user action to register or join devices.

## Authentication process for Windows 365 Link devices

1. When the user signs in on the Windows 365 Link interactive **Sign in** screen, their account is authenticated against the device registration service.
2. Windows 365 Link silently authenticates against the other required cloud resources (like Microsoft Graph and the Windows 365 service by using single sign-on (SSO)).

Windows 365 Cloud PC devices have two distinct stages of authentication:

- Interactive sign-in: When the user signs in on the Windows 365 Link sign in screen, the device registration service is used to get an authentication token.
- Non-interactive connections: The token obtained from the user sign in is then used to perform non-interactive sign-ins when connecting to other cloud app resources like Windows 365 services.

Sign-ins from Windows 365 Link devices don't trigger any Conditional Access policies that are targeted to *All resources (formerly cloud apps)* or directly to the *Device Registration Service* resource. Also, the non-interactive connection can't prompt a user to satisfy those requirements.

If a Conditional Access policy is assigned to any of the Windows 365 resources, then another policy with the same Access control settings must also be applied to the User Actions to Register or join devices. This policy can trigger an interactive sign-in and obtain the claims that are necessary for the connection.

Without a matching set of policies, the connection is interrupted, and users can't connect to their Cloud PC.

These activities can be seen in the Entra Conditional Access sign-in logs:

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/) > **Protection** > **Conditional Access** > **Sign-in logs**.
2. On the **User sign-ins (interactive)** tab, use filters to find events from the sign in screen.
3. On the **User sign-ins (non-interactive)** tab, use filters to find events from the connections. 

## Create a Conditional Access policy for interactive sign in

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/) > **Protection** > **Conditional Access** > **Policies** > **What if**.
2. For **User or Workload identity** select a user to test with.
3. For Cloud apps, actions, or authentication context, select **Any cloud app**.
4. For **Select target type** leave **Cloud app** selected.
5. Select **Select apps** then select the following resources, if they're available:
    - **Windows 365** (app ID 0af06dc6-e4b5-4f28-818e-e78e62d137a5).
    - **Azure Virtual Desktop** (app ID 9cdead84-a844-4324-93f2-b2e6bb768d07).
    - **Microsoft Remote Desktop** (app ID a4a365df-50f1-4397-bc59-1a1564b8bb9c).
    - **Windows Cloud Login** (app ID 270efc09-cd0d-444b-a71f-39af4910ec45).
6. Select **What If**.

Review each of the **Policies that will apply** and determine the access controls used to grant access to those resources and session settings.

You can now create a new Conditional Access policy to [Require MFA for device registration](/entra/identity/conditional-access/policy-all-users-device-registration#create-a-conditional-access-policy) using the same Access controls.

1. Sign in to the [Microsoft Entra admin center](https://aad.portal.azure.com/) > **Protection** > **Conditional Access** > **Polices** > **New policy**
2. Give your policy a name. Consider using a meaningful standard for policy names.
3. Under **Assignments** > **Users**, select **0 users and groups selected**.
4. Under **Include**, select **All users** or select a group of users who will sign-in through Windows 365 Link devices.
5. Under **Exclude**, select **Users and groups** > select your organization's emergency access or break-glass accounts.
6. Under **Target resources** > **User actions**, select **Register or join devices**.
7. Under **Access controls** > **Grant**, use the same controls found earlier using the What If tool.
8. Under **Access controls** > **Session**, use the same controls found earlier using the What If tool.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create**.
11. After confirming the settings using report-only mode, change the **Enable policy** toggle from **Report-only** to **On**.

For more information about creating Conditional Access policies for device registration, including potential conflicts, see [Require multifactor authentication for device registration](/entra/identity/conditional-access/policy-all-users-device-registration#create-a-conditional-access-policy).

For more information about user actions with Conditional Access, see [User actions](/entra/identity/conditional-access/concept-conditional-access-cloud-apps#user-actions).

For more information about creating Conditional Access policies for resources used for Windows 365, see [Set Conditional Access policies](../enterprise/set-conditional-access-policies.md).

<!-- ########################## -->
## Next steps

[Suppress single sign-on consent prompt](single-sign-on-suppress.md).
