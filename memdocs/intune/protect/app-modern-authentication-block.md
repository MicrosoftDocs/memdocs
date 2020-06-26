---
# required metadata

title: Block apps with no modern authentication on Intune
titleSuffix: Microsoft Intune
description: Learn about applications and modern authentication (ADAL) using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology:
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
---

# Block apps that don't use modern authentication (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

App-based Conditional Access with app protection policies rely on applications using [modern authentication](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), which is an implementation of OAuth2. Most current Office mobile and desktop applications use modern authentication. However, there are third-party apps and older Office apps that use other authentication methods, like basic authentication and forms-based authentication.

## Block access to apps

To block access to apps that don't use modern authentication, use Intune app protection policies to implement conditional access. For more information, see [App-based Conditional Access with Intune](app-based-conditional-access-intune.md).

## Additional information

For more information about Azure AD Conditional Access, see the following topics:
- [What is Conditional Access in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [How app-based Conditional Access works](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Set up SharePoint Online and Exchange Online for Azure Active Directory Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## Next steps

- [App-based Conditional Access with Intune](app-based-conditional-access-intune.md)
