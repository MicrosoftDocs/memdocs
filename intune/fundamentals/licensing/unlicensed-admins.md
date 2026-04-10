---
title: Enable Unlicensed Administrator Access to Microsoft Intune
description: Learn how to allow administrators to access Microsoft Intune without an Intune license by enabling unlicensed admin access in the admin center.
ms.date: 04/10/2026
ms.topic: how-to
ms.collection:
- M365-identity-device-management
---

# Enable unlicensed administrator access to Microsoft Intune

You can allow administrators to sign in to and manage Microsoft Intune without assigning them an Intune license. When this setting is enabled, it applies to all administrator roles, including Intune administrators and Microsoft Entra administrators. Some related features and services—such as Microsoft Entra ID P1 or P2—may still require the appropriate license.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To enable this setting, use an account assigned the [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator) :::image type="icon" source="../../media/icons/16/privileged-label.svg" border="false"::: Microsoft Entra role. Because this role is privileged, use it only when necessary.
:::column-end:::
:::row-end:::

> [!IMPORTANT]
> - Intune supports up to 350 unlicensed admins per security group and only applies to direct members.
> - It can take up to 48 hours for access changes to take effect.

## Enable the setting

1. In the [Microsoft Intune admin center], select **Tenant administration** > **Roles** > **Administrator Licensing**.
1. Select **Allow access to unlicensed admins**.

   > [!WARNING]
   > You can't undo this setting after selecting **Yes**.

1. Select **Yes** to allow access to unlicensed admins.

   :::image type="content" alt-text="Screenshot of administrator licensing to allow unlicensed admins." source="./images/unlicensed-admins-01.png" :::

After you enable this setting, users who sign in to the Microsoft Intune admin center don't require an Intune license. Roles assigned to users define their scope of access.

## Related content

- [Role-based access control (RBAC) with Microsoft Intune](../../intune-service/fundamentals/role-based-access-control.md)
- [Microsoft Intune licensing](../../fundamentals/licensing/index.md)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[Intune role administrator]: ../../intune-service/fundamentals/role-based-access-control-reference.md
[Custom role]: ../../intune-service/fundamentals/create-custom-role.md
