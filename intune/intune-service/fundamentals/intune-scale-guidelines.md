---
title: Distributed IT with multiple admins
description: Learn about scaling guidelines for Microsoft Intune when you have a large number of local admins who need to manage their own users/devices and policies within the same tenant. Use Microsoft Intune's Role Based Access Control to manage access.

author: brenduns
ms.author: brenduns
ms.date: 05/28/2025
ms.topic: article
ms.reviewer: dagerrit
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Distributed IT environment with many admins in the same Microsoft Intune tenant

Many organizations use a distributed IT environment where they have a single Microsoft Intune tenant with multiple local admins.
This article describes one way to scale Microsoft Intune to support multiple local admins who manage their own users, devices, and create their own policies all within a single Microsoft Intune tenant.

There's no right or wrong answer on how many admins you should have in your tenant. The article focuses on tenants that have many local administrators.

Distributed IT is needed in organizations where a large number of local admins connect to a single Intune tenant. For example, some school systems are organized so that you have a local admin for every school in the system or region. Sometimes, this distributed environment could include over 15 different local admins who roll up to the same central system or Microsoft Intune tenant.

Each local admin can set up groups to suit their local organizational needs. The local admin typically creates groups and organizes multiple users or devices by geographic location, department, or hardware characteristics. The local admins also use these groups to manage tasks at scale. For example, the local admins can set policies for many users or deploy apps to a set of devices.

## Terms used in this article

- **Least privilege**: Securing access to your organization is an essential security step. Intune uses role-based access controls (RBAC) to assign administrative users permissions within Intune to administer different tasks. With the principle of *least privilege* access, your admins can perform their assigned tasks on only those users and devices that they should be empowered to manage.

- **Central team**: The Central team or group includes the primary admins in your tenant. These admins can oversee all the local admins and can provide guidance to the local admins.

- **Local admins**: The local admins are local and focus on policies and profiles for their specific locations; schools, hospitals, and so on.

## Role-based access control

Securing access to your organization is an essential security step. Intune uses [role-based access controls](../fundamentals/role-based-access-control.md) to grant granular permissions to your admins to control who has access to your organization's resources, and what they can do with those resources. By assigning Intune RBAC roles and adhering to principles of least privilege access, your admins can perform their assigned tasks on only those users and devices that they should be empowered to manage.

The following sections briefly describe different models with guidelines under each model for managing policies, profiles, and apps between the *Central team* and the *local admins*. The models are:

- Partial delegation model
- Full delegation model
- Central model
- Devolved model
- Hybrid model

### Partial delegation model

The partial delegation model proposes the following guidelines for policy management between the Central team and the local admins.

✔️ **Permissions**

- Create, update and delete permissions for policies, enrollment profiles, and apps should be held by the Central team.
- Grant only read and assign permissions to the local admins.

✔️ **Reuse**

