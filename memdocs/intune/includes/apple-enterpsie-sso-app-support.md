---
title: include file
description: include file
author: MandiOhlinger
ms.service: microsoft-intune
ms.topic: include
ms.date: 02/28/2024
ms.author: mandia
ms.custom: include file
ms.reviewer: arnab
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. -->

For your apps to use the Microsoft Enterprise SSO plug-in, you have two options:

- **Option 1 - MSAL**: Apps that support the [Microsoft Authentication Library (MSAL)](/entra/identity-platform/msal-overview) automatically take advantage of the Microsoft Enterprise SSO plug-in. For example, Microsoft 365 apps support MSAL. So, they automatically use the plug-in.

  If your organization creates its own apps, then your app developer can add a dependency to the MSAL. This dependency enables your app to use the Microsoft Enterprise SSO plug-in.

  For a sample tutorial, go to [Tutorial: Sign in users and call Microsoft Graph from an iOS or macOS app](/entra/identity-platform/tutorial-v2-ios).

- **Option 2 - AllowList**: Apps that don't support or weren't developed with MSAL can use the SSO app extension. These apps include browsers like Safari and apps that use Safari web view APIs.

  For these non-MSAL apps, add the application bundle ID or prefix to the extension configuration in your Intune SSO app extension policy (in this article).

  For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property in your Intune policy. Be careful with the apps you allow, they can bypass interactive sign-in prompts for the signed in user.

  For more information, go to [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/entra/identity-platform/apple-sso-plugin#applications-that-dont-use-msal).
