---
# required metadata

title: Set up app-based Conditional Access policies with Intune
titleSuffix: Microsoft Intune
description: Create Conditional Access policies that work with Intune app protection policies
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- conditional-access
- sub-device-compliance
---

# Set up app-based Conditional Access policies with Intune

Set up app-based Conditional Access policies for apps that are part of the list of approved apps. The list of approved apps consists of apps that were tested by Microsoft.

Before you can use app-based Conditional Access policies, you need to have [Intune app protection policies](../apps/app-protection-policies.md) applied to your apps.

> [!IMPORTANT]
> This article walks through the steps to add a simple app-based Conditional Access policy. You can use the same steps for other cloud apps. For more information, see [Plan Conditional Access deployment](/azure/active-directory/conditional-access/plan-conditional-access)

## Create app-based Conditional Access policies

Conditional Access is a Microsoft Entra technology. The Conditional Access node you access from *Intune* is the same node that you access from *Microsoft Entra ID*. Because it's the same node, you don't need to switch between Intune and Microsoft Entra ID to configure policies.

Before you can create Conditional Access policies from the Microsoft Intune admin center, you must have a Microsoft Entra ID P1 or P2 license.

### To create an app-based Conditional Access policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Select **Endpoint security** > **Conditional Access** > **New policy**.

3. Enter a policy **Name**, and then under *Assignments*, select **Users or workload identities**, and apply the policy to *Users and groups*. Use the Include or Exclude options to add your groups for the policy.

4. Select **Cloud apps or actions**, and apply the policy to *Cloud apps*. Use the Include or Exclude options to select the apps to protect. For example, choose **Select apps**, and select **Office 365 (preview)**.

5. Select **Conditions** > **Client apps** to apply the policy to apps and browsers. For example, select **Yes**, and then select the checkboxes for enable **Browser** and **Mobile apps and desktop clients**.

6. Under *Access controls*, select **Grant** to apply Conditional Access based on a device compliance status. For example, select **Grant access** > **Require approved client app** and **Require app protection policy**, then select **Require one of the selected controls**.

7. For **Enable policy**, select **On**, and then select **Create** to save your changes. By default, *Enable policy* is set to *Report-only*.

## Next steps

- [Block apps that don't have modern authentication](app-modern-authentication-block.md)
- [Protect app data with app protection policies](../apps/app-protection-policies.md)
- Learn about [Conditional Access in Microsoft Entra ID](/azure/active-directory/active-directory-conditional-access)