- Commonly configured policies, enrollment profiles, and apps should be made available to the local admins to reuse, as much as possible.
- Microsoft Intune uses many common configurations that fall into a few categories. Review the recommendations listed for [App Protection Policies](../apps/app-protection-framework.md#level-1-enterprise-basic-data-protection).
- As local admins onboard, they should review the existing policies and reuse them as needed.

✔️ **Exceptions**

- The Central team can create new policies, enrollment profiles, and apps as exceptions when needed on behalf of the local admins. Usually, these exceptions include any type of profile that requires unique parameters.

A partial delegation model is proposed in these two areas:

**Group and assignment guidelines for local admins**: What are some of the best practices for local admins to adopt while organizing groups for device management through Microsoft Intune? To find out, see the [Intune grouping, targeting, and filtering: Recommendations for best performance - Microsoft Tech Community](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-grouping-targeting-and-filtering-recommendations-for-best-performance/2983058) blog.

**Feature specific guidelines**: How are policies/profiles/apps managed between a central authority and the local admins with specific permissions for the different features. For more information, see [Feature specific guidelines](#feature-specific-guidelines) in this article.

### Full delegation model

The full delegation model proposes the following guidelines for policy management between the Central team and the local admins.

- Each local admin should have their own scope tag to separate each object that they fully manage.
- When the local admin doesn't need to create, update or delete, then grant the local admin a role with read and assign permissions and avoid assigning any other role with full permission to them. With this approach, you can avoid combining permissions across scope tags.
- Sometimes the local admins might need to create their own policies, profiles, and apps while sharing some common policies, profiles, and apps. In such cases, create a special group and assign the common policies, profiles, and apps, to this group. This group shouldn't be included in the [Scope (Group)](../fundamentals/role-based-access-control.md#about-intune-role-assignments) of an Intune RBAC role assignment for any local admin. This approach prevents the *create*, *update*, and *delete* permissions assigned to the local admins from applying to these common policies, profiles, and apps.


### Central model

In the central model, a single local admin team (parent) manages multiple child orgs. Factors such as geography, business unit, or size can be used to group child orgs.

- There's only one scope tag used to cover all the managed local admins.

- If possible, the local admin team should standardize assignments across local admins and place all their devices into a single Microsoft Entra group for assignment. When it isn't possible to create a single Microsoft Entra group, the local admin team can create different Microsoft Entra groups to make different assignments.

- If a different local admin team manages or moves an org, the following steps must be taken:

  - All the org's devices and users must be extracted from common Microsoft Entra groups in scope of the original local admin team.

  - All policies/apps/profiles assigned uniquely for that org must have their scope tag updated for the new local admin team.

### Devolved model

In the devolved model, multiple local admins (children) are managed both by their dedicated local admin and also overseen by an intermediary local admin team. Both the parent and children admins have their own scope tags to represent management boundaries.

- If there are fewer than 50 children admins, the intermediate local admin team might be granted access by assigning all the children's scope tags to the intermediate local admin teams RBAC role assignment.
- If there are more than 50 children admins, the intermediate local admin team should be granted their own scope tag to represent the entire collection of children admins they oversee.
- Newly created policies under the children admin's scope tags must have the intermediate tag added by a user with an appropriate role to prevent the intermediate local admin team from losing visibility.

### Hybrid model

In the hybrid model, the same parent admin is used in both Central and Devolved model at the same time.
There are no special recommendations for this model.

## Feature specific guidelines

Depending on the business requirements for each feature, guidelines provided in this section can recommend that you create policies per local admin and possibly delegate the permissions needed for creating objects to the local administrators.

> [!NOTE]
> The guidance provided in this section doesn't address every feature, but only covers those areas for which we have special instructions.

### App protection policy

App protection policies are rules that ensure an organization's data remains safe or contained in a managed app. For more information, see [App protection policies](../apps/app-protection-framework.md).

The guidelines for App protection policies are split across the Central team and the local admins as follows:

#### Central team - Tasks

- Review the security and business needs across the organization and generate a set of common App protection policies for local admins.
- Review the recommendations listed to identify what security controls are appropriate before creating any App protection policies.
- Have an established method for local admins to request customized App protection policies, if necessary, for specific business needs where the business requirements can't be achieved with the existing common policies.
- For specific recommendations about each configuration level and the minimum apps that must be protected, see [Data protection framework using App protection policies](../apps/app-protection-framework.md).

#### Local admins - Permissions and Tasks

- Provide local admins read and assign permissions, but not create, update, or delete permissions on Managed Apps. This configuration of permissions prevents them from creating their own App protection policies.
- Provide read and assign permissions for application configuration policy assignment to their apps.
- Provide read and assign permissions only when there are different protection policies for managed devices and unmanaged devices. If the Central team chooses to offer only one policy for both, then application configuration policy isn't needed.
- If application configuration policy is used, we recommend that you assign the application configuration policy to all App instances without exception.
- Choose from common App protection policies. Local admins can request the Central team to create custom app protection policies as an exception, and only if necessary.
- For more information, see [App protection policies](../apps/app-protection-framework.md).

### Compliance policy

Compliance policies in Intune define the rules and settings that users and devices must meet to be compliant. Compliance can be required before a device can be used to access your organizations resources. For more information on compliance policies, see [Use compliance policies to set rules for devices you manage with Intune](../protect/device-compliance-get-started.md).

#### Central team

The Central team should create common compliance policies for local admins to choose from and only, if necessary, create exception policies. For more information, see [Use compliance policies to set rules for devices you manage with Intune](../protect/device-compliance-get-started.md).
Creating policies includes the creation of custom compliance policy scripts because they're subject to the same scale as normal compliance policy.

For more information on how to create a compliance policy, see [Create a compliance policy in Microsoft Intune](../protect/create-compliance-policy.md#create-the-policy).

#### Local admins

Provide local admins with read and assign permissions, but not create, update, or delete permissions on Compliance policies. The read and assign permissions allow them to choose from the common compliance policies created by the central team and assign them to their users and devices.

### Device configuration

In this section:

- Device restrictions and general configuration
- Resource access
- Windows update rings
- Feature updates
- Quality updates

#### Device restrictions and general configuration

- Grant local admins permission to create, update, delete within their own scope.

- Use the **Settings Catalog** and **security baselines** to the maximum possible extent, instead of profiles created in the Configuration profiles list, to mitigate scale in the Microsoft Intune admin center.

- In general, the central team should try to centrally monitor the content of configurations and replace duplicate profiles where possible with a shared profile.

#### Resource access

The [Full delegation model](#full-delegation-model) is recommended.

#### Windows update rings

- We recommend that Windows update rings are managed centrally. The Central team should create as many common Windows update ring policies as they need to support the variance of the local admins.
- The local admins shouldn't create their own Windows update rings. When you delegate to a large number of administrators, the total number of objects might become large and difficult to manage. Best practices vary for each feature. For more information, see [Windows update rings](../protect/windows-10-update-rings.md).

#### Feature updates

The [Full delegation model](#full-delegation-model) is recommended.

#### Quality updates

The [Full delegation model](#full-delegation-model) is recommended.

### Certificates

- We recommend you use permissions through the Central team to onboard and offboard connectors as needed. Onboard connectors for each local admin to support certificate issuance.

- Don't grant the local admins permission to update or delete connectors.

### Applications

Grant local admins full permissions to manage apps to the extent of their scope.

In this section:

- Apple Volume Purchase Program

- Windows

- Android

For more information, see [Manage apps](../apps/apps-add.md).

#### Apple Volume Purchase Program

Currently, there are no scale concerns for the supported number of Volume Purchase Program tokens.
For more information, see [How many tokens can I upload.](../apps/vpp-apps-ios.md#how-many-tokens-can-i-upload).

#### Windows

- Local admins can create Win32 apps as needed within the cross-platform, line-of-business app and web-link limit. For more information, see [Win32 app management](../apps/apps-win32-app-management.md).

  > [!NOTE]
  > Microsoft Store for Business is being retired. Starting with Windows 11, you have a new option for your private volume-licensed apps. For more information, see [Private app repository in Windows 11](/windows/application-management/private-app-repository-mdm-company-portal-windows-11) and [Update to Microsoft Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-endpoint-manager-integration-with-the-microsoft-store/ba-p/3585077).

#### Android

- Local admins should choose from existing store apps or ask the central team to add new Android store apps. Local admins shouldn't create new Android store apps. The total number of objects might become large and difficult to manage.

- Local admins can create Android line-of-business apps, as needed, within the cross-platform, line-of-business app and web-link limit.

- Central team must add Managed Google Play apps.
  - The central team can only see Managed Google Play apps available in their tenant's country or region. If the central team needs a Managed Google Play app only available in specific countries or regions, they might need to work with the app developer to get it listed correctly.
  - The central team should manage all content related to managed Google Play apps, including private apps, web apps, and collections. For example, if a customer plans on using the [Managed Google Play iframe to publish private apps](https://support.google.com/googleplay/work/answer/9146439?hl=en), they have to do that with a single developer account owned by the central team.
  - The central team can select a single scope tag as the Managed Google Play scope tag. It has a special dropdown in the Managed Google Play connector page. The scope tag will apply to all Managed Google Play apps after the central team adds them to the console, but won't apply retroactively to apps that have already been added. We highly recommend that the central team [set the scope tag](../enrollment/connect-intune-android-enterprise.md) before they add apps and then assign each regional team that scope tag. Otherwise, regional admins might not be able to see their Managed Google Play apps.
- Only one OEMConfig policy is supported per device, except for Zebra devices. With Zebra devices, we recommended that you have the smallest number of policies possible because the time to enforce the policy is additive. For example, if you assign six policies with the assumption that they'll layer on top of each other, it takes around 6X longer to start working on the device than a single policy.

> [!NOTE]
> Exercise extreme consideration and caution when setting high-priority update mode on many different apps and groups. This is for multiple reasons:
> - Although many apps can be set to high-priority mode, only one app update can be installed at a time. One large app update could potentially block many smaller updates until the large app is done installing.
> - Depending on when apps release new updates, there could be a sudden spike in your network usage if app releases coincide. If Wi-Fi isn't available on some devices, there could also be a spike in cellular usage.
> - Although disruptive user experiences have already been mentioned, the problem grows as more apps are set to high-priority update mode.

For more information on scale concerns regarding Managed Google Play app updates using high-priority update mode, see the Techcommunity blog [Best practices for updating your Android Enterprise apps](https://techcommunity.microsoft.com/blog/intunecustomersuccess/best-practices-for-updating-your-android-enterprise-apps/3038520).

### Enrollment profiles

In this section:

- Windows Autopilot
- Enrollment status page (ESP)
- Apple business manager (ABM)
- Android Enterprise profiles
- Enrollment restrictions
- Device categories

#### Windows Autopilot

- Grant local admins the permissions to read Windows Autopilot devices and upload new Windows Autopilot devices.
- Local admins shouldn't create Windows Autopilot profiles. When you delegate to a large number of administrators, the total number of objects might become large and difficult to manage. The best practice varies per feature area.
For more information on Windows Autopilot, see [Use Windows Autopilot to enroll Windows devices in Intune](/autopilot/tutorial/autopilot-scenarios).

#### Enrollment status page

- Local admins should select from existing Enrollment status page profiles to assign, or they should request the Central team to create an exception profile, only if necessary.
- Local admins shouldn't create Enrollment status page profiles. When you delegate to a large number of administrators, the total number of objects might become large and difficult to manage. The best practice varies per feature area. For information on Enrollment status page, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

#### Apple Business Manager

If possible, local admins shouldn't be granted create, update, or delete permissions on enrollment profiles. If local admins are given permissions to create Apple Business Manager profiles it also gives them create, update, and delete permissions in Windows Autopilot. However, local admins shouldn't create Windows Autopilot profiles.

When you delegate to a large number of administrators, the total number of objects might become large and difficult to manage. The best practice varies per feature area. For more information, see [Use Apple Business Manager to enroll Apple devices in Intune](../enrollment/tutorial-use-device-enrollment-program-enroll-ios.md).

#### Android Enterprise profiles

- The Central team should create Android Enterprise corporate-owned dedicated devices enrollment profiles for each local admin for device grouping.
- If possible, local admins shouldn't be granted create, update, or delete permissions on Android Enterprise devices. These restrictions prevent local admins from modifying the tenant-wide Android Enterprise settings and the global fully managed enrollment profile.

#### Enrollment restrictions

- The same set of permissions govern both device configuration and Enrollment restrictions. When you grant permissions to create for device configuration, then you're also granting permissions to create for enrollment restrictions. However, local admins shouldn't be given permission to create enrollment restriction profiles. Instead instruct them not to create new Enrollment restrictions profiles.

- Enrollment device limit restrictions define how many devices each user can enroll. The enrollment device limit restrictions should cover all possible device limits for local admins to share. For more information, see [What are enrollment restrictions](../enrollment/enrollment-restrictions-set.md#available-restrictions).

- The Central team should standardize Device Type restrictions as much as possible and add new restrictions but only as special exceptions after a local admin reviews existing restrictions.

#### Device categories

The Device categories (**Devices** > **Device categories**) feature doesn't have its own permissions family. Instead, its permissions are governed by the permissions set under *Organization*. Go to **Tenant administration > Roles**. Select a custom or built-in role and select **Properties**. Here you can assign permissions, one of them being *Organization*.

Central teams can create Device Categories. However, local admins shouldn't be allowed to create, update, or delete device categories, as it would require granting them permissions on *Organization* which grants them access to other tenant-level features governed by *Organization* permissions.

For more information, see [Device categories](../enrollment/device-group-mapping.md).

### Endpoint analytics

- The Central team should create as many common Endpoint Analytics baselines as they need to support the variance of the Local admins.
- If possible, local admins shouldn't create their own Endpoint Analytics baselines. When you delegate to a large number of administrators, the total number of objects might become large and difficult to manage. The best practice varies per feature area.
- For more information, see [Configuring settings in Endpoint analytics](../../endpoint-analytics/settings.md).
