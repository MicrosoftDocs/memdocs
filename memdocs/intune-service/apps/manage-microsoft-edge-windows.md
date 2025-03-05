---
# required metadata

title: Configure Microsoft Edge for Windows with Intune
titleSuffix: 
description: Use Intune configuration policies with Edge for Windows to ensure corporate websites are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Windows
- highpri
ms.custom: intune-azure
---

# Configure Microsoft Edge for Windows with Intune

Edge for Windows is designed to enable users to browse the web and supports multi-identity. Users can add a work account, as well as a personal account, for browsing. There is complete separation between the two identities, which is also offered in other Microsoft mobile apps.

This feature applies to:
- Applies to Windows 11 22H2

> [!NOTE]
> Edge for Windows doesn't consume settings that users set for the native browser on their devices, because Edge for Windows can't access these settings.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features.

## Add an app configuration policy for Edge as a managed app on Windows devices

To create a **Managed apps** app configuration policy for Microsoft Edge on Windows, see [Add an app configuration policy for managed apps on Windows devices](../apps/app-configuration-policies-managed-app.md#add-an-app-configuration-policy-for-managed-apps-on-windows-devices). Select the **Microsoft Edge for Windows** application when creating the app configuration policy. After the configuration is created, you can assign the policy to groups of users.

> [!NOTE]
> For more information about policies for Microsoft Edge for Windows, see [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
