---
# required metadata

title: Migrate your imported group policy to a policy in Microsoft Intune
description: After you import your Windows group policy objects in Microsoft Intune, use the migrate feature to transfer your GPOs to a Settings Catalog policy. This policy uses your imported GPOs, and can be assigned to users and devices managed by your organizations.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 05/04/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Create a Settings Catalog policy using your imported GPOs in Microsoft Intune (public preview)

You can import your on-premises Group Policy Objects (GPOs), and create an Intune policy using these imported settings. This policy can be deployed to users and devices managed by your organization.

With Group Policy Analytics, you import your on-premises GPOs. It analyzes your imported GPOs, and shows the settings that are also available in Microsoft Intune. For the settings that are available, you can create a [Settings Catalog policy](settings-catalog.md), and then deploy the policy to your managed devices.

This feature applies to:

- Windows 11
- Windows 10

This article shows you how to create the policy from your imported GPOs. For more information and an overview on Group Policy Analytics, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Intune](group-policy-analytics.md).

## Before you begin

- In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in as:

  - The **Intune administrator**

  **OR**

  - With a role that has the **Security baselines** permission and the **Device configurations/Create** permission

  For more information about the permissions included with the built-in Intune roles, go to [built-in admin roles](../fundamentals/role-based-access-control.md#built-in-roles). For information on custom roles, go to [assign permissions to custom roles](../fundamentals/create-custom-role.md#custom-role-permissions).

- Import your on-premises GPOs, and review the results.

  For the specific steps, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Intune](group-policy-analytics.md).

- Only admins scoped to the GPO can create a settings catalog policy from that imported GPO. Scope tags are first applied during import of the GPO and can be edited. If a scope tag isn't or wasn't selected during the GPO import, then the **Default** scope tag is automatically used.

- This feature is in public preview. For more information, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

## Review and migrate your GPOs to a Settings Catalog policy

After you import your GPOs, review the settings that can be migrated. Remember, some settings don't make sense on cloud native endpoints, like Windows 10/11 devices. After they've been reviewed, you can migrate the settings to a Settings Catalog policy.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)**.
2. In the list, your imported GPOs are shown. Next to the GPO you want in your Settings Catalog profile, select the **Migrate** checkbox. You can select one GPO or many GPOs:

    :::image type="content" source="./media/group-policy-analytics-migrate/select-migrate-checkbox-imported-gpo.png" alt-text="Screenshot that shows how to select the Migrate checkbox next to your imported GPO in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-migrate-checkbox-imported-gpo.png":::

3. To see all the settings in your imported GPO, select **Migrate**:

    :::image type="content" source="./media/group-policy-analytics-migrate/select-migrate-see-all-settings.png" alt-text="Screenshot that shows how to select the Migrate button to see all the settings in your imported GPO in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-migrate-see-all-settings.png":::

4. In the **Settings to migrate** tab, select the **Migrate** column for the settings you want to include in your Settings Catalog profile:

      :::image type="content" source="./media/group-policy-analytics-migrate/settings-to-migrate-tab.png" alt-text="Screenshot that shows the settings to migrate, and how to select the Migrate checkbox in Microsoft Intune.":::

    To help you pick the settings, you can use the built-in features:

    - **Select all on this page**: Select this option if you want all settings on the existing page to be included in your Settings Catalog profile.  

      :::image type="content" source="./media/group-policy-analytics-migrate/select-all-on-this-page.png" alt-text="Screenshot that shows how to use the select all on this page button to include all page settings in the Group Policy Analytics migrate feature in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-all-on-this-page.png":::

    - **Search by setting name**: Enter the setting name to find the settings you want:

      :::image type="content" source="./media/group-policy-analytics-migrate/search-by-setting-name.png" alt-text="Screenshot that shows how to search for the setting name in the Group Policy Analytics migrate feature in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/search-by-setting-name.png":::

    - **Sort**: Sort your settings using the column names:

      :::image type="content" source="./media/group-policy-analytics-migrate/sort-using-column-names.png" alt-text="Screenshot that shows how to sort the settings using the Migrate, Setting name, Group policy setting category, MDM support, value, scope, min OS version, and CSP name Group Policy Analytics migrate features in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/sort-using-column-names.png":::

    > [!TIP]
    > If you haven't already, review your Group Policy settings. It's possible some settings don't apply to cloud-based policy management or don't apply to cloud native endpoints, like Windows 10/11 devices. It's not recommended to include all your Group Policy settings without reviewing them.

    Select **Next**.

