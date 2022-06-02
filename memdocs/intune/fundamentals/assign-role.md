---
# required metadata

title: Assign a role to an Intune user
description: Learn how to assign a built-in or custom role to a user in Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 08/05/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Assign a role to an Intune user

You can assign a [built-in](role-based-access-control.md#built-in-roles) or [custom](create-custom-role.md) role to an Intune user.

To create, edit, or assign roles, your account must have one of the following permissions in Azure AD:
- **Global Administrator**
- **Intune Service Administrator**

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles**.

2. On the **Endpoint Manager roles - All roles** blade, choose the built-in role you want to assign > **Assignments** > **+ Assign**.

3. On the **Basics** page, enter an **Assignment name** and optional **Assignment description**, and then choose **Next**.

4. On the **Admin Groups** page, select the group that contains the user you want to give the permissions to. Choose **Next**.

5. On the **Scope (Groups)** page, choose a group containing the users/devices that the member above will be allowed to manage. You also have the option to choose all users and/or all devices. Choose **Next**.
  
      > [!NOTE] 
      > The **All users** and **All devices** are [Intune virtual groups](groups-add.md) and not Azure Active Directory (Azure AD) security groups. As a result, for **Scope (Groups)** assignment purposes you cannot use them as parents of Azure AD security groups. If you need both **All users** and **All devices** and specific Azure AD security groups for **Scope (Groups)** assignments, you must add them separately with separate assignments. Otherwise, even if the **Scope (Groups)** assignment for a role is set to **All Users** the admin in this role won't have access to specific Azure AD user groups.
      >  
      > For Azure AD security groups, nesting is supported.

7. On the **Scope (Tags)** page, choose tags where this role assignment will be applied. Choose **Next**.

8. On the **Review + Create** page, when you're done, choose **Create**. The new assignment is displayed in the list of assignments.

    > [!NOTE] 
    > When you create scope groups and assign a scope tag, you can only target groups that are listed in the Scope (Groups) of your role assignment.

## Next steps
- [Learn more about role-based access control in Intune](role-based-access-control.md)
- [Create a custom role](create-custom-role.md)


