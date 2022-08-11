---
# required metadata

title: Create a policy using settings catalog in Microsoft Intune
description: Use settings catalog in Microsoft Intune and Endpoint Manager to configure thousands of settings for Windows 10/11, iOS/iPadOS, and macOS client devices, including Microsoft Office apps, Microsoft Edge, and more. Add these settings in a device configuration profile to secure devices, and control different programs and features.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices

Settings catalog lists all the settings you can configure, and all in one place. This feature simplifies how you create a policy, and how you see all the available settings. More settings are continually being added. If you prefer to configure settings at a granular level, similar to on-premises GPO, then the settings catalog is a natural transition.

When you create the policy, you start from scratch. You add only the settings you want to control and manage. For example, you can use the settings catalog to create a BitLocker policy with all BitLocker settings, and all in one place in Intune.

Use the settings catalog as part of your mobile device management (MDM) solution to manage and secure devices in your organization.

This feature applies to:

- **iOS/iPadOS**

  Includes device settings that are directly generated from Apple Profile-Specific Payload Keys. More settings and keys are continually being added. To learn more about profile-specific payload keys, go to [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's website).

  Apple's declarative device management (DDM) is built into the settings catalog. When you configure settings from the settings catalog on iOS/iPadOS 15+ devices enrolled using [User Enrollment](../enrollment/ios-user-enrollment.md), you're automatically using DDM. If DDM doesn't work for any reason, then these devices use Apple’s standard MDM protocol. All other iOS/iPadOS devices continue to use Apple’s standard MDM protocol.

- **macOS**

  Includes device settings that are directly generated from Apple Profile-Specific Payload Keys. More settings and keys are continually being added. To learn more about profile-specific payload keys, go to [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's website).

- **Windows 10/11**

  There are thousands of settings, including settings that haven't been available before. These settings are directly generated from the Windows configuration service providers (CSPs). You can also configure Administrative Templates, and have more Administrative Template settings available. As Windows adds or exposes more settings to MDM providers, these settings are added quicker to Microsoft Intune for you to configure.

> [!TIP]
> To see the Microsoft Edge policies you have configured, open Microsoft Edge, and go to `edge://policy`.

This article lists the steps to create a policy, and shows how to search and filter the settings in Intune. When you create the policy, it creates a device configuration profile. You can then assign or deploy this profile to devices in your organization.

For information on some features you can configure using the settings catalog, go to [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md).

## Create the policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**, or select **Windows 10 and later**.
    - **Profile**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **macOS: MSFT Edge settings** or **Win10: BitLocker settings for all Win10 devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select a category to see all the available settings.

    For example, select **Windows 10 and later**, then select **Authentication** to see all the settings in this category:

    :::image type="content" source="./media/settings-catalog/settings-picker-authentication.png" alt-text="Screenshot that shows the Settings Catalog when you select Windows and Authentication in Microsoft Intune and Endpoint Manager admin center.":::

    For example, select **macOS**. The **Microsoft Edge - All** category lists all the settings you can configure, including any new settings. The other categories include settings that are obsolete, or settings that apply to older versions:

    :::image type="content" source="./media/settings-catalog/macos-settings-picker-edge-all.png" alt-text="Screenshot that shows the Settings Catalog when you select macOS and select a feature or category in Microsoft Intune and Endpoint Manager admin center.":::

    > [!TIP]
    >
    > - On macOS, the categories are temporarily removed. To find a specific setting, use the **Microsoft Edge - All** category, or search for the setting name. For a list of the setting names, go to [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).
    > 
    > - Use the **Learn more** link in the tooltip to see if a setting is obsolete, and to see the supported versions.

8. Select any setting you want to configure. Or, choose **Select all these settings**:

    :::image type="content" source="./media/settings-catalog/settings-picker-select-all-settings.png" alt-text="Screenshot that shows the settings when you select all these settings in Microsoft Intune and Endpoint Manager admin center.":::

    After you add your settings, close the settings picker. All the settings are shown, and configured with a default value, such as **Block** or **Allow**. These defaults values are the same default values in the OS. If you don't want to configure a setting, then select the minus:

    :::image type="content" source="./media/settings-catalog/default-setting-value-minus-not-configured.png" alt-text="Screenshot that shows the Settings Catalog and that the default values in Microsoft Intune and Endpoint Manager admin center are the same as the OS default values.":::

    When you select the minus (`-`):

    - Intune doesn't change or update this setting. The minus is the same as **Not configured**. When set to **Not configured**, the setting is no longer managed.
    - The setting is removed from the policy. The next time you open your policy, the setting isn't shown. You can add it again.
    - The next time devices check in, the setting is no longer locked. It can be changed by another policy or by the device user.

    > [!TIP]
    > In the Windows setting tooltips, **Learn more** links to the CSP.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Find some settings

There are thousands of settings available in the settings catalog. To make it easier to find specific settings, use the built-in features:

- In your policy, use **Add settings** > **Search** to find specific settings. You can search by category, such as `browser`, search for a keyword, such as `office` or `google`, and search for specific settings.

  For example, search for `internet explorer`. All the settings with `internet explorer` are shown. Select a category to see the available settings:

  :::image type="content" source="./media/settings-catalog/search-internet-explorer.png" alt-text="Screenshot that shows the Settings Catalog when you search for Internet Explorer to see all the IE settings in Microsoft Intune and Endpoint Manager admin center.":::

- In your policy, use **Add settings** > **Add filter**. Select the key, operator, and value.

  When you **filter on OS Edition**, you can filter the settings that apply to specific Windows editions:

  :::image type="content" source="./media/settings-catalog/settings-picker-filter-edition.png" alt-text="Screenshot that shows the Settings Catalog when you filter the settings list by Windows edition in Microsoft Intune and Endpoint Manager admin center.":::

  > [!NOTE]
  > For the Edge, Office, and OneDrive settings, the OS version or edition doesn't determine if the settings apply. So, if you filter to a specific edition, like Windows Professional, then the Edge, Office, and OneDrive settings aren't shown.

  You can also **filter the settings by device or user scope**. For more information on user scope and device scope, go to [Device scope vs. user scope settings](#device-scope-vs-user-scope-settings) (in this article):

  :::image type="content" source="./media/settings-catalog/settings-picker-filter-scope.png" alt-text="Screenshot that shows the user and device scope filter in the settings catalog in Microsoft Intune and Endpoint Manager admin center.":::  

## Copy a profile  

Select **Duplicate** to create a copy of an existing profile. Duplicating is useful when you need a profile that's similar yet distinct from the original one. The copy contains the same setting configurations and scope tags as the original profile, but doesn't have assignments attached to it. After you give the new profile a name, you can edit the profile to adjust the settings and add assignments.

1. Go to **Devices** > **Configuration profiles**.
2. Find the profile that you want to copy. Right-click the profile or select the ellipses context menu (**…**).
3. Select **Duplicate**.  
4. Enter a new name and description for the policy.
5. **Save** your changes.

## Reporting and conflicts

You create the policy, and assign it to your groups. In the Endpoint Manager admin center, you can check the status of your policy. The data refreshes automatically, and operates in near real time.

1. In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Device configuration profiles**. In the list, select the policy you created using the Settings Catalog. The **Profile type** column shows **Settings Catalog**:

    :::image type="content" source="./media/settings-catalog/profile-type-shows-settings-catalog.png" alt-text="Screenshot that shows how to open the settings catalog in Microsoft Intune and Endpoint Manager admin center.":::

2. When you select the policy, the device status shows. It shows a summary of your policy state and the policy properties. You can also change or update your policy in the **Configuration settings** section:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-device-status-report.png" alt-text="Screenshot that shows how to select the settings catalog policy to see the device status, policy state, and properties in Microsoft Intune and Endpoint Manager admin center.":::

3. Select **View report**. The report shows detailed information, including the device name, the policy status, and more. You can also filter on the deployment status, and **Export** the report to a `.csv` file:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-view-report.png" alt-text="Screenshot that shows how to see detailed report information in Microsoft Intune and Endpoint Manager admin center, including device name, policy status, and more." lightbox="./media/settings-catalog/settings-catalog-policy-view-report.png":::

4. You can also look at the states of each setting using the **per-setting status**. This status shows the total number of devices affected by each setting in the policy.

    You can:

    - See the number of devices with the setting successfully applied, in conflict, or in error.
    - Select the number of devices in compliance, conflict, or error. And, see a list of users or devices in that state.
    - Search, sort, filter, export, and go to the next and previous pages.

5. In the admin center, select **Devices** > **Monitor** > **Assignment failures**. If your Settings Catalog policy failed to deploy because of an error or conflict, it will show in this list. You can also **Export** to a `.csv` file.

6. Select the policy to see the devices. Then, select a specific device to see the setting that failed, and a possible error code.

> [!TIP]
> [Intune reports](../fundamentals/reports.md) is a great resource, and describes all the reporting features you can use. For information on all the reporting data you can view, go to [Intune reports](../fundamentals/reports.md).

### Conflicts

Conflicts happen when the same setting is updated to different values. Conflicts can also happen with policies configured using the settings catalog. For more information on conflict resolution, see:

- [Monitor device profiles](device-profile-monitor.md#view-conflicts)
- [Common questions and answers with device policies](device-profile-troubleshoot.md)

## Settings catalog vs. templates

When you create the policy, you have two policy types: **Settings catalog** and **Templates**:

:::image type="content" source="./media/settings-catalog/select-windows-policy-type.png" alt-text="Screenshot that shows when you create a Windows or macOS policy, select settings catalog or templates in Microsoft Intune and Endpoint Manager admin center.":::

The **Templates** include a logical group of settings, such as kiosk, VPN, Wi-Fi, and more. Use this option if you want to use these groupings to configure your settings.

The **Settings catalog** lists all the available settings. If you want to see all the available Firewall settings, or all the available BitLocker settings, then use this option. Also, use this option if you're looking for specific settings.

## Device scope vs. user scope settings

When you select a setting, some settings have a `(User)` tag or `(Device)` tag in the setting name, such as `Allow EAP Cert SSO (User)` or `Grouping (Device)`. When you see these tags, the policy only affects the user scope or the device scope.

For more information on user scope and device scope, see the [Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider).

Device and user groups are used when you assign your policies. Device and user scopes describe how a policy is enforced.

### Scope assignment behavior

When deploying policy from Intune, you can assign user scope or device scope to any type of target group. Behavior of the policy per user depends on the scope of the setting:

- User scoped policy writes to `HKEY_CURRENT_USER (HKCU)`. 
- Device scoped policy writes to `HKEY_LOCAL_MACHINE (HKLM)`.

When a device checks in to Intune, the device always presents a `deviceID`. The device may or may not present a `userID`, depending on the check-in timing and if a user is signed in.

The following list includes some possible combinations of scope, assignment, and the expected behavior:

- If a device scope policy is assigned to a device, then all users on that device have that setting applied.
- If a device scoped policy is assigned to a user, once that user signs in and an Intune sync occurs, then the device scope settings apply to all users on the device.
- If a user scope policy is assigned to a device, then all users on that device have that setting applied. This behavior is like a [loopback set to merge](/troubleshoot/windows-server/group-policy/loopback-processing-of-group-policy).
- If a user scoped policy is assigned to a user, then only that user has that setting applied.
- There are some settings that are available in the user scope and the device scope. If one of these settings is assigned to both user and device scope, then user scope takes precedence over device scope.

If there isn't a [user hive](/windows/win32/sysinfo/registry-hives) during initial check-ins, then you may see some user scope settings marked as not applicable. This behavior happens in the early moments of a device before a user is present.

## Next steps

- [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md)
- [Create a Universal Print policy in Microsoft Intune](settings-catalog-printer-provisioning.md)
- Be sure to [assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
