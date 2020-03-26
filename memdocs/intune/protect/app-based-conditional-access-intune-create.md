---
# required metadata

title: Set up app-based Conditional Access policy with Intune
titleSuffix: Microsoft Intune
description: Learn how to create an app-based Conditional Access policy with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set up app-based Conditional Access policies with Intune

Set up app-based Conditional Access policies for apps that are part of the list of approved apps. The list of approved apps consists of apps that were tested by Microsoft.

Before you can use app-based Conditional Access policies, you need to have [Intune app protection policies](../apps/app-protection-policies.md) applied to your apps.

> [!IMPORTANT]
> This article walks through the steps to add an app-based Conditional Access policy. You can use the same steps when add apps like SharePoint Online, Microsoft Teams, and Microsoft Exchange Online from the list of approved apps.

## Create app-based Conditional Access policies

Conditional Access is an Azure Active Directory (Azure AD) technology. The Conditional Access node you access from *Intune* is the same node that you access from *Azure AD*. Because it's the same node, you don't need to switch between Intune and Azure AD to configure policies.

Before you can create Conditional Access policies from the Microsoft Endpoint Manager admin center, you must have an Azure AD Premium license.

### To create an app-based Conditional Access policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Select **Endpoint security** > **Conditional access** > **New policy**.

3. Enter a policy **Name**, and then under *Assignments*, select **Users and groups**. Use the Include or Exclude options to add your groups for the policy, and select **Done**.

4. Select **Cloud apps or actions**, and choose which apps to protect. For example, choose **Select apps**, and select **Office 365 SharePoint Online** and **Office 365 Exchange Online**.

   Select **Done** to save your changes.

5. Select **Conditions** > **Client apps** to apply the policy to apps and browsers. For example, select **Yes**, and then enable **Browser** and **Mobile apps and desktop clients**.

   Select **Done** to save your changes.

6. Under *Access controls*, select **Grant** to apply Conditional Access based on device compliance. For example, select **Grant access** > **Require device to be marked as compliant**.

   Choose **Select** to save your changes.

7. For **Enable policy**, select **On**, and then select **Create** to save your changes.





## Next steps
[Block apps that don't have modern authentication](app-modern-authentication-block.md)

## See also

[Protect app data with app protection policies](../apps/app-protection-policies.md)
[Conditional Access in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
