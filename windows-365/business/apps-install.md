---
title: Users installing apps on Windows 365 Business Cloud PCs
description: Learn about users installing apps on Windows 365 Business Cloud PCs.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 01/12/2022
audience: Admin
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Install apps

Users can install apps on their Cloud PC as they would normally in Windows by either downloading them from the application’s website or by downloading them from the Microsoft Store.

To download an app from the Microsoft store:

1. On the Cloud PC, open the Microsoft Store app.
2. Search or browse for an app.
3. On the app's page, choose **Get**.
4. After the download completes, open the app.

Some apps may require that the user have administrator privileges. To change a user's role/privileges, see [Remote management actions](remotely-manage-business-cloud-pcs.md#remote-management-actions).

## Default apps

The following apps are pre-installed on Windows 365 Business Cloud PCs when they're created:

- [Microsoft 365 Apps for Enterprise](/mem/intune/apps/apps-add-office365) (formerly Office 365 Pro Plus)
- Microsoft Teams
- Microsoft OneDrive
- [Microsoft Edge](/mem/intune/apps/apps-windows-edge)

> [!IMPORTANT]
> If a user tries to use a Microsoft 365 Business Standard license on their Cloud PC, they might see the following error: "Account Issue: The products we found in your account cannot be used to activate Office in shared computer scenarios." In this scenario, the user must uninstall the version of Office installed on their Cloud PC and install a new copy from Office.com.

## Next steps

[Users installing apps](apps-install.md)

[Manage your Cloud PCs](device-management.md)
