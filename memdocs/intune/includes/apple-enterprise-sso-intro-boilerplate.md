---
title: include file
description: include file
author: miepping
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/18/2023
ms.author: miepping
ms.custom: include file
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. 4.10.2023 (mandia): Removed 'preview'. -->

The Microsoft Enterprise SSO plug-in provides single sign-on (SSO) to apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365. This plug-in uses the Apple single sign-on app extension framework. It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including any MDM that supports configuring SSO profiles.

Once set up, apps that support the Microsoft Authentication Library (MSAL) automatically take advantage of the Microsoft Enterprise SSO plug-in. Apps that don't support MSAL can be allowed to use the extension, including browsers like Safari and apps that use Safari web view APIs. Just add the application bundle ID or prefix to the extension configuration.

For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property. Be careful with the apps you allow, they'll be able to bypass interactive sign-in prompts for the signed in user.

For more information, see [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#applications-that-dont-use-msal).

> [!NOTE]
> Announced in March 2024, Microsoft Entra ID will be moving away from Apple’s Keychain for storing device identity keys. Starting in Q3 2026, all new device registrations will use Apple’s Secure Enclave by default. For more information see [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin#upcoming-changes-to-device-identity-key-storage). 

