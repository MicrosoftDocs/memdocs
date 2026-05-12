---
title: Set up device-based Conditional Access policies with Intune
description: Configure a device-based Conditional Access policy that uses device compliance status from Intune device compliance policies.
author: lenewsad
ms.author: lanewsad
ms.date: 09/18/2023
ms.topic: how-to
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- conditional-access
- sub-device-compliance
---

# Create a device-based Conditional Access policy

Microsoft Intune device compliance policies can evaluate the status of managed devices to ensure they meet your requirements before you grant them access to your organization's apps and services. The status results from your device compliance policies can be used by Microsoft Entra Conditional Access policies to enforce security and compliance standards. This combination is referred to as device-based Conditional Access.

> [!TIP]
> In addition to device-based Conditional Access policies, you can use [App-based Conditional Access with Intune](./app-based-policies.md).

Conditional Access is a Microsoft Entra technology. The Conditional Access node you access from the Microsoft Intune admin center is the same node you access from Microsoft Entra ID, so you don't need to switch between them to configure policies.

## Requirements

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> Before you create a device-based Conditional Access policy, you must have a **Microsoft Entra ID P1 or P2** license. For more information, see [Microsoft Entra pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing).

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::

> Your account must have one of the following roles in Microsoft Entra:
> - Security administrator
> - Conditional Access administrator

:::column-end:::
:::row-end:::

> [!IMPORTANT]
> Before you set up Conditional Access, you'll need to set up Intune device compliance policies to evaluate devices based on whether they meet specific requirements. See [Get started with device compliance policies in Intune](../compliance/create-policy.md).

## How this works

Device-based Conditional Access uses compliance status signals from Intune to enforce access controls in Microsoft Entra ID. Configuration involves two phases:

- Phase 1 - Configure device compliance policies in Intune: These policies evaluate whether managed devices meet your security requirements. Intune reports that compliance status to Microsoft Entra ID.

- Phase 2 - Create a Conditional Access policy in Microsoft Entra: The policy uses the compliance signal from Intune. This article shows you how to configure the policy from within the Microsoft Intune admin center.

## Create the Conditional Access policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional Access** > **Create new policy**.
:::image type="content" source="./media/create-conditional-access-intune/create-ca.png" alt-text="Create a new Conditional Access policy":::

   The **New** pane opens, which is the configuration pane from Microsoft Entra. The policy you’re creating is a Microsoft Entra policy for Conditional Access. To learn more about this pane and Conditional Access policies, see [Conditional Access policy components](/entra/identity/conditional-access/concept-conditional-access-policies) in the Microsoft Entra content.

3. Under **Assignments**, configure **Users and groups** to select the Identities in the directory that the policy applies to. To learn more, see [Users and groups](/entra/identity/conditional-access/concept-conditional-access-users-groups) in the Microsoft Entra documentation.

   - On the **Include** tab, configure the user and groups you want to include.
   - Use the **Exclude** tab if there are any users, roles, or groups you want to exclude from this policy.

   > [!TIP]
   > Test the policy against a smaller group of users to make sure it works as expected before deploying it to larger groups.

4. Next configure **Target resources**, which is also under *Assignments*. Use the drop-down for *Select what this policy applies to* to select **Cloud apps**.

   - On the **Include** tab, use available options to identify the apps and services that you want to protect with this Conditional Access policy.

     If you choose **Select apps**, use the available UI to select apps and services to protect with this policy.

     > [!CAUTION]
     > **Don't lock yourself out**. If you choose **All cloud apps**, be sure to review the warning, and then **Exclude** from this policy your user account or other relevant users and groups that should retain access to use the Microsoft Entra admin center or Microsoft Intune admin center after this policy takes effect.

   - Use the **Exclude** tab if there are any apps or services you want to exclude from this policy.

   For more information, see [Cloud apps or actions](/entra/identity/conditional-access/concept-conditional-access-cloud-apps) in the Microsoft Entra documentation.

5. Next, configure **Conditions**. Select the signals you want to use as conditions for this policy. Options include:

   - User risk
   - Sign-in risk
   - Device platforms
   - Locations
   - Client apps
   - Filter for devices

   For information about these options, see [Conditions](/entra/identity/conditional-access/concept-conditional-access-conditions) in the Microsoft Entra documentation.

   > [!TIP]
   > If you want to protect both **Modern authentication** clients and **Exchange ActiveSync clients**, create two separate Conditional Access policies, one for each client type. Although Exchange ActiveSync supports modern authentication, the only condition that is supported by Exchange ActiveSync is platform. Other conditions, including multi-factor authentication, aren't supported. To effectively protect access to Exchange Online from Exchange ActiveSync, create a Conditional Access policy that specifies the cloud app Microsoft 365 Exchange Online and the client app Exchange ActiveSync with Apply policy only to supported platforms selected.

6. Under **Access controls**, configure **Grant** to select one or more requirements. To learn about the options for Grant, see [Grant](/entra/identity/conditional-access/concept-conditional-access-grant) in the Microsoft Entra Documentation.

   > [!IMPORTANT]
   >
   > To have this policy use device compliance status, for *Grant access* you must select *Require device to be marked as compliant*.

   - **Block access**: Denies access to the specified apps or services.
   - **Grant access**: Grants access, but you can require one or more conditions. To use device compliance status from Intune, select **Require device to be marked as compliant**.

     :::image type="content" source="./media/create-conditional-access-intune/create-ca-grant-access-settings.png" alt-text="Screenshot of the configuration surface and options for Grant":::

7. Under **Enable policy**, select **On**. By default, the policy is set to *Report-only*.

8. Select **Create**.

## Next steps

- [App-based Conditional Access with Intune](./app-based-policies.md)
- [Troubleshooting Intune Conditional Access](/troubleshoot/mem/intune/device-protection/troubleshoot-conditional-access)
