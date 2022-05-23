---
# required metadata

title: Drive end-user adoption with Conditional Access
titleSuffix: Microsoft Intune
description: Learn how to use Conditional Access to drive enrollment in Microsoft Intune.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: c2d7ce3f-fe97-4044-ad9e-25ac8fa301c9

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Drive end-user adoption with Conditional Access in Microsoft Intune

Enabling Conditional Access features with Intune, such as blocking email for unenrolled devices, can help drive enrollment and compliance but they are not required for a migration to be successful. Your migration adoption goals and security requirements should dictate the success.

## Migration campaign with Conditional Access

Here is a typical approach to enhancing a migration campaign with Conditional Access:

1. Set Conditional Access rules to be enforced for all users but specifically exclude the users who need to migrate from the old MDM provider. You can create an Azure AD user group with all Conditional Access excluded users.

2. As users migrate, remove them from the Conditional Access exclusion group.

3. After migration completes, configure all Conditional Access policies to block by default unless Intune allows access.

### Advantages

- Provides access control for new user accounts or user account who were not managed by the previous solution.

- Provides grace period for users of previous solution to migration.

- Minimizes loss of productivity

### Disadvantages

- Users of previous solution could potentially access resources using unmanaged devices until Conditional Access is enabled for those users.


This is one approach among many. You may choose a simpler process that defers all Conditional Access until after every phase has been instructed to enroll, or a stricter process that enforces Conditional Access from the very beginning and requires full compliance for all access.

- Learn more about [Conditional Access](../protect/conditional-access.md).

## Task list for Conditional Access

### Task 1: Decide how you are going to implement Conditional Access

[Common ways to use Conditional Access](../protect/conditional-access-intune-common-ways-use.md).

### Task 2: Set up Intune Conditional Access

Choose one of the following options:

- [Configure Conditional Access in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)

- [Configure Hybrid Modern Authentication](/office365/enterprise/hybrid-modern-auth-overview)

- [Set up app-based Conditional Access policies for Exchange Online](../protect/app-based-conditional-access-intune-create.md)

- [Set up app-based Conditional Access policies for SharePoint Online](../protect/app-based-conditional-access-intune-create.md)

- [Block apps that do not use modern authentication (MSAL)](../protect/app-modern-authentication-block.md) 

## Next steps

Be sure to [create a rollout plan](intune-planning-guide.md).
