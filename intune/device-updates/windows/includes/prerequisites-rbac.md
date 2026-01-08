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
:::column-end:::
:::row-end:::

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#policy-and-profile-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role