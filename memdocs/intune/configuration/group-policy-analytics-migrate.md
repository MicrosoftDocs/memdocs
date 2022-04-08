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

You can import your on-premises Group Policy Objects (GPOs), and create an Intune policy. This policy can be deployed to users and devices managed by your organization.

With Group Policy Analytics, you import your on-premises GPOs. This tool analyzes your imported GPOs, and shows the settings that are also available in Microsoft Intune. For the settings that are available, you can create a Settings Catalog policy, and then deploy the policy.

This article shows you how to create the policy from your imported GPOs. For more information and an overview on Group Policy Analytics, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md).

## Before you begin

- In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in as the Intune administrator or with a role that has the **Security Baselines** permission.

  For example, the **Endpoint Security Manager** role has the **Security Baselines** permission. For more information on the built-in roles, see [role-based access control](../fundamentals/role-based-access-control.md).

- Import your on-premises GPOs, and run analysis. The settings with a **Ready for migration** status can be migrated. 

  For the specific steps, go to [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md).

- This feature is in public preview. For more information on what that means, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

- Currently, the Migrate functionality isn't supported in sovereign clouds. For more information on sovereign clouds, see [What is Azure Government?](https://docs.microsoft.com/azure/azure-government/documentation-government-welcome).

## Migrate your GPOs to a Settings Catalog policy

Group Policy analytics shows the settings that are **Ready for migration**. These settings can be migrated to a Settings Catalog policy. 

Once you’ve assessed your Group Policy analytics data on settings that are Ready for migration, Not supported, and Deprecated, you can create a Settings Catalog profile using the “Migrate” capability in Group Policy analytics: 

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Group Policy analytics (preview)**.
2. In the list, your imported GPOs are shown. Select the GPOs you want in your Settings Catalog profile. You can select one GPO or many GPOs.

    INSERT SCREEN SHOT

3. Select **Migrate**:

    INSERT SCREEN SHOT

4. In the **Settings to Migrate** column, select the settings you want to include in your Settings Catalog profile. To help you pick the settings, you can use the built-in features:

    - **Select all on this page**: Select this option if you want all settings on the existing page to be included in your Settings Catalog profile.  
    - **Search bar**: Enter the setting name to find the settings you want.
    - **Sort**: Sort using the Migrate, Setting Name, Group Policy Setting Category, MDM Support, Value, Scope, Min OS version, CSP name columns.

    > [!TIP]
    > If you haven't already, review your Group Policy settings. It's possible some settings don't apply to cloud-based policy management or don't apply to cloud-native endpoints, like Windows 10/11 devices. It's not recommended to include all your Group Policy without reviewing them.

5. Select **Next**.
6. In **Configuration**, your settings and their values are shown. The values are the same values in the on-premises Group Policy. Review these settings and their values. 

    Select **Next**.

    After you create the Settings Catalog  policy, you can change any values.

7. In **Profile**, enter the following settings:

    - **Name**: Enter a descriptive name for the Setting Catalog profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Windows 10/11: Imported Microsoft Edge GPOs**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

8. Select **Next**.
9. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles in Intune](device-profile-assign.md).

    Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the **Devices** tab > profiles list.

The next time any device within your assigned groups checks for configuration updates, the settings you configured are applied. 

## Known issues

### Conflicting settings during migration

It's possible you have multiple GPOs that include the same setting, and that the setting is set to different values. When you select these conflicting settings, these settings show the following error:

`INSERT ERROR MESSAGE`

You need to resolve this conflict before migrating the GPOs. You can do resolve the conflict when creating the Settings Catalog policy. In the **Settings to Migrate** column, uncheck the conflicting setting, an


When selecting settings to migrate, you may hit the scenario where there is a setting that is selected twice, each time with a different value. This may be more likely to occur in the event you have selected multiple GPOs to run through the “Migrate” functionality.  

If more than one of the same setting is selected for migrate with a conflicting value, you will see an error message indicating that you must specify a single value for each specified setting before proceeding in your profile creation process. Please resolve this on the “Settings to Migrate” tab before hitting “Next”.

### Settings fail to migrate

The “Migrate” functionality takes what is parsed from the imported Group Policy object (GPO) and translates it into the relevant setting (if one exists) in Settings Catalog. Given the variation between settings that can be imported, and what the Settings Catalog expects, there may occasionally be some errors during the process. The “Migrate” functionality is best effort – this means that when creating a Settings Catalog profile, any settings that can be included in the profile will be included. Settings that throw an error during profile creation get surfaced via the Notifications pane in Microsoft Endpoint Manager. Some reasons a setting may throw an error is: 

- If the value for a setting is in an unexpected format. 

- If a child setting is missing from the imported GPO but required to configure the parent setting. 

- < Other scenarios >

### Alternative technology available  

In some cases, in the “MDM Support” column, settings may be identified as having MDM Support, however, the exact same setting as it was configured in Group Policy no longer makes sense to use in MDM. For example, you may see this for older Office Administrative Template settings, or for Google Chrome settings that have an equivalent setting in Microsoft Edge.

## Next steps

- [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](group-policy-analytics.md)
- [Use Windows 10/11 Administrative Templates to configure group policy settings in Microsoft Endpoint Manager](administrative-templates-windows.md)
