---
title: Unlicensed admins in Microsoft Intune | Microsoft Docs
description: This article describes how to give unlicensed admins permissions to access Intune.
author: BrenDuns
ms.author: brenduns
ms.date: 05/09/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
---

# Unlicensed admins

You can give administrators access to Microsoft Intune without them requiring an Intune license. This feature applies to any administrator, including Intune Administrators, Microsoft Entra administrators, and so on. Other features or services, such as those in Microsoft Entra ID P1 or P2, might require a license for the administrator.

## Allow access

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **Administrator Licensing**.
2. Select **Allow access to unlicensed admins**.

    > [!WARNING]
    > You can't undo this setting after clicking **Yes**.

3. Select **Yes** to allow access to unlicensed admins.

    :::image type="content" alt-text="Screenshot of administrator licensing to allow unlicensed admins." source="./media/unlicensed-admins/unlicensed-admins-01.png" :::

4. From now on, users who sign in to the Microsoft Intune admin center don't require an Intune license. Roles assigned to users define their scope of access.

   Intune supports up to 350 unlicensed admins per security group, and only applies to direct members. Admins above this limit experience unpredictable behavior.

   It can take up to 48 hours for access changes to take effect.

## Next step

[Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)

[Microsoft Intune licensing](licenses.md)
