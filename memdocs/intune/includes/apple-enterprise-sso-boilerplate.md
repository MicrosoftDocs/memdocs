---
title: include file
description: include file
author: miepping
ms.service: microsoft-intune
ms.topic: include
ms.date: 01/10/2023
ms.author: miepping
ms.custom: include file
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. -->

# Configure the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices with a Mobile Device Management solution (MDM)

The Microsoft Enterprise SSO plug-in (preview) provides single sign-on (SSO) to apps and websites that use Microsoft Azure Active Directory (Azure AD) for authentication, including Microsoft 365. This plug-in uses the Apple single sign-on app extension framework. It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including any MDM that supports configuring SSO profiles.

Once set up, apps that support the Microsoft Authentication Library (MSAL) automatically take advantage of the Microsoft Enterprise SSO plug-in (preview). Apps that don't support MSAL can be allowed to use the extension. Just add the application bundle ID or prefix to the extension configuration.  

For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property. Be careful with the apps you allow, they'll be able to bypass interactive sign-in prompts for the signed in user.

For more information, see [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#applications-that-dont-use-msal).  

This feature applies to:

- iOS/iPadOS

This article explains how to deploy the Microsoft Enterprise SSO plug-in (preview) for iOS/iPadOS Devices with a generic MDM solution..

> [!IMPORTANT]
> The Microsoft Enterprise SSO plug-in for Apple Devices is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended to use in production. Certain features might not be supported or might have restricted behavior. For more information, see:
>
> - [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)