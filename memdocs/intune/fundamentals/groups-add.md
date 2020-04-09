---
# required metadata

title: Add groups to organize users and devices
titleSuffix: Microsoft Intune
description: Add groups to organize users and devices by geography, department, or hardware specifics.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: f0a2b858-a824-4598-ab81-bdd8e62ac3b3

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add groups to organize users and devices

Intune uses Azure Active Directory (Azure AD) groups to manage devices and users. As an Intune admin, you can set up groups to suit your organizational needs. Create groups to organize users or devices by geographic location, department, or hardware characteristics. Use groups to manage tasks at scale. For example, you can set policies for many users or deploy apps to a set of devices.

You can add the following types of groups:

- **Assigned groups** - Manually add users or devices into a static group. 
- **Dynamic groups** (Requires Azure AD Premium) - Automatically add users or devices to user groups or device groups based on an expression you create.

  For example, when a user is added with the manager title, the user is automatically added to an **All managers** users group. Or, when a device has the iOS/iPadOS device OS type, the device is automatically added to an **All iOS/iPadOS devices** devices group.

## Add a new group

Use the following steps to create a new group.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Groups** > **New group**:

   ![Screenshot of the Azure portal with New Group selected](./media/groups-add/groups-add-new.png)

3. In **Group type**, choose one of the following options:

    - **Security**: Security groups define who can access resources, and are recommended for your groups in Intune. For example, you can create groups for users, such as **All Charlotte employees** or **Remote workers**. Or, create groups for devices, such as **All iOS/iPadOS devices** or **All Windows 10 student devices**.

        > [!TIP]
        > The users and groups created can also be seen in the [Microsoft 365 admin center](https://admin.microsoft.com), Azure Active Directory admin center, and [Microsoft Intune in the Azure portal](https://go.microsoft.com/fwlink/?linkid=2090973). In your organization tenant, you can create and manage groups in all these areas.
        >
        > If your primary role is device management, we recommend you use the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

    - **Office 365**: Provides collaboration opportunities by giving members access to a shared mailbox, calendar, files, SharePoint site, and more. This option also lets you give people outside of your organization access to the group. For more information, see [Learn about Office 365 Groups](https://support.office.com/article/learn-about-office-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2).

4. Enter a **Group name** and **Group description** for the new group. Be specific and include information so others know what the group is for.

    For example, enter **All Windows 10 student devices** for group name, and **All Windows 10 devices used by students in Contoso high school grades 9-12** for group description.

5. Enter the **Membership type**. Your options:

    - **Assigned**: Administrators manually assign users or devices to this group, and manually remove users or devices.
    - **Dynamic User**: Administrators create membership rules to automatically add and remove members.
    - **Dynamic Device**: Administrators create dynamic group rules to automatically add and remove devices.

        ![Screenshot of Intune group properties](./media/groups-add/groups-add-properties.png)

    For more information on these membership types, and creating dynamic expressions, see:

    - [Create a basic group and add members using Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal)
    - [Dynamic membership rules for groups in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership)

    > [!NOTE]
    > In this admin center, when you create users or groups, you might not see the **Azure Active Directory** branding. But, that's what you're using.

6. Choose **Create** to add the new group. Your group is shown in the list.

> [!TIP]
> Consider some of the other dynamic user and device groups you can create, such as:
>
> - All Students in Contoso high school
> - All Android Enterprise devices
> - All iOS 11 and older devices
> - Marketing
> - Human Resources
> - All Charlotte employees
> - All WA employees

## Groups and policies

Access to your organization’s resources are controlled by users and groups you create.

When you create groups, consider how you'll apply [compliance policies](../protect/device-compliance-get-started.md) and [configuration profiles](../configuration/device-profiles.md). For example, you might have:

- Policies that are specific to a device operating system.
- Policies that are specific to different roles in your organization.
- Policies that are specific to organizational units you defined in Active Directory.

To create the basic compliance requirements of your organization, you can create a default policy that applies to all groups and devices. Then, create more specific policies for the broadest categories of users and devices. For example, you might create email policies for each of the device operating systems.

For configuration profile recommendations and guidance, see [Assign policies to user groups or device groups](../configuration/device-profile-assign.md#user-groups-vs-device-groups) and [profile recommendations](../configuration/device-profile-create.md#recommendations).

## See also

- [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)
- [Manage access to resources with Azure AD groups](https://docs.microsoft.com/azure/active-directory/active-directory-manage-groups)