6. In **Configuration**, your settings and their values are shown. The values are the same values in the on-premises Group Policy. Review these settings and their values.

    After you create the Settings Catalog policy, you can change any values.

    Select **Next**.

7. In **Profile info**, enter the following settings:

    - **Name**: Enter a descriptive name for the Setting Catalog profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Windows 10/11: Imported Microsoft Edge GPOs**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    
    Select **Next**.

8. In **Scope tags**, optionally assign a tag to filter the profile to specific IT groups, such as US-NC IT Team or JohnGlenn_ITDepartment. For more information about scope tags, go to [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

9. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, including advice and guidance, go to [Assign user and device profiles in Intune](device-profile-assign.md).

    Select **Next**.

10. In **Review + deploy**, review your settings.

    When you select **Create**, your changes are saved, and the profile is assigned. The policy is shown in the **Devices** > **Configuration profiles** list.

The next time any device within your assigned groups checks for configuration updates, the settings you configured are applied.

## Conflicting settings are detected early

It's possible you have multiple GPOs that include the same setting, and that the setting is set to different values. When you're creating a policy, and selecting your settings in the **Settings to migrate** tab, any conflicting settings show the following error:

`Conflicts are detected for the following settings: <setting name>. Select only one version with the value you prefer in order to continue.`

:::image type="content" source="./media/group-policy-analytics-migrate/conflicting-settings.png" alt-text="Screenshot that shows conflicts are detected error message with the Group Policy Analytics migrate feature in Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/conflicting-settings.png":::

To resolve the conflict, uncheck a conflicting setting, and continue the migration.

## What you need to know

The **Migrate** feature takes the parsed data from the imported Group Policy object (GPO) and translates it to a relevant setting in the Settings Catalog, if the setting exists. 

**Migrate** is best effort. 

When you create the Settings Catalog profile, any settings that can be included in the profile are included. There can be some differences with the imported settings and the settings in Settings Catalog.

- **Some settings have a better configuration experience in Endpoint Security**

  If you import AppLocker settings or Firewall rule settings, then the **Migrate** option is disabled and grayed out. Instead, configure these settings using the Endpoint Security workload in the Intune admin center.

  For more information, go to:
  
  - [Firewall policy in Endpoint Security](../protect/endpoint-security-firewall-policy.md)
  - [Endpoint security firewall rule migration tool overview](../protect/endpoint-security-firewall-rule-tool.md)
  - [Application control policy in Endpoint Security](../protect/endpoint-security-asr-policy.md).

  If you have GPOs that focus on endpoint security, then you should look at the features available in [Endpoint Security](../protect/endpoint-security.md), including Security Baselines and mobile threat defense.

- **Some settings don't migrate exactly, and may use a different setting**

  In some scenarios, some GPO settings don't migrate to the exact same setting in the Settings Catalog. Intune shows an alternate setting that has a similar effect.

  For example, you may see this behavior if you import GPOs that include older Office Administrative Template settings or older Google Chrome settings.

- **Some settings fail to migrate**

  It's possible some errors can happen when the settings are migrating. When the profile is being created, settings that return an error are shown in **Notifications**:

  :::image type="content" source="./media/group-policy-analytics-migrate/notifications.png" alt-text="Screenshot that shows notifications with additional information when the policy is being created in Microsoft Intune.":::

  Some common reasons a setting may show an error include:

  - The setting value is in an unexpected format.
  - A child setting is missing from the imported GPO and is required to configure the parent setting.

## Next steps

- [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Intune](group-policy-analytics.md)
- [Use Windows 10/11 Administrative Templates to configure group policy settings in Microsoft Intune](administrative-templates-windows.md)
- [Use the settings catalog to configure settings on Windows and macOS devices](settings-catalog.md)
