---
# required metadata
title: Remotely manage Windows 365 Business Cloud PCs
titleSuffix:
description: Learn how to remotely manage Windows 365 Business Cloud PCs
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/27/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Remotely manage Windows 365 Business Cloud PCs

You can remotely manage Windows 365 Business Cloud PCs by using the Microsoft 365 admin center or windows365.microsoft.com. Each supports several remote management [actions](#remote-management-actions).

## Permissions

To use these remote actions, you must have the appropriate Microsoft Entra role-based access roles.

| Admin actions | Roles required for windows365.microsoft.com | Roles required for Microsoft 365 admin center |
| --- | --- | --- |
| Windows 365 Business remote management actions (like reset, restart, and so on) | [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference#windows-365-administrator) | [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference#windows-365-administrator) and [Global Reader](/azure/active-directory/roles/permissions-reference#global-reader) (this grants access to the admin center) |
| License administration (assignment and removal of licenses from a user) | [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference#windows-365-administrator) and [License Administrator](/azure/active-directory/roles/permissions-reference#license-administrator) | [License Administrator](/azure/active-directory/roles/permissions-reference#license-administrator) |

## Remotely manage Cloud PCs on windows365.microsoft.com

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com).
2. Select **Your organization’s Cloud PCs**.
3. Select the user whose Cloud PC you want to manage.
4. Select **Devices**.
5. Select the Cloud PC you want to manage.
6. Select the action that you want to perform.

## Remotely manage Cloud PCs by using the Microsoft 365 admin center simplified view

1. Sign in to [Microsoft 365 admin center](https://admin.microsoft.com).
2. Select the user whose Cloud PC you want to manage.
3. Select **Devices**.
4. Select the Cloud PC you want to manage.
5. Select the action that you want to perform.

## Remotely manage Cloud PCs by using the Microsoft 365 admin center

1. Sign in to [Microsoft 365 admin center](https://admin.microsoft.com).
2. In the left navigation, select **Users** -> **Active users**.
3. Select the user whose Cloud PC you want to manage.
4. Select **Devices**.
5. Select the Cloud PC you want to manage.
6. Select the action that you want to perform.

## Remote management actions

The following remote actions are supported on windows365.microsoft.com and the Microsoft 365 admin center:

**Change account type**: Change the role of a user on their Cloud PC. Options include Standard User and Local Administrator. For the role change to take effect, the user must sign out of Windows on their Cloud PC and sign back in. Alternatively, the admin can remotely restart the Cloud PC, but the user may lose any unsaved data.

**Rename**: Change the Cloud PC name that users see on windows365.microsoft.com.

**Reset**: If a user is having trouble with their Cloud PC, admins can reset the Cloud PC for them. This action:

- Reinstalls Windows (with the option to choose between Windows 11 and Windows 10).
- Removes all apps and locally stored files.
- Removes changes made to settings.

For Windows 365 Business users, it’s not possible to upgrade their Windows 10 Cloud PC to Windows 11 and retain their data and settings. Instead, to upgrade them to a Windows 11 Cloud PC, you must use the **Reset** remote action and choose Windows 11. Reset is a destructive action that removes all the user's data and settings from their Cloud PC.

**Resize**: The Resize remote action, which preserves user and disk data, lets you:

- Upgrade the RAM, CPU, and storage size of a Cloud PC.
- These operations don't require reprovisioning of the Cloud PC.

You might consider resizing a Cloud PC when a user needs:

- Higher RAM and VCPU cores to run CPU intensive applications.
- More disk space for file storing.

Resizing automatically disconnects the user from their session and any unsaved work might be lost. Therefore, it's best to coordinate any resizing with the user before you begin. Contact your end users and have them save their work and sign out before you begin resizing.

Resizing 16vCPU isn't supported. 

**Restart**: Restart a user’s Cloud PC on their behalf.

## Grant remote action permissions to another user

If you want to grant remote action permissions to another user, you can assign the Windows 365 Administrator role to them. This role is scoped to performing actions that can alter the state of a Cloud PC. This role can't manage users, licenses, or billing.

To assign a Windows 365 Administrator role to a user:

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com).
2. Select **Your organization’s Cloud PCs**.
3. Select the user whose Cloud PC you want to manage.
4. Select **Manage roles** > **Admin center access** > **Show all by category**.
5. Scroll down to the **Devices** section.
6. Select **Windows 365 Administrator** > **Save changes**.

You can also assign the Windows 365 Administrator role through the Microsoft 365 Admin Center and Microsoft Entra ID.

## Next steps

You can manage users and Cloud PCs in other ways. For more information, see [Managing Cloud PCs](get-started-windows-365-business.md#).
