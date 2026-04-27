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
> To manage this feature, use an account with at least one of the following roles:
>
> - [Policy and Profile manager][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The **Device configurations** permissions **Assign**,**Create**,**Delete**,**View Reports**,**Update**, and **Read**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
>
> To view the reports for this feature, use an account with at least one of the following roles:
>
> - [Endpoint Security Manager][INT-R2]
> - [Read Only Operator][INT-R3]
> - [Help Desk Operator][INT-R4]
> - [Custom role][INT-RC] with the **Managed devices**/**View Reports** permission.
:::column-end:::
:::row-end:::

<!-- role links -->

[INT-R1]: ../../../fundamentals/role-based-access-control/ref-built-in-roles.md#policy-and-profile-manager
[INT-R2]: ../../../fundamentals/role-based-access-control/ref-built-in-roles.md#endpoint-security-manager
[INT-R3]: ../../../fundamentals/role-based-access-control/ref-built-in-roles.md#read-only-operator
[INT-R4]: ../../../fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[INT-RC]: ../../../fundamentals/role-based-access-control/create-custom-role.md