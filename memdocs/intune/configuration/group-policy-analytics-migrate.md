---
# required metadata

title: Migrate your imported group policy to a policy in Microsoft Intune
description: After you import your group policy objects in Microsoft Intune and Endpoint Manager, use the migrate feature to create a Settings Catalog policy. This policy will use your imported GPOs, and can be assigned to users and devices managed by your organizations.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 04/18/2022
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
  - M365-identity-device-management
  - highpri
---

# Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager (public preview)

You can import your on-premises Group Policy Objects (GPOs), and create an Intune policy using these imported settings. This policy can be deployed to users and devices managed by your organization.

With Group Policy Analytics, you import your on-premises GPOs. It analyzes your imported GPOs, and shows the settings that are also available in Microsoft Intune. For the settings that are available, you can create a Settings Catalog policy, and then deploy the policy.

This article shows you how to create the policy from your imported GPOs. For more information and an overview on Group Policy Analytics, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md).

## Before you begin

- In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in as the Intune administrator or with a role that has the **Security Baselines** permission.

  For example, the **Endpoint Security Manager** role has the **Security Baselines** permission. For more information on the built-in roles, see [role-based access control](../fundamentals/role-based-access-control.md).

- Import your on-premises GPOs, and review the results.

  For the specific steps, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md).

- This feature is in public preview. For more information, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

- Currently, the Migrate feature isn't supported in sovereign clouds. For more information on sovereign clouds, see [What is Azure Government?](/azure/azure-government/documentation-government-welcome).

## Review and migrate your GPOs to a Settings Catalog policy

After you import your GPOs, review the settings that can be migrated. Remember, some settings don't make sense on cloud native endpoints, like Windows 10/11 devices. After they've been reviewed, you can migrate the settings to a Settings Catalog policy.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)**.
2. In the list, your imported GPOs are shown. Next to the GPO you want in your Settings Catalog profile, select the **Migrate** checkbox. You can select one GPO or many GPOs:

    :::image type="content" source="./media/group-policy-analytics-migrate/select-migrate-checkbox-imported-gpo.png" alt-text="Select the Migrate checkbox next to your imported GPO in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-migrate-checkbox-imported-gpo.png":::

3. To see all the settings in your imported GPO, select **Migrate**:

    :::image type="content" source="./media/group-policy-analytics-migrate/select-migrate-see-all-settings.png" alt-text="Select the Migrate button to see all the settings in your imported GPO in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-migrate-see-all-settings.png":::

4. In the **Settings to migrate** tab, select the **Migrate** column for the settings you want to include in your Settings Catalog profile:

      :::image type="content" source="./media/group-policy-analytics-migrate/settings-to-migrate-tab.png" alt-text="In the Settings to migrate, select the Migrate checkbox in Endpoint Manager and Microsoft Intune.":::

    To help you pick the settings, you can use the built-in features:

    - **Select all on this page**: Select this option if you want all settings on the existing page to be included in your Settings Catalog profile.  

      :::image type="content" source="./media/group-policy-analytics-migrate/select-all-on-this-page.png" alt-text="Use the Select all on this page button to include all page settings in Group Policy Analytics migrate feature in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/select-all-on-this-page.png":::

    - **Search by setting name**: Enter the setting name to find the settings you want:

      :::image type="content" source="./media/group-policy-analytics-migrate/search-by-setting-name.png" alt-text="Search for the setting name in Group Policy Analytics migrate feature in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/search-by-setting-name.png":::

    - **Sort**: Sort your settings using the column names:

      :::image type="content" source="./media/group-policy-analytics-migrate/sort-using-column-names.png" alt-text="Sort the settings using the Migrate, Setting name, Group policy setting category, MDM support, value, scope, min OS version, and CSP name Group Policy Analytics migrate feature in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/sort-using-column-names.png":::

    > [!TIP]
    > If you haven't already, review your Group Policy settings. It's possible some settings don't apply to cloud-based policy management or don't apply to cloud native endpoints, like Windows 10/11 devices. It's not recommended to include all your Group Policy settings without reviewing them.

5. Select **Next**.
6. In **Configuration**, your settings and their values are shown. The values are the same values in the on-premises Group Policy. Review these settings and their values.

    After you create the Settings Catalog policy, you can change any values.

    Select **Next**.

7. In **Profile info**, enter the following settings:

    - **Name**: Enter a descriptive name for the Setting Catalog profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Windows 10/11: Imported Microsoft Edge GPOs**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

8. Select **Next**.
9. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, including advice and guidance, see [Assign user and device profiles in Intune](device-profile-assign.md).

    Select **Next**.

10. In **Review + deploy**, review your settings.

    When you select **Create**, your changes are saved, and the profile is assigned. The policy is shown in the **Devices** > **Configuration profiles** list.

The next time any device within your assigned groups checks for configuration updates, the settings you configured are applied.

## Conflicting settings are detected early

It's possible you have multiple GPOs that include the same setting, and that the setting is set to different values. When you're creating a policy, and selecting your settings in the **Settings to migrate** tab, any conflicting settings will show the following error:

`Conflicts are detected for the following settings: <setting name>. Select only one version with the value you prefer in order to continue.`

:::image type="content" source="./media/group-policy-analytics-migrate/conflicting-settings.png" alt-text="Conflicts are detected error message with Group Policy Analytics migrate feature in Endpoint Manager and Microsoft Intune." lightbox="./media/group-policy-analytics-migrate/conflicting-settings.png":::

To resolve the conflict, uncheck a conflicting setting, and continue the migration.

## What you need to know

The **Migrate** feature takes the parsed data from the imported Group Policy object (GPO) and translates it to a relevant setting in the Settings Catalog, if the setting exists. 

**Migrate** is best effort. 

When you create the Settings Catalog profile, any settings that can be included in the profile will be included. There can be some differences with the imported settings and the settings in Settings Catalog.

- **Some settings fail to migrate**

  It's possible there will be some errors when the settings are migrating. When the profile is being created, settings that return an error are shown in **Notifications**:

  :::image type="content" source="./media/group-policy-analytics-migrate/notifications.png" alt-text="Notifications shows additional information when the policy is being created in Endpoint Manager and Microsoft Intune.":::

  Some common reasons a setting may show an error include:

  - The setting value is in an unexpected format.
  - A child setting is missing from the imported GPO and is required to configure the parent setting.

- **Some settings don't migrate exactly, and may use a different setting**

  In some scenarios, some GPO settings won't migrate to the exact same setting in the Settings Catalog. An alternate setting that has a similar impact is recommended.

  For example, you may see this behavior if you import GPOs that include older Office Administrative Template settings or older Google Chrome settings.

## Next steps

- [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md)
- [Use Windows 10/11 Administrative Templates to configure group policy settings in Microsoft Endpoint Manager](administrative-templates-windows.md)
- [Use the settings catalog to configure settings on Windows and macOS devices - preview](settings-catalog.md)
