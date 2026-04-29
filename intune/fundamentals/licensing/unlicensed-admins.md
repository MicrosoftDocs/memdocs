---
title: Unlicensed administrator access to Microsoft Intune
description: Learn about unlicensed administrator access in Microsoft Intune, including default behavior for newer tenants and how to enable it for older tenants.
ms.date: 04/29/2026
ms.topic: how-to
ms.collection:
- M365-identity-device-management
---

# Unlicensed administrator access to Microsoft Intune

Administrators can sign in to and manage Microsoft Intune without an assigned Intune license. This access is enabled by default for tenants created after July 2021 and applies to all administrator roles, including Intune administrators and Microsoft Entra administrators. Tenants created before July 2021 can enable this access manually.

Unlicensed admin access grants sign-in and management access to the Microsoft Intune admin center. It doesn't replace license requirements for other features and services. For example, features that depend on Microsoft Entra ID P1 or P2 still require the appropriate license.

Whether you need to enable this setting depends on when your tenant was created:

- **Tenants created after July 2021**: Unlicensed administrator access is supported by default. No action is required.
- **Tenants created before July 2021**: Administrators require an Intune license unless the **Allow access to unlicensed admins** setting is enabled. This setting can't be undone after it's turned on.

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
> - Intune supports up to 350 unlicensed admins per security group. If more than 350 administrators are needed for a role assignment, you can use multiple security groups.
> - Unlicensed admin access only applies to direct members of a security group. Members of nested security groups aren't included and still require an Intune license.
> - It can take up to 48 hours for access changes to take effect.

## Enable the setting for pre-July 2021 tenants

Tenants created after July 2021 already have unlicensed admin access enabled by default. The following steps apply only to tenants created before July 2021.

1. In the [Microsoft Intune admin center], select **Tenant administration** > **Roles** > **Administrator Licensing**.
1. Select **Allow access to unlicensed admins**.

   > [!WARNING]
   > You can't undo this setting after selecting **Yes**.

1. Select **Yes** to allow access to unlicensed admins.

   :::image type="content" alt-text="Screenshot of administrator licensing to allow unlicensed admins." source="./media/unlicensed-admins/unlicensed-admins-01.png" :::

After you enable this setting, users who sign in to the Microsoft Intune admin center don't require an Intune license. Roles assigned to users define their scope of access.

## Related content

- [Role-based access control (RBAC) with Microsoft Intune](../../fundamentals/role-based-access-control/overview.md)
- [Microsoft Intune licensing](../../fundamentals/licensing/index.md)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[Intune role administrator]: ../../fundamentals/role-based-access-control-reference.md
[Custom role]: ../../fundamentals/create-custom-role.md
