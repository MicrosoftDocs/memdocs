---
title: Walkthrough-Create a settings catalog policy
description: This tutorial or walkthrough steps through creating and comparing an on-premises Administrative Templates (ADMX) Group Policy and Microsoft Intune cloud-based settings catalog policy. It shows similar settings in on-premises and the Intune settings catalog to create and manage policies for Office, Windows, and Microsoft Edge on Windows 10/11 client devices.
author: MandiOhlinger
ms.author: mandia
ms.date: 08/21/2025
ms.topic: tutorial
ms.reviewer: mayurjadhav
ms.collection:
- M365-identity-device-management
- intune-scenario
---

# Walkthrough - Create an Intune settings catalog policy and compare with on-premises ADMX

> [!NOTE]
> This walkthrough was created as a technical workshop and updated to apply to the Intune settings catalog. It has more prerequisites than typical walkthroughs, as it compares using and configuring settings catalog policies in Intune and on-premises Group Policy Administrative Templates (ADMX).

Group policy and ADMX templates include settings you can configure on Windows devices. These settings are used and managed by Mobile Device Management (MDM) providers, like Microsoft Intune, to configure features and settings on Windows devices. For example, you can turn on Design Ideas in PowerPoint, set a home page in Microsoft Edge, and more.

These settings are built into the Microsoft Intune [settings catalog](settings-catalog.md). In a settings catalog profile, you configure the settings you want to include, and then assign this profile to your devices.

In this walkthrough, you:

> [!div class="checklist"]
>
> - Get introduced to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
> - Create user groups and create device groups.
> - Compare the settings in Intune with on-premises ADMX settings.
> - Create different settings catalog policies, and configure the settings that target the different groups.

By the end of this lab, you can use Intune to manage your users, and deploy settings catalog policies.

This feature applies to:

- Windows
- Microsoft Edge version 77 and newer

> [!TIP]
>
> - For an overview of the Intune settings catalog, go to [Use the settings catalog to configure settings](settings-catalog.md).
> - For more information on ADMX policies, go to [Understanding ADMX-backed policies](/windows/client-management/mdm/understanding-admx-backed-policies).

## Prerequisites

