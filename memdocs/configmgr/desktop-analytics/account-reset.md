---
title: How to reset your account
titleSuffix: Configuration Manager
description: Learn how to reset your Desktop Analytics account.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# How to reset your account

<!-- 3733897 -->

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

After reset, refresh the page, and rerun the onboarding process. For more information, see [How to set up Desktop Analytics](set-up.md).

If you have any problems during this process, contact Microsoft Support for further assistance.
