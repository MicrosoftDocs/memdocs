---
title : Set up Intune
description: Step 1 for deploying or setting up Intune. The starting point is to review supported configurations, sign up for the trial, configure the custom domain name, add users and groups to Intune, assign licenses to users, manage roles, grant admin permissions, and set the MDM authority.
author: paolomatarazzo
ms.author: paoloma
ms.date: 03/18/2026
ms.topic: install-set-up-deploy
ms.collection:
- M365-identity-device-management
- highpri
- ContentFreshnessFY24
---

# Step 1: Set up Microsoft Intune

The first step when deploying Microsoft Intune is to set up your Intune environment.

:::image type="content" source="./media/deployment-plan-setup/deployment-plan-setup-intune.png" alt-text="Diagram that shows getting started with Intune with step 1, which is setting up Microsoft Intune.":::

This article takes you through each step in the process of setting up Microsoft Intune. It also provides the choices and considerations you need to make when setting up an endpoint-management solution such as Intune.

The purpose of this article is to help you get a better understanding of Intune's supported configurations. After reviewing the article, you should be able to sign up for the [Microsoft Intune free trial](try-intune-overview.md), add end users, define user groups, assign licenses to users, and set up the other needed settings to begin using Microsoft Intune. All the steps provided in the article help you add and manage devices and apps by using Intune.

## Prerequisites

Before you begin setting up Microsoft Intune, review the [Planning guide](intune-planning-guide.md). The planning guide helps you plan your move or migration to Intune.

The planning guide also helps you address these areas:

- What are some of the common objectives for device management?
- How to address potential licensing needs?
- How to handle personally owned devices?
- How to review current policies and infrastructure?
- What are some examples of creating a rollout plan?

## 1 - Review the Supported Configurations

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with supported configurations**

Before you begin setting up Microsoft Intune, you should:

- Review the device platforms and operating systems that Intune supports.
- Review which web browsers are supported when accessing Intune using Microsoft Intune admin center.
- Get familiar with the network bandwidth requirements to perform installations and updates using Intune.
- Review [Network endpoints](intune-endpoints.md) for IP addresses and port settings needed for proxy settings in your Microsoft Intune deployments.

For guidance and need-to-know information, see [Supported configurations](supported-devices-browsers.md).

> [!TIP]
> By default, all device platforms can enroll in Intune. If you want to prevent specific platforms, create a restriction. For more information, see [Create a device platform restriction](../enrollment/create-device-platform-restrictions.md).

## 2 - Sign up for Microsoft Intune

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with sign up, or sign in to Intune**

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

Before you sign up for Intune, determine whether you already have a Microsoft Online Services account, Enterprise Agreement, or equivalent volume licensing agreement. A Microsoft volume licensing agreement or other Microsoft cloud services subscription, such as Microsoft 365, usually includes a work or school account.

If you already have a work or school account, **sign in** with that account and add Intune to your subscription. Otherwise, you can **sign up** for a new account to use Intune for your organization.

For guidance, see [Sign in to Intune](account-sign-up.md).

## 3 - Configure a custom domain name for your Intune tenant

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with configuring a custom domain name for your Intune tenant**

When your organization signs up for Microsoft Intune, you get an initial domain name hosted in Microsoft Entra ID that looks like *your-domain.onmicrosoft.com*.

Microsoft assigns the *onmicrosoft.com* suffix to all accounts added to subscriptions.

You can **optionally** configure your organization's custom domain in Intune, such as `contoso.com`. If you don't add your domain account, then for example, `contoso.onmicrosoft.com` might be used.

- Set DNS registration to connect your company's domain name with Intune. When you connect your company's domain name with Intune, users experience a familiar domain when connecting to Intune and using resources.

- If you're simply evaluating Intune using the free trial, you can skip this step.

- If you're moving to Microsoft 365 from an Office 365 subscription, your domain might already be in Microsoft Entra ID. Intune uses the same Microsoft Entra ID, and can use your existing domain.

For guidance, see [Configure domain name](custom-domain-name-configure.md).

## 4 - Add users to Intune

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with adding users to Intune**

Users are stored in Microsoft Entra ID, which is also included with Microsoft 365. Microsoft Entra ID controls access to resources, and authenticates users.

You can add users or connect Active Directory to sync with Intune. This step is **required** unless your devices are "userless" kiosk devices.

For guidance, see [Add users](users-add.md).

Each person in your organization needs a user account before they can sign in and access Microsoft Intune. To create user accounts, add users to Intune. Once added, you can grant permissions and assign licenses to users. Later, you can assign different types of policies to users to help and protect them.

As an administrator, you can add users individually or in bulk to Intune.

