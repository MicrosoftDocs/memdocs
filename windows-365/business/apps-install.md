---
title: Users installing apps on Windows 365 Business Cloud PCs
description: Learn about users installing apps on Windows 365 Business Cloud PCs.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 02/12/2022
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

Some apps may require that the user have administrator privileges. To change a user's role/privileges, see [Remote management actions](remotely-manage-business-cloud-pcs.md#remote-management-actions).

> [!IMPORTANT]
> If a user tries to use a Microsoft 365 Business Standard license on their Cloud PC, they might see the following error: "Account Issue: The products we found in your account cannot be used to activate Office in shared computer scenarios." In this scenario, the user must uninstall the version of Office installed on their Cloud PC and install a new copy from Office.com.

## Sending outbound email messages using port 25 is not supported

Sending outbound email messages directly on port 25 from a Windows 365 Business Cloud PC is not supported. Communication over port TCP/25 is blocked at the Windows 365 Business network layer for security reasons. If your email service uses Simple Mail Transfer Protocol (SMTP) for your email client application, you can use their web interface, if available. Or you can ask your email service provider for help to configure their email client app to use secure SMTP over Transport Layer Security (TLS), which uses a different port.

## Next steps

[Manage your Cloud PCs](device-management.md)
