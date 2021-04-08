---
# required metadata

title: Create a policy using settings catalog in Microsoft Intune - Azure | Microsoft Docs
description: Use settings catalog in Microsoft Intune and Endpoint Manager to configure thousands of settings for Windows 10 devices, and configure Microsoft Edge on macOS devices. Add these settings in a device configuration profile to secure devices, and control different programs and features.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/22/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the settings catalog to configure settings on Windows and macOS devices - preview

Settings catalog lists all the settings you can configure, and all in one place. This feature simplifies how you create a policy, and how you see all the available settings. More settings are continually being added.

When you create the policy, you start from scratch. You add only the settings you want to control and manage. For example, you can use the settings catalog to create a BitLocker policy with all BitLocker settings, and all in one place in Intune.

Use the settings catalog as part of your mobile device management (MDM) solution to manage and secure devices in your organization.

This feature applies to:

- **macOS**

  Configure Microsoft Edge version 77 and newer. Previously, you had to [use a property list (plist) file](/deployedge/configure-microsoft-edge-on-mac) (opens another Microsoft website). For a list of the settings you can configure, see [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies) (opens another Microsoft website). Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then it's recommended to continue using the [preference file](preference-file-settings-macos.md).

- **Windows 10 and newer**

  There are thousands of settings to choose, including settings that haven't been available before. These settings are directly generated from the Windows configuration service providers (CSPs). You can also configure Administrative Templates, and have more Administrative Template settings available. As Windows adds or exposes more settings to MDM providers, these settings are added quicker to Microsoft Intune for you to configure.

> [!TIP]
> To see the Microsoft Edge policies you have configured, open Microsoft Edge, and go to `edge://policy`.

This article lists the steps to create a policy, and shows how to search and filter the settings in Intune. When you create the policy, it creates a device configuration profile. You can then assign or deploy this profile to devices in your organization.

## Create the policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**, or select **Windows 10 and later**.
    - **Profile**: Select **Settings catalog (preview)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **macOS: MSFT Edge v77 settings** or **Win10: BitLocker settings for all Win10 devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select a category to see all the available settings.

    For example, choose **Windows 10 and later**, then select **Authentication** to see all the settings in this category:

    :::image type="content" source="./media/settings-catalog/settings-picker-authentication.png" alt-text="In Settings Catalog, select Windows and select Authentication in Microsoft Intune and Endpoint Manager admin center.":::

    For example, choose **macOS**. The **Microsoft Edge - All** category lists all the settings you can configure, including any new settings. The other categories include settings that are obsolete, or settings that apply to older versions:

    :::image type="content" source="./media/settings-catalog/macos-settings-picker-edge-all.png" alt-text="In Settings Catalog, select macOS, and select a feature or category in Microsoft Intune and Endpoint Manager admin center.":::

    > [!TIP]
    >
    > - On macOS, the categories are temporarily removed. To find a specific setting, use the **Microsoft Edge - All** category, or search for the setting name. For a list of the setting names, go to [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).
    > 
    > - Use the **Learn more** link in the tooltip to see if a setting is obsolete, and to see the supported versions.

8. Select any setting you want to configure. Or, choose **Select all these settings**:

    :::image type="content" source="./media/settings-catalog/settings-picker-select-all-settings.png" alt-text="In Settings Catalog, choose select all these settings in Microsoft Intune and Endpoint Manager admin center.":::

    After you add your settings, close the settings picker. All the settings are shown, and configured with a default value, such as **Block** or **Allow**. These defaults values are the same default values in the OS. If you don't want to configure a setting, then select the minus:

    :::image type="content" source="./media/settings-catalog/default-setting-value-minus-not-configured.png" alt-text="In Settings Catalog, the default value in Microsoft Intune and Endpoint Manager admin center is the same as the OS default value.":::

    When you select the minus:

    - Intune doesn't change or update this setting. The minus is the same as **Not configured**. When set to **Not configured**, the setting is no longer managed.
    - The setting is removed from the policy. The next time you open your policy, the setting isn't shown. You can add it again.
    - The next time devices check in, the setting is no longer locked. It can be changed by another policy or by the device user.

    > [!TIP]
    > In the Windows setting tooltips, **Learn more** links to the CSP.

