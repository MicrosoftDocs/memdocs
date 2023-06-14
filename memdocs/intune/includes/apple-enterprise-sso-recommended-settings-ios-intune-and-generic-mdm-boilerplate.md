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

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs for generic MDMs. -->

| Key | Type | Description |
| --- | --- | --- |
| **AppPrefixAllowList** | String | **Recommended value**: `com.apple.` <br/><br/> Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.,com.apple.` to allow all Microsoft and Apple apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
| **browser_sso_interaction_enabled** | Integer | **Recommended value**: `1` <br/><br/> When set to `1`, users can sign in from Safari browser, and from apps that don't support MSAL. Enabling this setting allows users to bootstrap the extension from Safari or other apps.|
| **disable_explicit_app_prompt** | Integer | **Recommended value**: `1` <br/><br/> Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these prompts. |

> [!TIP]
> For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).
