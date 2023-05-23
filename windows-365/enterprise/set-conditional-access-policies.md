---
# required metadata
title: Set conditional access policies for Windows 365
titleSuffix:
description: Learn how to set conditional access policies for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
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

- Azure. For more information, see [Azure AD Conditional Access](/azure/active-directory/conditional-access/).
- Microsoft Endpoint Manager. The steps below explain this process. For more information, see [Learn about Conditional Access and Intune](/mem/intune/protect/conditional-access).

No matter which method you use, the policies will be enforced on the Cloud PC End-user portal and the connection to the Cloud PC.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Endpoint Security** > **Conditional Access** > **New Policy**.
2. Provide a **Name** for your specific Conditional Access policy.
3. On the **New Policy** tab, under **Users and groups**, choose **Specific users included**. Select the specific user or group you want to target with the CA policy. You can also **Exclude certain users or groups** to fine-tune the assignment.
4. Under **Cloud apps or actions**, select **No cloud apps, action, or authentication contexts selected**.
5. Select **Cloud apps** > **Include** > **Select apps**.
6. In the **Select** pane, search for and select both the following apps:
    - **Windows 365** (you can also search for "cloud" to find this app).
    - **Windows Virtual Desktop** (this may also appear as **Azure Virtual Desktop**)

    By choosing both of these apps, you make sure that the policy applies to the Cloud PC End-user portal and the connection to the Cloud PC. If you want to exclude apps, you must also choose both these apps.
    
   >[!NOTE]
   >If you have configured a provisioning policy to **Use single sign-on (preview)**, you may need to also add the **Microsoft Remote Desktop** to the exclude list in Step 6 for single sign-on connections to work as expected.

7. If you want to fine-tune your policy, under **Access controls**, choose **0 controls selected**.  Under **Grant**, choose the options that you want to apply to all objects assigned to this policy.
8. If you want to test your policy first, under **Enable Policy**, set **Report-only** to **Off**. If you set it to **On**, the policy will be applied as soon as you create it.
9. Select **Create** to create the policy.

You can see your list of active and inactive policies in the **Policies** view in the Conditional Access UI.

<!-- ########################## -->
## Next steps

[Manage RDP device redirections](manage-rdp-device-redirections.md)
