---
title: Add users to Microsoft Intune
description: Learn how to add and managing Microsoft Entra user accounts from within Microsoft Intune.
author: paolomatarazzo
ms.author: paoloma
ms.date: 03/04/2025
ms.topic: how-to
ms.reviewer: dougeby
ms.collection:
- M365-identity-device-management
- highpri
---

# Add and manage users for Microsoft Intune

Microsoft Entra ID, part of Microsoft Entra, is the identity service for Microsoft Intune which means user accounts you see in Intune exist in Microsoft Entra. As an administrator with sufficient role-based access control (RBAC) permissions within Microsoft Entra, you can use the Intune admin center to manage Microsoft Entra user account. Those same Entra permissions also enable an admin to manage users from within the Microsoft 365 admin center or directly through the Microsoft Entra admin center.

Intune also supports use of user accounts that synchronize from Active Directory to any cloud-based service that shares the tenant with Intune and your Entra tenant.

After a user is added or synchronized to Entra and [assigned a license to Intune](../fundamentals/licenses-assign.md), that user can enroll devices with Intune and begin to access company resources. Intune administrators can also [assign Intune RBAC roles](../fundamentals/assign-role.md) and permissions to discreet groups of users to enable those users to help administer your Intune subscription.

The remainder of this article focuses on using the Intune admin center to manage user accounts.

- For information on using the Microsoft Entra admin center to manage users, see [How to create, invite, and delete users](/entra/fundamentals/how-to-create-delete-users) in the Microsoft Entra documentation.
- For information on using the Microsoft 365 admin center to manage users, see [Add users](/microsoft-365/admin/add-users/add-users) and [Add several users](/microsoft-365/enterprise/add-several-users-at-the-same-time) in the Microsoft 365 documentation.

## Role-based access controls for managing user accounts

Before you can use the Intune admin center to manage users, your account must have RBAC permissions within Microsoft Entra to manage user accounts. Microsoft Entra permissions are required as Intune RBAC is a subset of Entra RBAC. As a subset, Intune-only RBAC permissions aren't sufficient to manage accounts in Microsoft Entra. However, there are some [Microsoft Entra roles](../fundamentals/role-based-access-control.md#microsoft-entra-roles-with-intune-access) that include permissions within Intune.

When working with RBAC, Microsoft recommends following the principle of least-permissions by using only accounts that have the minimum required permissions for a task, and **limiting** use and assignment of [privileged](/entra/identity/role-based-access-control/privileged-roles-permissions) administrative roles like the Intune Administrator.

The following Microsoft Entra built-in RBAC role is the least privileged built-in role that includes sufficient permissions to add and manage user accounts:

