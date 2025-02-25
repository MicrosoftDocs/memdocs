---
# required metadata

title: Block apps with no modern authentication on Intune
titleSuffix: Microsoft Intune
description: Learn about applications and modern authentication (MSAL) using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/28/2024
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: conceptual
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-device-compliance
---

# Block apps that don't use modern authentication (MSAL)

App-based Conditional Access with app protection policies rely on applications using [modern authentication](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), which is an implementation of OAuth2. Most current Office mobile and desktop applications use modern authentication. However, there are third-party apps and older Office apps that use other authentication methods, like basic authentication and forms-based authentication.

## Block access to apps

To block access to apps that don't use modern authentication, use Intune app protection policies to implement Conditional Access. For more information, see [App-based Conditional Access with Intune](app-based-conditional-access-intune.md).

## Additional information

For more information about Microsoft Entra Conditional Access, see the following topics:
- [What is Conditional Access in Microsoft Entra ID?](/azure/active-directory/conditional-access/overview)
- [How app-based Conditional Access works](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Set up SharePoint Online and Exchange Online for Microsoft Entra Conditional Access](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## Next steps

- [App-based Conditional Access with Intune](app-based-conditional-access-intune.md)
