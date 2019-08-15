---
title: How to reset your account
titleSuffix: Configuration Manager
description: Learn how to reset your Desktop Analytics account.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to reset your account

<!-- 3733897 -->

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

If you set up Desktop Analytics in your environment, but want to start over with onboarding and enrollment, use this process to reset your account.

## Prerequisites

Only a **Global Administrator** can reset the account in the Azure portal.

## Behaviors

- This process doesn't change any existing Azure AD users, apps, or permissions

- If you choose to add a new workspace, none of the following user inputs on assets are kept:
    - Importance
    - Owner
    - Upgrade decision
    - Remediation notes

## Process

1. Open the [Desktop Analytics portal](https://aka.ms/desktopanalytics) in Microsoft 365 Device Management as a user with the **Global Administrator** role.

1. In the **Global Settings** menu, select **Connected services**. In the enroll devices section, select the option to **Reset**.

1. If you decide to continue, your account is reset. You'll need to set up Desktop Analytics again.

## Next steps

After reset, refresh the page, and rerun the onboarding process. For more information, see [How to set up Desktop Analytics](/sccm/desktop-analytics/set-up).

If you have any problems during this process, contact Microsoft Support for further assistance.
