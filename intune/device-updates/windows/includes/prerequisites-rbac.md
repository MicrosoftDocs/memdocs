---
author: paolomatarazzo
ms.author: paoloma
ms-topic: include
ms.date: 01/08/2026
---

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::

To manage Windows Driver updates, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permissions:

- **Device configurations**:
  - Assign
  - Create
  - Delete
  - View Reports
  - Update
  - Read

You can add the *Device configurations* permission with one or more rights to your own custom RBAC roles or use one the built-in **Policy and Profile manager** role, which includes these rights.

For more information, see [Role-based access control for Microsoft Intune](../../intune-service/fundamentals/role-based-access-control.md).
:::column-end:::
:::row-end:::