- A Microsoft 365 E3 or E5 subscription, which includes Intune and Microsoft Entra ID P1 or P2. If you don't have an E3 or E5 subscription, [try it for free](/microsoft-365/commerce/try-or-buy-microsoft-365).

  For more information on what you get with the different Microsoft 365 licenses, go to [Transform your Enterprise with Microsoft 365](https://www.microsoft.com/microsoft-365/enterprise/microsoft365-plans-and-pricing).

- Microsoft Intune is configured as the **Intune MDM Authority**. For more information, go to [Set the mobile device management authority](../fundamentals/mdm-authority-set.md).

  :::image type="content" source="./media/tutorial-settings-catalog-group-policy/tenant-status.png" alt-text="Screenshot that shows how to set the MDM authority to Microsoft Intune in your tenant status.":::

- On an on-premises Active Directory domain controller (DC):

  1. Copy the following Office and Microsoft Edge templates to the [Central Store (sysvol folder)](/troubleshoot/windows-client/group-policy/create-and-manage-central-store):

      - [Office administrative templates](https://www.microsoft.com/download/details.aspx?id=49030)
      - [Microsoft Edge policy file](https://www.microsoft.com/edge/business/download)

  2. Create a group policy to push these templates to a Windows Enterprise administrator computer in the same domain as the DC. In this walkthrough:

      - The group policy we created with these templates is named **OfficeandEdge**. You'll see this name in the images.
      - The Windows Enterprise administrator computer we use is named the **Admin computer**.

      In most organizations, a domain administrator has two accounts:
        - A typical domain work account
        - A different domain administrator account used only for domain administrator tasks, like group policy

      The purpose of this **Admin computer** is for administrators to sign in with their domain administrator account, and access tools designed for managing group policy.

- On this **Admin computer**:

  - Sign in with a Domain Administrator account.

  - Add the **RSAT: Group Policy Management Tools**:

    1. Open the **Settings** app > **System** > **Add an optional feature** > **View features**.

    1. Select **RSAT: Group Policy Management Tools** > **Add**.

        Wait while Windows adds the feature. When complete, it eventually shows in the **Windows Administrative Tools** app.

        :::image type="content" source="./media/tutorial-settings-catalog-group-policy/windows-administrative-tools-app.png" alt-text="Screenshot that shows the Windows Administrative Tools apps, including the Group Policy Management app." lightbox="./media/tutorial-settings-catalog-group-policy/windows-administrative-tools-app.png":::

  - Be sure you have internet access and administrator rights to the Microsoft 365 subscription, which includes the Intune admin center.

## Open the Intune admin center

1. Open a Chromium-based web browser, like Microsoft Edge.
2. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Sign in with the following account:

    **User**: Enter the administrator account of your Microsoft 365 tenant subscription.
    **Password**: Enter its password.

The Intune admin center is focused on device management, and includes Azure services, like Microsoft Entra ID. You might not see the **Microsoft Entra ID** and **Azure** branding, but you're using them.

You can also open the Intune admin center from the [Microsoft 365 admin center](https://admin.microsoft.com):

1. Go to [https://admin.microsoft.com](https://admin.microsoft.com).
2. Sign in with the administrator account of your Microsoft 365 tenant subscription.
3. Select **Show all** > **Admin centers** > **Microsoft Intune**. The Intune admin center opens.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/microsoft-365-admin-centers.png" alt-text="Screenshot that shows the admin centers in the Microsoft 365 admin center.":::

## Create groups, and add users

On-premises policies are applied in the LSDOU order - local, site, domain, and organizational unit (OU). In this hierarchy, OU policies overwrite local policies, domain policies overwrite site policies, and so on.

In Intune, policies are applied to users and groups you create. There isn't a hierarchy. For example:

- If two policies update the same setting, then the setting shows as a conflict.
- If two compliance policies are in conflict, then the most restrictive policy applies.
- If two configuration profiles are in conflict, then the setting isn't applied.

For more information, go to [Common questions, issues, and resolutions with device policies and profiles](device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

In these next steps, you create security groups, and add users to these groups. You can add a user to multiple groups. For example, it's normal for a user to have multiple devices, like a Surface Pro for work, and an Android mobile device for personal. And, it's normal for a person to access organizational resources from these multiple devices.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New group**.

2. Enter the following settings:

    - **Group type**: Select **Security**.
    - **Group name**: Enter **All Windows student devices**.
    - **Membership type**: Select **Assigned**.

3. Select **Members**, and add some devices.

    Adding devices is optional. The goal is to practice creating groups, and knowing how to add devices. If you're using this walkthrough in a production environment, then be aware of what you're doing.

4. **Select** > **Create** to save your changes.

    Don't see your group? Select **Refresh**.

5. Select **New group**, and enter the following settings:

    - **Group type**: Select **Security**.
    - **Group name**: Enter **All Windows devices**.
    - **Membership type**: Select **Dynamic Device**.
    - **Dynamic device members**: Select **Add dynamic query**, and configure your query:

        - **Property**: Select **deviceOSType**.
        - **Operator**: Select **Equals**.
        - **Value**: Enter **Windows**.

        1. Select **Add expression**. Your expression is shown in the **Rule syntax**:

            :::image type="content" source="./media/tutorial-settings-catalog-group-policy/dynamic-group-query.png" alt-text="Screenshot that shows how to create a dynamic group query, and add expressions in Microsoft Intune." lightbox="./media/tutorial-settings-catalog-group-policy/dynamic-group-query.png":::

            When users or devices meet the criteria you enter, they're automatically added to the dynamic groups. In this example, devices are automatically added to this group when the operating system is Windows. If you're using this walkthrough in a production environment, then be careful. The goal is to practice creating dynamic groups.

        2. **Save** > **Create** to save your changes.

6. Create the **All Teachers** group with the following settings:

    - **Group type**: Select **Security**.
    - **Group name**: Enter **All Teachers**.
    - **Membership type**: Select **Dynamic User**.
    - **Dynamic user members**: Select **Add dynamic query**, and configure your query:

      - **Property**: Select **department**.
      - **Operator**: Select **Equals**.
      - **Value**: Enter **Teachers**.

        1. Select **Add expression**. Your expression is shown in the **Rule syntax**.

            When users or devices meet the criteria you enter, they're automatically added to the dynamic groups. In this example, users are automatically added to this group when their department is Teachers. You can enter the department and other properties when users are added to your organization. If you're using this walkthrough in a production environment, then be careful. The goal is to practice creating dynamic groups.

        2. **Save** > **Create** to save your changes.

### Talking points

- Dynamic groups are a feature in some Microsoft Entra ID licenses. If you don't have the correct Microsoft Entra ID license, then you're only licensed to create assigned groups. For more information on dynamic groups, go to:

  - [Understand and manage dynamic group processing in Microsoft Entra ID](/entra/identity/users/manage-dynamic-group)
  - [Manage rules for dynamic membership groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership)

- Your Microsoft Entra ID license can include other services that are commonly used when managing apps and devices, including [multifactor authentication (MFA)](/entra/identity/authentication/concept-mfa-howitworks) and [Conditional Access](/entra/identity/conditional-access/overview).

- Many administrators ask when to use user groups and when to use device groups. For some guidance, go to [User groups vs. device groups](device-profile-assign.md#user-groups-vs-device-groups).

- Remember, a user can belong to multiple groups. Consider some of the other dynamic user and device groups you can create, like:

  - All Students
  - All Android devices
  - All iOS/iPadOS devices
  - Marketing
  - Human Resources
  - All Charlotte employees
  - All Redmond employees
  - West coast IT administrators
  - East coast IT administrators

The users and groups created are also seen in the [Microsoft 365 admin center](https://admin.microsoft.com) and [Microsoft Entra admin center](https://entra.microsoft.com). You can create and manage groups in all these areas for your tenant subscription. **If your goal is device management, then use the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)**.

### Review group membership

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Users** > **All users** > select the name of any existing user.
2. Review some of the information you can add or change. For example, look at the **Properties** you can configure, like Job Title, Department, City, Office location, and more. You can use these properties in your dynamic queries when you create dynamic groups.
3. Select **Groups** to see the membership of this user. You can also remove the user from a group.
4. Select some of the other options to see more information, and what you can do. For example, look at the assigned license, the user's devices, and more.

### What did I just do?

In the Intune admin center, you created new security groups, and added existing users and devices to these groups. We use these groups in later steps in this tutorial.

## Create a settings catalog policy in Intune

In this section, we create a settings catalog policy in Intune, look at some settings in on-premises **Group Policy Management**, and compare the same setting in Intune. The goal is to show a setting in group policy, and show the same setting in Intune.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
2. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

3. Select **Create**.
4. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, enter **Windows student devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. Select **Next**.
6. In **Configuration settings**, select **Add settings**. You see a list of all the settings.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-settings-picker.png" alt-text="Screenshot that shows the settings catalog settings picker in Microsoft Intune." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-settings-picker.png":::

     You can also filter settings that apply to **devices** and settings that apply to **users**, and **Search** for settings:

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-filter-search.png" alt-text="Screenshot that shows how you can filter and search in the settings catalog settings picker in Microsoft Intune.":::

7. In search, enter **download**. All the policy settings with "download" in their name are filtered and shown in the list:

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-download-settings.png" alt-text="Screenshot that shows how to search for policies with a keyword in the settings catalog in a Microsoft Intune." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-download-settings.png":::

8. Go to the **Microsoft Edge** category > select **SmartScreen settings**. Notice the SmartScreen policy settings with "download" in their name are filtered and shown:

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-microsoft-edge-smart-screen-filtered-settings.png" alt-text="Screenshot that shows how to see the Microsoft Edge Smart Screen policy settings in the settings catalog in Microsoft Intune." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-microsoft-edge-smart-screen-filtered-settings.png":::

### Compare a policy in Group Policy Management and Intune

In this section, we show a policy in Intune and its matching policy in Group Policy Management Editor.

1. On the **Admin computer**, open the **Group Policy Management** app.

    This app gets installed with **RSAT: Group Policy Management Tools**, which is an optional feature you add on Windows. [Prerequisites](#prerequisites) (in this article) lists the steps to install it.

2. Expand **Domains** > select your domain. For example, select `contoso.net`.
3. Right-click the **OfficeandEdge** policy > **Edit**. The Group Policy Management Editor app opens.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/open-group-policy-management.png" alt-text="Screenshot that shows how to right-click the on-premises Office and Microsoft Edge ADMX group policy, and select Edit.":::

    **OfficeandEdge** is a group policy that includes the Office and Microsoft Edge ADMX templates. This policy is described in [prerequisites](#prerequisites) (in this article).

4. Expand **Computer configuration** > **Policies** > **Administrative Templates** > **Control Panel** > **Personalization**. Notice the available settings.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/open-group-policy-management-editor-admx-policy.png" alt-text="Screenshot that shows how to expand Computer Configuration in on-premises Group Policy Management Editor, and go to Personalization.":::

    Double-click **Prevent enabling lock screen camera**, and see the available options:

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/prevent-enabling-lock-screen-camera-admx-policy.png" alt-text="Screenshot that shows how to see the on-premises Computer configuration setting options in group policy.":::

5. In the Intune admin center, go to your **Windows student devices** settings catalog policy.
6. Select **Configuration settings** > **Edit** > **Add settings**. Search for **Personalization** and select the `Administrative templates\Control Panel\Personalization` category. Notice the available settings:

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-admx-personalization-category.png" alt-text="Screenshot that shows the ADMX personalization policy setting path in the Microsoft Intune settings catalog." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-admx-personalization-category.png":::

    This path and the available settings are similar to what you see in Group Policy Management Editor. If you select the **Prevent enabling lock screen camera** setting, you see similar options that are available in Group Policy Management Editor.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-control-panel-personalization.png" alt-text="Screenshot that shows the ADMX Prevent enabling lock screen camera setting path in the Microsoft Intune settings catalog." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-control-panel-personalization.png":::

### Compare a user policy in Group Policy Management and Intune

1. In your **Windows student devices** settings catalog policy, select **Configuration settings** > **Edit** > **Add settings**. Search for `inprivate browsing`. Notice the settings options. The `(User)` setting applies to user configurations. The other setting applies to device configurations.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-inprivate-browsing.png" alt-text="Screenshot that shows a user setting and a device setting in the Microsoft Intune settings catalog." lightbox="./media/tutorial-settings-catalog-group-policy/settings-catalog-inprivate-browsing.png":::

2. In **Group Policy Management Editor**, find the matching user and device settings:

    - Device: Expand **Computer configuration** > **Policies** > **Administrative Templates** > **Windows components** > **Internet Explorer** > **Privacy** > **Turn off InPrivate Browsing**.
    - User: Expand **User configuration** > **Policies** > **Administrative Templates** > **Windows components** > **Internet Explorer** > **Privacy** > **Turn off InPrivate Browsing**.

    :::image type="content" source="./media/tutorial-settings-catalog-group-policy/group-policy-turn-off-inprivate-browsing.png" alt-text="Screenshot that shows how to turn off InPrivate Browsing in Internet Explorer using on-premises ADMX template.":::

> [!TIP]
> To see the built-in Windows policies, you can also use GPEdit (**Edit group policy** app).

### What did I just do?

You created a settings catalog policy in Intune. In this policy, we looked at some settings, and looked at the same ADMX settings in on-premises Group Policy Management.

## Create a OneDrive settings catalog policy

In this section, you create a OneDrive settings catalog policy in Intune to control some settings. These specific settings are chosen because they're commonly used by organizations.

1. Create another Intune policy (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**).

2. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

3. Select **Create**.
4. In **Basics**, enter the following properties:

    - **Name**: Enter **OneDrive policies for all Windows users**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. Select **Next**.
6. In **Configuration settings**, select **Add settings**. In the category list, search for or go to **OneDrive**. Select the following settings and then close the settings picker:

    - **Prevent users from syncing personal OneDrive accounts (User)**
    - **Silently sign in users to the OneDrive sync app with their Windows credentials**
    - **Use OneDrive Files On-Demand**

7. Configure these settings:

    | Setting | Value |
    |---------|-------|
    | Prevent users from syncing personal OneDrive accounts (User) | Enabled |
    | Silently sign in users to the OneDrive sync app with their Windows credentials | Enabled |
    | Use OneDrive Files On-Demand | Enabled |

Your settings look similar to the following settings:

:::image type="content" source="./media/tutorial-settings-catalog-group-policy/settings-catalog-onedrive.png" alt-text="Screenshot that shows how to create a OneDrive settings catalog policy in Microsoft Intune.":::

For more information on OneDrive client settings, go to [Use Group Policy to control OneDrive sync client settings](/sharepoint/use-group-policy).

### Assign your policy

1. In your policy, select **Next** until you get to **Assignments**. Choose **Add groups**:
2. A list of existing users and groups is shown. Select the **All Windows devices** group you created earlier > **Select**.

    If you're using this walkthrough in a production environment, then consider adding groups that are empty. The goal is to practice assigning your policy.

3. Select **Next**. In **Review + create**, select **Create** to save your changes.

In this section, you created some settings catalog policies, and assigned them to groups you created.

## Policy best practices

When you create policies and profiles in Intune, there are some recommendations and best practices to consider. For more information, go to [policy and profile best practices](device-profile-create.md#recommendations).

## Clean up resources

When no longer needed, you can:

- Delete the groups you created:

  - **All Windows student devices**
  - **All Windows devices**
  - **All Teachers**

- Delete the settings catalog policies you created:

  - **Windows student devices**
  - **OneDrive policies that apply to all Windows users**

## Summary

In this tutorial, you got more familiar with the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), used the query builder to create dynamic groups, and created settings catalog policies in Intune to configure different settings. You also compared using ADMX templates on-premises and in the cloud with Intune.
