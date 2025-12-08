---
title: Configure a custom domain name
description: Add a custom domain name for your Microsoft Intune subscription
author: paolomatarazzo
ms.author: paoloma
ms.date: 05/21/2025
ms.topic: article
ms.collection:
- M365-identity-device-management
---

# Configure a custom domain name

This article tells administrators how you can create a DNS CNAME to simplify and customize your sign in experience using Microsoft Intune.

When your organization signs up for a Microsoft cloud-based service like Intune, you're given an initial domain name hosted in Microsoft Entra ID that looks like **your-domain.onmicrosoft.com**. In this example, **your-domain** is the domain name that you chose when you signed up. **onmicrosoft.com** is the suffix assigned to the accounts you add to your subscription. You can configure your organization's custom domain to access Intune instead of the domain name provided with your subscription.

Before you create user accounts or synchronize your on-premises Active Directory, we strongly recommend that you decide whether to use only the *.onmicrosoft.com* domain or to add one or more of your custom domain names. Set up a custom domain before adding users to simplify user management. Setting up a customer domain lets users sign in with the credentials they use to access other domain resources.

When you subscribe to a cloud-based service from Microsoft, your instance of that service becomes a [Microsoft Entra tenant](/entra/fundamentals/whatis). Your Entra tenant provides identity and directory services for Intune and your other cloud-based services. Because the tasks to configure Intune to use your organizations custom domain name are the same as for other services, you can use the information and procedures in [Managing custom domain names in your Microsoft Entra ID](/entra/fundamentals/add-custom-domain).

> [!TIP]
> You can add, verify, or remove custom domain names used with Intune to keep your business identity clear, but you can't rename or remove the initial *onmicrosoft.com* domain name.
>
> To learn more about custom domains, see [Conceptual overview of custom domain names in Microsoft Entra ID](/entra/identity/users/domains-manage).

## Role-based access controls

The following Microsoft Entra built-in RBAC role is the least privileged role that includes sufficient permissions to manage custom domain names:

- [Domain Name Administrator](/entra/identity/role-based-access-control/permissions-reference#domain-name-administrator) - This role provides permissions sufficient to [manage custom domain names](/entra/identity/role-based-access-control/delegate-by-task#custom-domain-names-least-privileged-roles) (read, add, verify, update, and delete). Users assigned this role can also read directory information about users, groups, and applications, as these objects possess domain dependencies.

When working with role-based access controls (RBAC), Microsoft recommends following the principle of least-permissions by using only accounts that have the minimum required permissions for a task, and **limiting** use and assignment of [privileged](/entra/identity/role-based-access-control/privileged-roles-permissions) administrative roles.

## Add and verify your custom domain

Managing custom domains for your Microsoft Entra organization requires use of an account with [sufficient permissions](#role-based-access-controls) in Entra ID. For guidance to add and then verify that your custom domain name is valid in Microsoft Entra, see [Add your custom domain name to your tenant](/entra/fundamentals/add-custom-domain) in the Entra ID documentation.

Learn more [about the initial onmicrosoft.com domain in Microsoft 365](https://support.office.com/article/About-your-initial-onmicrosoft-com-domain-in-Office-365-B9FC3018-8844-43F3-8DB1-1B3A8E9CFD5A).

## Related content

- [Add users](../fundamentals/users-add.md)
- [Add groups](../fundamentals/groups-add.md)