9. Select **Next**.
10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Find some settings

There are thousands of settings available in the settings catalog. To make it easier to find specific settings, use the built-in features:

- In your policy, use **Add settings** > **Search** to find specific settings. You can search by category, such as `browser`, search for a keyword, such as `office`, and search for specific settings.

  For example, search for `internet explorer`. All the settings with `internet explorer` are shown. Select a category to see the available settings:

  :::image type="content" source="./media/settings-catalog/search-internet-explorer.png" alt-text="In Settings Catalog, search for Internet Explorer to see all the settings in Microsoft Intune and Endpoint Manager admin center.":::

- In your policy, use **Add settings** > **Add filter**. Select the key, operator, and value. In **value**, you can filter to only show the settings that apply to Holographic for Business, Windows Enterprise, and other editions:

  :::image type="content" source="./media/settings-catalog/settings-picker-filter-edition.png" alt-text="In Settings Catalog, filter the settings list by Windows edition in Microsoft Intune and Endpoint Manager admin center.":::

## Reporting and conflicts

You create the policy, and assign it to your groups. In the Endpoint Manager admin center, you can check the status of your policy. The data refreshes automatically, and operates in near real time.

1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Device configuration profiles**. In the list, select the policy you created using the Settings Catalog. The **Profile type** column shows **Settings Catalog**:

    :::image type="content" source="./media/settings-catalog/profile-type-shows-settings-catalog.png" alt-text="In Microsoft Intune and Endpoint Manager admin center, the profile type shows Settings Catalog.":::

2. When you select the policy, the device status shows. It shows a summary of your policy state and the policy properties. You can also change or update your policy in the **Configuration settings** section:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-device-status-report.png" alt-text="Select the settings catalog policy to see the device status, policy state, and properties in Microsoft Intune and Endpoint Manager admin center.":::

3. Select **View report**. The report shows detailed information, including the device name, the policy status, and more. You can also filter on the deployment status, and **Export** the report to a `.csv` file:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-view-report.png" alt-text="See detailed report information in Microsoft Intune and Endpoint Manager admin center, including device name, policy status, and more.":::

4. In the admin center, select **Devices** > **Monitor** > **Assignment failures**. If your Settings Catalog policy failed to deploy because of an error or conflict, it will show in this list. You can also **Export** to a `.csv` file.

5. Select the policy to see the devices. Then, select a specific device to see the setting that failed, and a possible error code.

> [!TIP]
> [Intune reports](../fundamentals/reports.md) is a great resource, and describes all the reporting features you can use.

### Conflicts

Conflicts happen when the same setting is updated to different values. Conflicts can also happen with policies configured using the settings catalog. For more information on conflict resolution, see:

- [Monitor device profiles](device-profile-monitor.md#view-conflicts)
- [Common questions and answers with device policies](device-profile-troubleshoot.md)

## Settings catalog vs. templates

When you create the policy, you have two policy types: **Settings catalog** and **Templates**:

:::image type="content" source="./media/settings-catalog/select-windows-policy-type.png" alt-text="When you create a Windows or macOS policy, select settings catalog or templates in Microsoft Intune and Endpoint Manager admin center.":::

The **Templates** include a logical group of settings, such as device restrictions, kiosk, and more. Use this option if you want to use these groupings to configure your settings.

For Windows, the **Settings catalog** lists all the available settings. If you want to see all the available Firewall settings, or all the available BitLocker settings, then use this option. Also, use this option if you're looking for specific settings.

## Next steps

- Be sure to [assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

- For more information on device configuration policies, see [Device configuration overview](device-profiles.md) and [Create a device profile](device-profile-create.md).

- For information on all the reporting data you can view, go to [Intune reports](../fundamentals/reports.md).
