---
title: Sign up or sign in to Microsoft Intune
description: How to sign up for a Microsoft Intune subscription or sign in to start with your subscription.
author: paolomatarazzo
ms.author: paoloma
ms.date: 05/21/2025
ms.topic: article
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- get-started
---


# Sign up or sign in to Microsoft Intune

This article can help system administrators sign up for an Intune account. Before you sign up for Intune, determine if your organization already uses [Microsoft Entra ID](/entra/fundamentals/what-is-entra). Microsoft Entra supports work or school accounts that you use with Intune and other Microsoft online services and subscriptions, like Microsoft Azure and Microsoft 365.

- To add an Intune subscription to an Entra tenant, you must use an account that is assigned an Entra ID built-in role with sufficient permissions to add Intune. The initial sign-up page identifies the applicable built-in roles, including:

  - [Billing Administrator](/entra/identity/role-based-access-control/permissions-reference#billing-administrator)
  - [Compliance Administrator](/entra/identity/role-based-access-control/permissions-reference#compliance-administrator)

- If you don't have a Microsoft Entra tenant, then a tenant is created for your organization when you **sign up** for an Intune subscription. You can also sign up for a [trial subscription](try-intune-overview.md).

> [!WARNING]
> You can't combine an existing work or school account after you sign up for a new account.

[!INCLUDE [MFA requirement for admin center](../includes/mfa-console.md)]

## Role-based access controls

Securing access to your organization is a foundational security step. We recommend immediately after you sign up for Intune, plan to use the Microsoft 365 admin center to assign a user account the Entra ID built-in role [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).

The Intune Administrator is a privileged account. The permissions this role includes are applicable only within the scope of Microsoft Intune.

In addition to configuring Intune, an Intune Administrator can use the Intune admin center to assign other user accounts to the specific Intune built-in roles that they require to complete their regular day-to-day administrative tasks. Use of lesser-privileged roles to manage daily tasks follows the principle of *least privileged* access and reduces risk.

For enhanced security, consider enabling [Multi Admin Approval](../fundamentals/multi-admin-approval.md) for role-based access control changes. [!INCLUDE [multi-admin-approval-rbac](../includes/multi-admin-approval-rbac.md)]

For more information, see [Best practices](/entra/identity/role-based-access-control/best-practices) for Microsoft Entra roles, and [Role-based access control](../fundamentals/role-based-access-control.md) (RBAC) with Microsoft Intune.

## How to sign up for Intune

1. In a web browser, open the [Intune set up account page](https://go.microsoft.com/fwlink/?linkid=2019088) and solve the puzzle to confirm you're not a robot.

2. On the *Sign-in details* page, sign in or sign up to manage a new subscription of Intune.

   :::image type="content" source="./media/account-sign-up/account-sign-up-site.png" alt-text="Screenshot of the Microsoft Intune Trial account sign-up web page.":::

## Post sign up considerations

After you sign up for a new subscription, you receive an email message that contains your account information at the email address that you provided during the sign-up process. This email confirms your subscription is active.

After completing the sign-up process, you're directed to the Microsoft 365 admin center to add users and assign them licenses. If you only have cloud-based accounts using your default *onmicrosoft.com* domain name, then you can go ahead and add users and assign licenses at this point. However, if you plan to use your organization's [custom domain name](custom-domain-name-configure.md) or [synchronize user account information](users-add.md#sync-active-directory-and-add-users-to-intune) from on-premises Active Directory, then you can close that browser window.

## Sign in to Microsoft Intune

After signing up for Intune, use any device with a [supported browser](../fundamentals/supported-devices-browsers.md#intune-supported-web-browsers) to sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to administer the service. Administration of Intune requires your account to have sufficient RBAC permissions within Intune for the tasks you want to manage. Initially, you might use an account that is assigned the Microsoft Entra ID built-in role of [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).

The Intune Administrator is a [privileged role](/entra/identity/role-based-access-control/privileged-roles-permissions) with global permissions within Microsoft Intune. With this role a user can configure Intune, add users, create groups of users, and assign the members of those groups Intune RBAC roles that provide them less privileged administrative access for daily use.

Microsoft recommends using roles with the least privilege necessary for daily administration, reducing risk if an account is compromised. To learn more about Intune built-in and custom RBAC roles and for guidance about assigning these roles to users, see [Use role-based access control with Microsoft Intune](../fundamentals/role-based-access-control.md).

### Intune Admin portal URL

Microsoft Intune admin center: `https://intune.microsoft.com`

Intune for Education: `https://intuneeducation.portal.azure.com`

### URLs for Intune services provided by Microsoft 365

Microsoft 365 Business: `https://portal.microsoft.com/adminportal`

Microsoft 365 Mobile Device Management: `https://admin.microsoft.com/adminportal/home#/MifoDevices`

## Related content

- [Configure domains](../fundamentals/custom-domain-name-configure.md)
- [Add users](../fundamentals/users-add.md)
- [Add groups](../fundamentals/groups-add.md)