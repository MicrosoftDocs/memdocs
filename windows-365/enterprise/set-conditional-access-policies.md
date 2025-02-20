---
# required metadata
title: Set Conditional Access policies for Windows 365
titleSuffix:
description: Learn how to set Conditional Access policies for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 7/26/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

# Set Conditional Access policies

Conditional Access is the protection of regulated content in a system by requiring certain criteria to be met before granting access to the content. Conditional Access policies at their simplest are if-then statements. If a user wants to access a resource, then they must complete an action. For example, a payroll manager wants to access the payroll application and is required to perform multi-factor authentication (MFA) to do so.

Using Conditional Access, you can achieve two primary goals:

- Empower users to be productive anywhere at any time.
- Protect your organization's assets.

By using Conditional Access policies, you can apply the right access controls when needed to keep your organization secure and stay out of your user's way when not needed.

How often a user is prompted to reauthenticate depends on [Microsoft Entra session lifetime configuration settings](/entra/identity/authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime#azure-ad-session-lifetime-configuration-settings). While remembering credentials is convenient, it can also make deployments for Enterprise scenarios using personal devices less secure. To protect your users, you can make sure the client asks for Microsoft Entra multi-factor authentication credentials more frequently. You can use Conditional Access sign-in frequency to configure this behavior.

## Assign a Conditional Access policy for Cloud PCs

Conditional Access policies aren't set for your tenant by default.  You can target CA policies to the Cloud PC first-party app by using either of the following platforms:

- Azure. For more information, see [Microsoft Entra Conditional Access](/azure/active-directory/conditional-access/).
- Microsoft Intune. The steps below explain this process. For more information, see [Learn about Conditional Access and Intune](/mem/intune-service/protect/conditional-access).

No matter which method you use, the policies will be enforced on the Cloud PC End-user portal and the connection to the Cloud PC.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Endpoint security** > **Conditional Access** > **Create new policy**.
2. Provide a **Name** for your specific Conditional Access policy.
3. Under **Users**, select **0 users and groups selected**.
4. Under the **Include** tab, select **Select users and groups** > check **Users and groups** > under **Select**, choose **0 users and groups selected**.
5. On the new pane that opens, search for and select the specific user or group that you want to target with the CA policy, then choose **Select**.
6. Under **Target resources**, select **No target resources selected**.
7. Under the **Include** tab, choose **Select apps** > under **Select**, choose **None**.
8. In the **Select** pane, search for and select the following apps based on the resources you are trying to protect:
    - **Windows 365** (app ID 0af06dc6-e4b5-4f28-818e-e78e62d137a5). You can also search for "cloud" to find this app. This app is used when retrieving the list of resources for the user and when users initiate actions on their Cloud PC like Restart.
    - **Azure Virtual Desktop** (app ID 9cdead84-a844-4324-93f2-b2e6bb768d07). This app may also appear as **Windows Virtual Desktop**. This app is used to authenticate to the Azure Virtual Desktop Gateway during the connection and when the client sends diagnostic information to the service.
    - **Microsoft Remote Desktop** (app ID a4a365df-50f1-4397-bc59-1a1564b8bb9c) and **Windows Cloud Login** (app ID 270efc09-cd0d-444b-a71f-39af4910ec45). These apps are only needed when you [configure single sign-on](configure-single-sign-on.md) in a provisioning policy. These apps are used to authenticate users to the Cloud PC.

     It's recommended to match Conditional Access policies between these apps. This ensures that the policy applies to the Cloud PC End-user portal, the connection to the Gateway and the Cloud PC for a consistent experience. If you want to exclude apps, you must also choose all of these apps.

     > [!IMPORTANT]
     > With SSO enabled, authentication to the Cloud PC uses the **Microsoft Remote Desktop** Entra ID app today. An upcoming change will transition the authentication to the **Windows Cloud Login** Entra ID app. To ensure a smooth transition, you need to add both Entra ID apps to your CA policies.

     > [!NOTE]
     > If you don't see the Windows Cloud Login app when configuring your Conditional Access policy, use the steps below to create the app. You must have Owner or Contributor permissions on the subscription to make these changes:
     >
     >  1. Sign into the [Azure Portal](https://portal.azure.com).
     >  1. Select **Subscriptions** from the list of Azure Services.
     >  1. Select your Subscription name.
     >  1. Select **Resource providers** then select **Microsoft.DesktopVirtualization**.
     >  1. Select **Register** at the top.
     >
     > After the resource provider is registered, the Windows Cloud Login app appears in the Conditional Access policy configuration when selecting apps to apply the policy to. If you aren't using Azure Virtual Desktop, you can unregister the Microsoft.DesktopVirtualization resource provider after the Windows Cloud Login app is available.
9. If you want to fine-tune your policy, under **Grant**, choose **0 controls selected**.
10. In the **Grant** pane, choose the grant or block access options that you want to apply to all objects assigned to this policy > **Select**.
11. If you want to test your policy first, under **Enable policy**, select **Report-only**. If you set it to **On**, the policy will be applied as soon as you create it.
12. Select **Create** to create the policy.

You can see your list of active and inactive policies in the **Policies** view in the Conditional Access UI.

## Configure sign-in frequency

Sign-in frequency policies let you configure how often users are required to sign-in when accessing Microsoft Entra-based resources. This can help secure your environment and is especially important for personal devices, where the local OS may not require MFA or may not lock automatically after inactivity. Users are prompted to authenticate only when a new access token is requested from Microsoft Entra ID when accessing a resource.

Sign-in frequency policies result in different behavior based on the Microsoft Entra app selected:

| App name | App ID | Behavior |
|--|--|--|
| **Windows 365** | 0af06dc6-e4b5-4f28-818e-e78e62d137a5 | Enforces re-authentication when a user retrieves their list of Cloud PCs and when users initiate actions on their Cloud PC like Restart. |
| **Azure Virtual Desktop** | 9cdead84-a844-4324-93f2-b2e6bb768d07 | Enforces re-authentication when a user authenticates to the Azure Virtual Desktop Gateway during a connection. |
| **Microsoft Remote Desktop**<br /><br />**Windows Cloud Login** | a4a365df-50f1-4397-bc59-1a1564b8bb9c<br /><br />270efc09-cd0d-444b-a71f-39af4910ec45 | Enforces re-authentication when a user signs in to the Cloud PC when [single sign-on](configure-single-sign-on.md) is enabled.<br /><br />Both apps should be configured together as the clients will soon switch from using the Microsoft Remote Desktop app to the Windows Cloud Login app to authenticate to the Cloud PC. |

To configure the time period after which a user is asked to sign-in again:

1. Open the policy you created previously.
1. Under **Session**, select **0 controls selected**.
1. In the **Session** pane, select **Sign-in frequency**.
1. Select **Periodic reauthentication** or **Every time**.
    - If you select **Periodic reauthentication**, set the value for the time period after which a user is asked to sign-in again when performing an action that requires a new access token, and then select **Select**. For example, setting the value to **1** and the unit to **Hours**, requires multi-factor authentication if a connection is launched more than an hour after the last user authentication.
    - The **Every time** option is currently available in preview and is only supported when applied to the **Microsoft Remote Desktop** and **Windows Cloud Login** apps when single sign-on is enabled for your Cloud PCs. If you select **Every time**, users are prompted to re-authenticate when launching a new connection after a period of 5 to 10 minutes since their last authentication.
1. At the bottom of the page, select **Save**.

> [!NOTE]
>
> - Re-authentication only happens when a user must authenticate to a resource and a new access token is needed. After a connection is established, users aren't prompted even if the connection lasts longer than the sign-in frequency you've configured.
> - Users must re-authenticate if there is a network disruption that forces the session to be re-established after the sign-in frequency you've configured. This can lead to more frequent authentication requests on unstable networks.

## Next steps

[Manage RDP device redirections](manage-rdp-device-redirections.md)
