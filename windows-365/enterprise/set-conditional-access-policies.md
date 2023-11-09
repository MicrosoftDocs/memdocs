---
# required metadata
title: Set conditional access policies for Windows 365
titleSuffix:
description: Learn how to set conditional access policies for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/06/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Set conditional access policies

Conditional Access is the protection of regulated content in a system by requiring certain criteria to be met before granting access to the content. Conditional Access policies at their simplest are if-then statements. If a user wants to access a resource, then they must complete an action. For example, a payroll manager wants to access the payroll application and is required to perform multi-factor authentication (MFA) to do so.

Using Conditional Access, you can achieve two primary goals:

- Empower users to be productive anywhere at any time.
- Protect your organization's assets.

By using Conditional Access policies, you can apply the right access controls when needed to keep your organization secure and stay out of your user's way when not needed.

## Assign a Conditional Access policy for Cloud PCs

Conditional Access policies aren't set for your tenant by default.  You can target CA policies to the Cloud PC first-party app by using either of the following platforms:

- Azure. For more information, see [Microsoft Entra Conditional Access](/azure/active-directory/conditional-access/).
- Microsoft Intune. The steps below explain this process. For more information, see [Learn about Conditional Access and Intune](/mem/intune/protect/conditional-access).

No matter which method you use, the policies will be enforced on the Cloud PC End-user portal and the connection to the Cloud PC.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Endpoint security** > **Conditional access** > **Create new policy**.
2. Provide a **Name** for your specific Conditional Access policy.
3. Under **Users**, choose **0 users and groups selected**. Select the specific user or group you want to target with the CA policy. You can also **Exclude** certain users or groups to fine-tune the assignment.
4. Under **Cloud apps or actions**, select **No cloud apps, actions, or authentication contexts selected**.
5. Select **Cloud apps** > **Include** > **Select apps** > **None** (under **Select**).
6. In the **Select** pane, search for and select the following apps as needed:
    - **Windows 365** (app ID 0af06dc6-e4b5-4f28-818e-e78e62d137a5). You can also search for "cloud" to find this app. This app is used when retrieving the list of resources for the user and when users initiate actions on their Cloud PC like Restart.
    - **Azure Virtual Desktop** (app ID 9cdead84-a844-4324-93f2-b2e6bb768d07). This app may also appear as **Windows Virtual Desktop**. This app is used to authenticate to the Gateway during the connection and when the client sends diagnostic information to the service.
    - **Microsoft Remote Desktop** (app ID a4a365df-50f1-4397-bc59-1a1564b8bb9c) and **Windows Cloud Login** (app ID 270efc09-cd0d-444b-a71f-39af4910ec45). These apps are only needed when **Use Microsoft Entra single sign-on (preview)** is enabled in a provisioning policy. These apps are used to authenticate users to the Cloud PC.

     It's recommended to match conditional access policies between these apps. This ensures that the policy applies to the Cloud PC End-user portal, the connection to the Gateway and the Cloud PC for a consistent experience. If you want to exclude apps, you must also choose all of these apps.

     > [!IMPORTANT]
     > With SSO enabled, authentication to the Cloud PC uses the **Microsoft Remote Desktop** Entra ID app today. An upcoming change will transition the authentication to the **Windows Cloud Login** Entra ID app. To ensure a smooth transition, you need to add both Entra ID apps to your CA policies.

7. If you want to fine-tune your policy, under **Access controls**, choose **0 controls selected**. Under **Grant**, choose the options that you want to apply to all objects assigned to this policy.
8. If you want to test your policy first, under **Enable Policy**, set **Report-only** to **Off**. If you set it to **On**, the policy will be applied as soon as you create it.
9. Select **Create** to create the policy.

You can see your list of active and inactive policies in the **Policies** view in the Conditional Access UI.

<!-- ########################## -->
## Next steps

[Manage RDP device redirections](manage-rdp-device-redirections.md)
