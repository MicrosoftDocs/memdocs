---
title: include file
description: include file
author: MandiOhlinger
ms.service: microsoft-intune
ms.topic: include
ms.date: 05/01/2024
ms.author: mandia
ms.custom: include file
ms.reviewer: miepping
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. 4.10.2023 (mandia): Removed 'preview'. 4.16.2024 (mandia) Updated for platform SSO.-->

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) is a feature in Microsoft Entra ID that provides single sign-on (SSO) features for Apple devices. This plug-in uses the Apple single sign-on app extension framework.

- For iOS/iPadOS devices, the Enterprise SSO plug-in includes the **SSO app extension**.
- For macOS devices, the Enterprise SSO plug-in includes **[Platform SSO and the SSO app extension](../configuration/platform-sso-macos.md)**.

The **SSO app extension** provides single sign-on to apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365 apps. It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including any MDM that supports configuring SSO profiles.