- [**User Administrator**](/entra/identity/role-based-access-control/permissions-reference#user-administrator) – This role provides permissions sufficient to add and edit user accounts from within the admin centers for Microsoft Intune, Microsoft Entra, and Microsoft 365.

> [!TIP]
> The Microsoft Entra *User Administrator* role also provides sufficient permissions to assign licenses to Intune and other products to users. However, license management is a task that can only be managed when using the Microsoft 365 admin center. For more information, see [Assign Intune licenses to users](../fundamentals/licenses-assign.md).

## Add users to Intune

You can use the Intune admin center to manually add new user accounts to your Microsoft Entra ID where they will then be available to your subscription. You can add users individually and also use a bulk operation to add multiple users at the same time when they're defined in a csv file.

### Add individual users

The following procedural steps can be used to add individual users to your Intune subscription. For a more complete review of creating new user accounts, see [How to create, invite, and delete users](/entra/fundamentals/how-to-create-delete-users) in the Microsoft Entra documentation.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Users** > **All users** > select **New user** > **Create new user**.

2. On the **Basics** tab, configure the following user details:
   - **User principal name** - The User Principal Name (UPN) is stored in Microsoft Entra ID and is used to access services, including Microsoft Entra, Microsoft 365, and Microsoft Intune.
   - **Mail nickname** - To enter an email nickname that is different from the user principal name, uncheck the **Derive from user principal name** option and then enter the mail nickname.
   - **Display name** – How the user's name is displayed. For example, Chris Green or Chris A. Green.
   - **Password** - Add a password for the new user or choose to have it autogenerated. All new users are directed to create a new password at their first sign-in.
   - **Account enabled** - When an account isn't enabled, the user is blocked from signing in. This setting can be updated after creating the account.

   You can select **Review + create** to create the new user account using only the Basic information, or you can select **Next: Properties** to complete additional but optional configurations.

3. On the **Properties** tab, configure the following details which are all optional. Values that aren't specified remain blank when the account is created and can be edited later.
   - **Identity**:
     - **First name**
     - **Last name**
     - **User type** - Choose either **Member** or **Guest**. Both user types are internal to your organization. Members are commonly full-time employees in your organization. Guests have an account in your tenant, but have [guest-level privileges](/entra/identity/users/users-restrict-guest-permissions).
     - **Authorization info** – When you use Certificate Based Authentication for users, you can use this field to add up to five certificate user IDs. For more information, see [Mapping to the certificateUserIds attribute in Microsoft Entra ID](/entra/identity/authentication/concept-certificate-based-authentication-certificateuserids).
   - **Job information**: Specify job-related information, like the user's job title, department, or manager.
   - **Contact information**: Add contact information for the user.
   - **Parental controls**: For organizations like K-12 school districts, the user's age group might need to be provided. *Minors* are 12 and under, *Not adult* are 13-18 years old, and *Adults* are 18 and over. The combination of age group and consent provided by parent options determine the Legal age group classification. The Legal age group classification might limit the user's access and authority.
   - **Settings**: You can use **Usage location** to identify a user's global location.

   Select **Review + create** or continue on to **Next: Assignments**.

4. On the **Assignments** tab you can assign the user to a single administrative unit, and up to 20 groups or Microsoft Entra roles at the time the account is created. You can also configure Assignments after the user is created.

   > [!TIP]
   > Some options might not be available to configure based on your accounts level of privilege in Microsoft Entra. For example, if you're assigned only the *User Administrator* role, you can assign users to groups but lack rights to assign an administrative unit or assign the user a Microsoft Entra role. For information about the permissions provided by different roles, see [Microsoft Entra built-in roles](/entra/identity/role-based-access-control/permissions-reference).

   **To assign a group to the new user**:
   1. Select **+ Add group**.
   2. From the menu that appears, choose up to 20 groups from the list and select the **Select** button.
   3. Select the **Review** + **create** button.

   **To assign a Microsoft Entra role to the new user**:
   When a user requires permissions within Entra, you can use this option to assign them a suitable role. To assign Entra roles to other accounts, your account must have permissions equal to the Microsoft Entra [Privileged Role Administrator](/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator).

   > [!TIP]
   > Most users you add to Intune won't require a *Microsoft Entra* role assignment. Instead, for the users that manage only Intune, plan to [assign an Intune RBAC role](../fundamentals/assign-role.md) to them after their account is created.

   1. Select **+ Add role**.
   2. From the menu that appears, choose up to 20 roles from the list and select the **Select** button.
   3. Select the **Review + create** button.

   **To add an administrative unit to the new user**:
   Most users you add to Intune will never require an Administrative Units (AUs), which in Microsoft Entra ID is a powerful way to delegate administrative control over subsets of users, groups, or devices within your organization.

   Instead, within Intune you can use [scope tags](../fundamentals/scope-tags.md) and [scope groups](../fundamentals/role-based-access-control.md#about-intune-role-assignments).

   To assign an administrative unit to a user, your account must have permissions equal to the Entra [Privileged Role Administrator](/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator).

   1. Select **+ Add administrative unit**.
   2. From the menu that appears, select one administrative unit and then the **Select** button.
   3. Select the **Review + create**.

5. On the **Review + Create** tab, review the details to be sure the information is correct and details passed validation. Review the details and select the **Create** button if everything looks good.

> [!NOTE]
> You can also invite guest users to your Intune tenant. For more information, see [Add Microsoft Entra B2B collaboration users in the Microsoft Entra admin center](/entra/external-id/add-users-administrator).

### Add multiple users

You can add Intune users in bulk by uploading a csv file containing the full list of users. The csv file is a comma-separated value list that can be edited in Notepad or Excel.

**To add multiple users to Intune**:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Users** > **All users** > **Bulk operations** > **Bulk create**. The **Bulk create users** pane is displayed, which provides an option to **Download** a CVS template you can use.
3. When your CVS template is ready, use the browse functionality to locate and upload the file. Select **Submit** to begin the import.

   For more information about using a csv file to add Intune users, see [Bulk create users in Microsoft Entra ID](/azure/active-directory/enterprise-users/users-bulk-add).

> [!NOTE]
> You can also invite multiple guest users to your Intune tenant. For more information, see [Tutorial: Bulk invite Microsoft Entra B2B collaboration users](/entra/external-id/tutorial-bulk-invite).

## Sync Active Directory and add users to Intune

You can configure directory synchronization to import user accounts from your on-premises Active Directory to Microsoft Entra which includes Intune users. Having your on-premises Active Directory service connected with all of your Entra ID-based services makes managing user identity simpler. You can also configure single sign-on features to make the authentication experience for your users familiar and easy. When you link the same [Entra tenant](/azure/active-directory/hybrid/whatis-hybrid-identity) with multiple services, the user accounts that you previously synchronized are available to all your cloud-based services.

Be sure your Active Directory admins have access to your Entra subscription and are trained to complete common Active Directory and Microsoft Entra tasks.

### How to sync on-premises users with Microsoft Entra ID

- To move existing users from on-premises Active Directory to Entra ID, you can set up [hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity). Hybrid identities exist in both services - on-premises Active Directory and Microsoft Entra ID.
- You can also export Active Directory users using the UI or through script. An internet search can help you find the best option for your organization.
- To synchronize your user accounts with Entra ID, use the [Microsoft Entra Connect wizard](https://www.microsoft.com/download/details.aspx?id=47594). The *Microsoft Entra Connect* wizard provides a simplified and guided experience for connecting your on-premises identity infrastructure to the cloud. Choose your topology and needs (single or multiple directories, password hash sync, pass-through authentication, or federation). The wizard deploys and configures all components required to get your connection up and running. Including: sync services, Active Directory Federation Services (AD FS), and the [Microsoft Graph PowerShell](/powershell/microsoftgraph/overview) module.

> [!TIP]
> *Microsoft Entra Connect* encompasses functionality that was previously released as *Dirsync* and *Azure AD Sync*. Learn more about [directory integration](/previous-versions/azure/azure-services/jj573653(v=azure.100)). To learn about syncing user accounts from a local directory to Entra ID, see [Similarities between Active Directory and Microsoft Entra ID](/previous-versions/azure/azure-services/dn518177(v=azure.100)).

## Delete users

After a user leaves your organization, you can use the Intune admin center to delete them from Microsoft Entra, which also removes them from Intune. You can also delete multiple users using **Bulk operations**.

To delete users from Entra, your administrative account must have permissions equal to the Microsoft Entra [User Administrator](/entra/identity/role-based-access-control/permissions-reference#user-administrator) role.

**To delete an individual user from Intune**:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Browse to **Users** > **All users**.
3. Select the user you want to delete.
4. Select **Delete**.

**To delete multiple users from Intune**:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Users** > **All users** > **Bulk operations** > **Bulk delete**. The *Bulk delete users* pane is displayed which provides an option to **Download** a CVS template you can use.
3. When your CVS template is ready, use the browse functionality to locate and upload the file. Select **Submit** to begin deletion.

   For related information, see [Bulk delete users in Microsoft Entra ID](/entra/identity/users/users-bulk-delete).

> [!TIP]
> As a user with sufficient permissions to manage user accounts, there are some accounts you might not be able to delete. Reasons you can't delete a specific account can include:
> - Accounts that are synchronized from an on-premises Active Directory.
> - Accounts that are assigned a higher-privileged Entra role than your account.
- what resources they can change.
> - Accounts that fall outside your current Intune [scope group](../fundamentals/role-based-access-control.md#about-intune-role-assignments) when using the Intune admin center.

## Related content

- [Add groups to organize users and devices](../fundamentals/groups-add.md)
- [Assign users licenses to Intune](../fundamentals/licenses-assign.md)
