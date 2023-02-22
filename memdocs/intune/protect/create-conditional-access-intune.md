---
# required metadata

title: Set up device-based Conditional Access policies with Intune
titleSuffix: Microsoft Intune
description: Configure a device-based Conditional Access policy that uses device status from a Microsoft Intune device compliance policies.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/11/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Create a device-based Conditional Access policy

With Microsoft Intune device compliance policies, your Azure Active Directory (Azure AD) Conditional Access policies can use a devices status to either grant or deny access to your organizations apps and services.

You can use the Microsoft Endpoint Manager admin center to configure your device-based Conditional Access policies. From within the admin center you have access to the Conditional Access policy UI as found in Azure AD. Use of the Azure AD UI provides access to all the options you would have if you were to configure the policy from within the Azure portal. The policies you create can specify the apps or services you want to protect, the conditions under which the apps or services can be accessed, and the users the policy applies to.

To Create a device-based Conditional Access policy your account must have one of the following permissions in Azure AD:

- Global administrator
- Security administrator
- Conditional Access administrator

To take advantage of device compliance status, configure Conditional Access policies to **Require device to be marked as compliant**. This option is set while configuring *Grant* access during step 6 of the following procedure.

> [!IMPORTANT]
> Before you set up Conditional Access, you'll need to set up Intune device compliance policies to evaluate devices based on whether they meet specific requirements. See [Get started with device compliance policies in Intune](device-compliance-get-started.md).

## Create the Conditional Access policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional access** > **Policies** > **New policy**.
:::image type="content" source="./media/create-conditional-access-intune/create-ca.png" alt-text="Create a new Conditional Access policy":::

   The **New** pane opens, which is the configuration pane from Azure AD. The policy you’re creating is an Azure AD policy for Conditional Access. To learn more about this pane and Conditional Access policies, see [Conditional Access policy components](/azure/active-directory/conditional-access/concept-conditional-access-policies) in the Azure AD content.

3. Under **Assignments**, configure **Users** to select the Identities in the directory that the policy applies to. To learn more, see [Users and groups](/azure/active-directory/conditional-access/concept-conditional-access-users-groups) in the Azure AD documentation.

   - On the **Include** tab, configure the user and groups you want to include.  
   - Use the **Exclude** tab if there are any users, roles, or groups you want to exclude from this policy.

   > [!TIP]
   > Test the policy against a smaller group of users to make sure it works as expected before deploying it to larger groups.

4. Next configure **Cloud apps or actions**, which is also under *Assignments*. For the drop-down selection for what this policy applies to, choose **Cloud apps**.

   - On the **Include** tab, use available options to identify the apps and services you want to protect with this Conditional Access policy.

     If you choose **Select apps**, select the apps and services you want to protect with this policy. 

     > [!CAUTION]
     > If you choose  **All cloud apps**, be sure to review the warning, and then **Exclude** from this policy your account or other relevant users and groups that should retain access to use the Azure portal or Microsoft Endpoint Manager admin center after this policy takes effect.

   - Use the **Exclude** tab if there are any apps or services you want to exclude from this policy.

   For more information, see [Cloud apps or actions](/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps) in the Azure AD documentation.

5. Next, configure **Conditions**. Select the signals you want to use as conditions for this policy. Options include:

   - User risk
   - Sign-in risk
   - Device platforms
   - Locations
   - Client apps
   - Filter for devices

   For information about these options, see [Conditions](/azure/active-directory/conditional-access/concept-conditional-access-conditions) in the Azure AD documentation.

   > [!TIP]
   > If you want to protect both **Modern authentication** clients and **Exchange ActiveSync clients**, create two separate Conditional Access policies, one for each client type. Although Exchange ActiveSync supports modern authentication, the only condition that is supported by Exchange ActiveSync is platform. Other conditions, including multi-factor authentication, are not supported. To effectively protect access to Exchange Online from Exchange ActiveSync, create a Conditional Access policy that specifies the cloud app Microsoft 365 Exchange Online and the client app Exchange ActiveSync with Apply policy only to supported platforms selected.

6. Under **Access controls**, select **Grant** and then one or more requirements. To learn about the options for Grant, see [Grant](/azure/active-directory/conditional-access/concept-conditional-access-grant) in the Azure AD Documentation.

   - **Block access**: The users specified in this policy will be denied access to the apps or services under the conditions you've specified.
   - **Grant access**: The users specified in this policy will be granted access, but you can require any of the following further actions:
     - Require multi-factor authentication
     - *Require device to be marked as compliant* - This option is required for the policy to use device compliance status.
     - Require Hybrid Azure AD joined device
     - Require approved client app
     - Require app protection policy
     - Require password change

     :::image type="content" source="./media/create-conditional-access-intune/create-ca-grant-access-settings.png" alt-text="Screen shot of the configuration surface and options for Grant":::

7. Under **Enable policy**, select **On**. By default, the policy is set to *Report-only*.

8. Select **Create**.

## Next steps

[App-based Conditional Access with Intune](app-based-conditional-access-intune.md)

[Troubleshooting Intune Conditional Access](https://support.microsoft.com/help/4456106)
