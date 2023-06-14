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
| **AppPrefixAllowList** | String |  **Recommended value**: `com.microsoft.,com.apple.,com.jamf.,com.jamfsoftware.` <br/><br/> Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.,com.apple.,com.jamf.,com.jamfsoftware.` to allow all Microsoft, Apple, and Jamf Pro apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
| **disable_explicit_app_prompt** | Integer | **Recommended value**: `1` <br/><br/> Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these prompts. |

> [!TIP]
> For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).
