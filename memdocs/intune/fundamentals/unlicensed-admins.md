---
# required metadata

title: Unlicensed admins in Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: This article describes how to give unlicensed admins permissions to access Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 09/29/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata
# CustomerIntent: As an  IT admin, I want to give other administrators access to Microsoft Intune without them requiring an Intune license so that right admins have the correct access. 

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---

# Unlicensed admins

You can give administrators access to Microsoft Intune without them requiring an Intune license. This feature applies to any administrator, including Intune administrators, global administrators, Microsoft Entra administrators, and so on. Other features or services, such as those in Microsoft Entra ID P1 or P2, may require a license for the administrator.

The Unlicensed admins option has been enabled by default on all accounts created after the 2006 release.

## Allow access

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **Administrator Licensing**.
2. Select **Allow access to unlicensed admins** > **Yes**.

    > [!WARNING]
    > You can't undo this setting after clicking **Yes**.

3. From now on, users who sign in to the Microsoft Intune admin center don't require an Intune license. Their scope of access is defined by the roles assigned to them.

Intune supports up to 350 unlicensed admins per security group, and only applies to direct members. Admins above this limit will experience unpredictable behavior.

It can take up to 48 hours for access changes to take effect.

## Next step

[Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)

[Microsoft Intune licensing](licenses.md)
