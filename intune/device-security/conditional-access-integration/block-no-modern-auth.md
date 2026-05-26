---
title: Block Apps with No Modern Authentication on Intune
description: Learn about applications and modern authentication (MSAL) using Microsoft Intune.
ms.date: 03/28/2024
author: nicholasswhite
ms.author: nwhite
ms.topic: article
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
- sub-device-compliance
---

# Block Apps That Don't Use Modern Authentication (MSAL)

App-based Conditional Access with app protection policies rely on applications using [modern authentication](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), which is an implementation of OAuth2. Most current Office mobile and desktop applications use modern authentication. However, there are third-party apps and older Office apps that use other authentication methods, like basic authentication and forms-based authentication.

## Block access to apps

To block access to apps that don't use modern authentication, use Intune app protection policies to implement Conditional Access. For more information, see [App-based Conditional Access with Intune](./app-based-policies.md).

## Additional information

For more information about Microsoft Entra Conditional Access, see the following topics:
- [What is Conditional Access in Microsoft Entra ID?](/entra/identity/conditional-access/overview)
- [How app-based Conditional Access works](./app-based-policies.md#how-app-based-conditional-access-works)

## Next steps

- [App-based Conditional Access with Intune](./app-based-policies.md)
