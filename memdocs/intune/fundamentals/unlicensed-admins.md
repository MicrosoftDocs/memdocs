---
# required metadata

title: Unlicensed admins in Microsoft Intune
description: Learn how to give unlicensed admins permissions to access Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---


# Unlicensed admins

You can grant Intune/Microsoft Endpoint Manager admin center access to admins without Intune licenses.

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **Administrator licensing**.
2. Choose **Allow access to unlicensed admins** > **Yes**.
    >[!WARNING]
    >You can’t undo this setting after clicking **Yes**.

3. From now on, users who sign in to the Microsoft Endpoint Manager admin center don’t require an Intune license. Their scope of access is defined by the roles assigned to them.

Intune supports up to 350 unlicensed admins per security group and only applies to direct members. Admins above this limit will experience unpredictable behavior.