You must be a Microsoft Entra [License Administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator) or [User Administrator](/entra/identity/role-based-access-control/permissions-reference#user-administrator) to add users to Intune.

## 5 - Create groups in Intune

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with adding groups to Intune**

Add groups to assign apps, settings, and other resources. For guidance, see [Add groups](groups-add.md).

Intune uses Microsoft Entra groups to organize and manage devices and users. As an Intune admin, you can set up groups to suit your organizational needs. For instance, you can create groups to organize users or devices by geographic location, department, or hardware characteristics. Also, you can use groups to manage tasks at scale. For example, you can set policies for many users or deploy apps to a set of devices based on groups.

## 6 - Manage licenses

Intune is available with different subscriptions, including as a stand-alone service. Determine the licensed services your organization needs and then continue to assign each user an Intune license before users can enroll their devices in Intune.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Determine your license needs**

Microsoft Intune is available for different organization sizes and needs. It offers a simple-to-use management experience for schools and small businesses, and more advanced functionality required by enterprise customers. An admin must have a license assigned to them to administer Intune (unless you select to allow unlicensed admins).

For guidance, see [Microsoft Intune licensing](../../fundamentals/licensing/index.md).

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with assigning licenses to users**

Whether you add users one at a time or all at once, you must assign each user an Intune license before users can enroll their devices in Intune. The [Microsoft Intune's free trial](try-intune-overview.md) provides 25 Intune licenses. For a list of licenses, see Licenses that include Intune.
Give users permission to use Intune. Each user or userless device requires an Intune license to access the service.

For guidance, see [Assign licenses](../../fundamentals/licensing/assign-licenses.md).

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Unlicensed admins**

You can give administrators access to Microsoft Intune without them requiring an Intune license. This feature applies to any administrator, including Intune administrators, Microsoft Entra administrators, and so on.

For guidance, see [Unlicensed admins](../../fundamentals/licensing/unlicensed-admins.md).

## 7 - Manage roles and grant admin permissions for Intune

After you add users to your Intune tenant, create your administrative team.

Microsoft Intune uses role-based access control (RBAC) to manage administrative access. It includes built-in roles that have predefined permissions to complete admin-specific tasks, like managing apps and creating policies. For more granular control, you can create custom roles that only include the exact set of permissions you need.

Scope tags work with roles to limit which Intune objects, like devices, policies, and apps, are visible to an admin. By using roles and scope tags together, you can implement least-privilege access and support distributed IT administration across teams or regions.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with managing roles**

1. Assign the built-in roles to the admins based on their responsibilities. For example, assign the **Policy and Profile manager** role to the admins that create and manage enrollment policies. Role assignments determine what admins can see and modify in Intune.

    For guidance, see:

    - [Role-based access control (RBAC) with Intune](role-based-access-control.md)
    - [Built-in role permissions for Intune](role-based-access-control-reference.md)
    - [Assign a role in Intune](assign-role.md)

2. Create your own custom roles with the exact set of permissions you need, and then assign to the admins based on their responsibilities. Custom roles let you define a precise set of permissions when built-in roles don't meet your requirements, or you want to implement least-privilege access. For example, you can create a custom role that only has permissions to create and update device compliance policies.

    For guidance, see:

    - [Create a custom role in Intune](create-custom-role.md)
    - [Built-in role permissions for Intune](role-based-access-control-reference.md)
    - [Assign a role in Intune](assign-role.md)

3. Use scope tags to limit visibility of Intune objects. Scope tags control which objects admins can see. Roles control what actions they can take on those objects. Using RBAC together with scope tags helps ensure admins only have access to the resources they're responsible for.

    For guidance, see [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md).

4. Configure Multi Admin Approval. To help protect against a compromised administrative account, this feature requires that a second administrative account must approve a change before the change is applied. It adds an extra layer of security by ensuring that high-impact changes, like wiping or deleting devices, require approval from multiple administrators.

    For guidance, see [Configure Multi Admin Approval](multi-admin-approval.md).

## 8 - Set the mobile device management authority

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with MDM authority**

The mobile device management (MDM) authority setting determines how you manage your devices. By default, the Intune free trial sets your MDM authority to Intune. As an IT admin, you must set an MDM authority before users can enroll devices for management. When you set the MDM authority, you can start enrolling devices.

If you're changing your tenant to support Intune, change your MDM authority configuration.

For guidance, see [Set the mobile device management authority](mdm-authority-set.md).

## 9 - Customize the Intune company portal

The Company Portal apps, Company Portal website, and Intune app on Android are where users access company data and can do common tasks. Common tasks include enrolling devices, installing apps, and locating information (such as for assistance from your IT department).

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Get started with configuring the company portal**

Customize the Intune Company Portal that users use to enroll devices and install apps. These settings appear in both the Company Portal app and the Intune Company Portal website. You can also customize the Company Portal app so it includes your organization details.

For guidance, see [Configure the company portal](../apps/company-portal-app.md).

## Follow the minimum recommended baseline policies

This article is part of a five-step series that describes how to deploy Microsoft Intune. The series includes the following articles, in order:

1. 🡺 **Set up Microsoft Intune** (this article)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Create compliance policies](deployment-plan-compliance-policies.md)
4. [Configure device features and settings](deployment-plan-configuration-profile.md)
5. [Enroll devices](deployment-guide-enroll.md)
