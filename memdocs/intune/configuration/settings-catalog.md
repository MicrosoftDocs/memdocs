---
# required metadata

title: Create a policy using settings catalog in Microsoft Intune
description: Use settings catalog in Microsoft Intune to configure thousands of settings for Windows 10/11, iOS/iPadOS, and macOS client devices, including Microsoft Office apps, Microsoft Edge, and more. Add these settings in a device configuration profile to secure devices, and control different programs and features. Use Microsoft Copilot to create a policy, get impact What If analysis, and learn more about each setting.
keywords: settings catalog, security copilot, intune, microsoft intune
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/21/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano, beflamm, rashok
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices

> [!WARNING]
> This article is being updated to include Copilot.

Settings catalog lists all the settings you can configure, and all in one place. This feature simplifies how you create a policy, and how you see all the available settings. For example, you can use the settings catalog to create a BitLocker policy with all BitLocker settings.

You can also use [Microsoft Copilot in Intune](../fundamentals/copilot-intune-overview.md). When you combine the settings catalog with Copilot, you can use Copilot to:

- Learn more about each setting in the settings catalog.
- Create settings catalog policies using prompts.
- Get impact What If analysis on the settings you configure and the policies you create.

If you prefer to configure settings at a granular level, similar to on-premises Group Policy Objects (GPOs), then the settings catalog is a natural transition to cloud-based policy.

When you create the policy, you start from scratch. You add only the settings you want to control and manage.

Use the settings catalog as part of your mobile device management (MDM) solution to manage and secure devices in your organization. More settings are continually being added to the settings catalog. For a list of the settings, go to the [IntunePMFiles / DeviceConfig GitHub repository](https://github.com/IntunePMFiles/DeviceConfig).

This feature applies to:

- **iOS/iPadOS**

  Includes device settings that are directly generated from Apple Profile-Specific Payload Keys. More settings and keys are continually being added. To learn more about profile-specific payload keys, go to [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's website).

  Apple's declarative device management (DDM) is built into the settings catalog. When you configure settings from the settings catalog on iOS/iPadOS 15+ devices enrolled using [User Enrollment](../enrollment/ios-user-enrollment.md), you're automatically using DDM. If DDM doesn't work for any reason, then these devices use Apple's standard MDM protocol. All other iOS/iPadOS devices continue to use Apple's standard MDM protocol.

- **macOS**

  Includes device settings that are directly generated from Apple Profile-Specific Payload Keys. More settings and keys are continually being added. To learn more about profile-specific payload keys, go to [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's website).

  Apple's declarative device management (DDM) is available in the settings catalog. You can [use DDM to manage software updates](../protect/managed-software-updates-ios-macos.md), passcode restrictions, and more.

- **Windows 10/11**

  There are thousands of settings, including settings that haven't been available before. These settings are directly generated from the Windows configuration service providers (CSPs). You can also configure Administrative Templates, and have more Administrative Template settings available. As Windows adds or exposes more settings to MDM providers, these settings are added quicker to Microsoft Intune for you to configure.

> [!TIP]
>
> - For a list of the settings in the settings catalog, go to the [IntunePMFiles / DeviceConfig GitHub repository](https://github.com/IntunePMFiles/DeviceConfig).
> - To see the Microsoft Edge policies you have configured, open Microsoft Edge, and go to `edge://policy`. Or, if you use Copilot, you can use a prompt like **Show me all the existing policies that configure microsoft edge browser**.

This article lists the steps to create a policy, shows how to search and filter the settings in Intune, and shows how to use Copilot for these tasks.

When you create the policy, it creates a device configuration profile. You can then assign or deploy this profile to devices in your organization.

For information on some features you can configure using the settings catalog, go to [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md).

## Create the policy

# [Settings catalog profile](#tab/create-policy-sc)

You can create the policy using the settings catalog profile type.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Create**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**, **macOS**, or **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **macOS: MSFT Edge settings** or **Win10: BitLocker settings for all Win10 devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select a category to see all the available settings.

    For example, select **Windows 10 and later**, then select **Authentication** to see all the settings in this category:

    :::image type="content" source="./media/settings-catalog/settings-picker-authentication.png" alt-text="Screenshot that shows the Settings Catalog when you select Windows and Authentication in Microsoft Intune and Intune admin center.":::

    For example, select **macOS**. The **Microsoft Edge - All** category lists all the settings you can configure, including any new settings. The other categories include settings that are obsolete, or settings that apply to older versions:

    :::image type="content" source="./media/settings-catalog/macos-settings-picker-edge-all.png" alt-text="Screenshot that shows the Settings Catalog when you select macOS and select a feature or category in Microsoft Intune and Intune admin center.":::

    > [!TIP]
    >
    > - On macOS, the categories are temporarily removed. To find a specific setting, use the **Microsoft Edge - All** category, or search for the setting name. For a list of the setting names, go to [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).
    >
    > - Use the **Learn more** link in the tooltip to see if a setting is obsolete, and to see the supported versions.

8. Select any setting you want to configure. Or, choose **Select all these settings**:

    :::image type="content" source="./media/settings-catalog/settings-picker-select-all-settings.png" alt-text="Screenshot that shows the settings when you select all these settings in Microsoft Intune and Intune admin center.":::

    After you add your settings, close the settings picker. All the settings are shown, and configured with a default value, such as **Block** or **Allow**. These defaults values are the same default values in the OS. If you don't want to configure a setting, then select the minus:

    :::image type="content" source="./media/settings-catalog/default-setting-value-minus-not-configured.png" alt-text="Screenshot that shows the Settings Catalog and that the default values in Microsoft Intune and Intune admin center are the same as the OS default values.":::

    When you select the minus (`-`):

    - Intune doesn't change or update this setting. The minus is the same as **Not configured**. When set to **Not configured**, the setting is no longer managed.
    - The setting is removed from the policy. The next time you open your policy, the setting isn't shown. You can add it again.
    - The next time devices check in, the setting is no longer locked. Another policy or device user can change the policy.

    > [!TIP]
    >
    > - In the Windows setting tooltips, **Learn more** links to the CSP.
    > - When a setting allows multiple values, it's recommended to add each value separately.
    >
    >   For example, you can enter multiple values in the **Bluetooth** > **Services Allowed List** setting. Enter each value on a separate line:
    >   :::image type="content" source="./media/settings-catalog/setting-with-multiple-values.png" alt-text="Screenshot that shows a setting with multiple values on a separate line in the Settings Catalog in Microsoft Intune and the Intune admin center":::
    >
    >   You can add multiple values in a single field, but you may experience a character limit.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

# [Copilot](#tab/create-policy-copilot)

You can create a policy using Copilot prompts.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Copilot**:

    :::image type="content" source="./media/settings-catalog/copilot-devices-configuration-ui.png" alt-text="Screenshot that shows how to open Copilot to create a device configuration policy using the Settings Catalog in Microsoft Intune and Intune admin center.":::

3. In the prompt, enter something like **Create a settings catalog policy that configures all bitlocker settings for Windows 10 devices**. Copilot can show you the settings, can show the values the settings are set to, and can give you a **Draft policy** option:

    :::image type="content" source="./media/settings-catalog/copilot-create-bitlocker-policy.png" alt-text="Screenshot that shows Copilot creating a new BitLocker policy using the Settings Catalog in Microsoft Intune and Intune admin center.":::

4. To start creating the policy, select **Draft policy**. All the settings in your draft policy are shown, and they're typically set to the default value. You can change any setting value and save the policy when you're done.

    :::image type="content" source="./media/settings-catalog/copilot-bitlocker-policy-default-values.png" alt-text="Screenshot that shows Copilot creating a new BitLocker policy with the default setting values using the Settings Catalog in Microsoft Intune and Intune admin center.":::

5. Continue creating the policy and save your changes. In **Assignments**, you can assign the policy to users or groups. Or, you can just save the policy and assign it later. The policy doesn't apply until you assign it.

### Sample Copilot prompts that create a new policy

When creating a policy, we recommend you use the **Generate**, **Draft**, or **Create** keywords in the prompt. These keywords help Copilot and other AI languages understand your intent.

You can also export a policy from another MDM provider and paste the text into Copilot. Copilot uses this text to create a  policy.

Here are some sample prompts to get you started:

- Create an Intune policy that turns on the Windows Firewall.
- Create an Intune policy that blocks users from using any removable storage devices on Windows 11 laptops.
- Draft a policy to prevent autoplay on removable drives.
- Create a policy that configures Microsoft auto update to enforce installation after 14 days on mac devices.
- Generate a policy that hides the shutdown button on the start menu.​
- Draft a policy from this JAMF output `paste the text`.

---

## Find some settings and learn more about each setting

There are thousands of settings available in the settings catalog. To help find the settings you want, you can use the search and filter features in the settings catalog. If you use Copilot, then you can get more Copilot-generated information about each setting.

# [Search and filter](#tab/sc-search-filter)

When you create a new policy or update an existing policy, there are built-in search and filter features to help you find settings.

- In your policy, to find specific settings, you can use **Add settings** > **Search**. You can search by category, such as `browser`, search for a keyword, such as `office` or `google`, and search for specific settings.

  For example, search for `internet explorer`. All the settings with `internet explorer` are shown. Select a category to see the available settings:

  :::image type="content" source="./media/settings-catalog/search-internet-explorer.png" alt-text="Screenshot that shows the Settings Catalog when you search for Internet Explorer to see all the IE settings in Microsoft Intune and Intune admin center.":::

- In your policy, use **Add settings** > **Add filter**. Select the key, operator, and value.

  When you **filter on OS Edition**, you can filter the settings that apply to specific Windows editions:

  :::image type="content" source="./media/settings-catalog/settings-picker-filter-edition.png" alt-text="Screenshot that shows the Settings Catalog when you filter the settings list by Windows edition in Microsoft Intune and Intune admin center.":::

  > [!NOTE]
  > For the Edge, Office, and OneDrive settings, the OS version or edition doesn't determine if the settings apply. So, if you filter to a specific edition, like Windows Professional, then the Edge, Office, and OneDrive settings aren't shown.

  You can also **filter the settings by device or user scope**. For more information on user scope and device scope, go to [Device scope vs. user scope settings](#device-scope-vs-user-scope-settings) (in this article):

  :::image type="content" source="./media/settings-catalog/settings-picker-filter-scope.png" alt-text="Screenshot that shows the user and device scope filter in the settings catalog in Microsoft Intune and Intune admin center.":::

# [Copilot](#tab/copilot-tooltips)

When you use settings catalog policies, you can use Copilot to get more information about a specific setting.

1. In your policy, select **Add settings**. In the Settings Picker, select some settings. For example, in a macOS policy, expand **Declarative Device Management** > **Software Update** > **Select all these settings**. Close the Settings Picker.

2. For the settings, notice the Copilot prompts button:

    :::image type="content" source="./media/settings-catalog/copilot-settings-catalog-policy-tooltip.png" alt-text="Screenshot that shows Copilot tooltip prompts button for on any setting in the Settings Catalog in Microsoft Intune and Intune admin center.":::

3. When you select a Copilot prompts button, more information is shown about the setting. In the prompt, you can ask Copilot more questions, including the effect of the setting:

    :::image type="content" source="./media/settings-catalog/copilot-settings-catalog-policy-details.png" alt-text="Screenshot that shows Copilot giving more detailed information on any setting in the Settings Catalog in Microsoft Intune and Intune admin center.":::

### Sample Copilot prompts to learn more about a setting

- Tell me about this setting.
- What is the impact of this setting?
- What happens if I deploy this setting to my devices?
- Does Microsoft recommend enabling this setting?
- Is this setting configured in any other policies?

---

## Copy a profile  

Select **Duplicate** to create a copy of an existing profile. Duplicating is useful when you need a profile that's similar yet distinct from the original one.

The copy contains the same setting configurations and scope tags as the original profile, but doesn't have assignments attached to it. After you give the new profile a name, you can edit the profile to adjust the settings and add assignments.

1. Go to **Devices** > **Configuration**.
2. Find the profile that you want to copy. Right-click the profile or select the ellipses context menu (`…`).
3. Select **Duplicate**.  
4. Enter a new name and description for the policy.
5. **Save** your changes.

## Import and export a profile

This feature applies to:

- Windows 10 and later

When you create a settings catalog policy, you can export the policy to a `.json` file. You can then import this file to create a new policy. This feature is useful if you want to create a policy that's similar to an existing policy. For example, you export a policy, import it to create a new policy, and then make changes to the new policy.

1. Go to **Devices** > **Configuration**.

2. To export an existing policy, select the profile > select the ellipsis context menu (`…`) > **Export JSON**:

    :::image type="content" source="./media/settings-catalog/export-settings-catalog-policy.png" alt-text="Screenshot that shows how to export a settings catalog policy as JSON in Microsoft Intune and Intune admin center.":::

3. To import a previously exported settings catalog policy, select **Create** > **Import policy**:

    :::image type="content" source="./media/settings-catalog/import-settings-catalog-policy.png" alt-text="Screenshot that shows how to import an existing settings catalog policy in Microsoft Intune and Intune admin center.":::

    Select the JSON file you exported and name your new policy. **Save** your changes.

## Conflicts and reporting

Conflicts happen when the same setting is updated to different values, including policies configured using the settings catalog. In the Intune admin center, you can check the status of your existing policies. The data refreshes automatically, and operates in near real time.

There are built-in features that can help you troubleshoot conflicts, including per-setting status reporting. If you use Copilot, then you can use prompts to help avoid conflicts and get more information on existing policies.

# [Reporting and troubleshooting](#tab/sc-reporting)

In the Intune admin center, you can use the built-in reporting features to help find and resolve conflicts.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration**. In the list, select the policy you created using the Settings Catalog. The **Profile type** column shows **Settings Catalog**:

    :::image type="content" source="./media/settings-catalog/profile-type-shows-settings-catalog.png" alt-text="Screenshot that shows how to open the settings catalog in Microsoft Intune and Intune admin center.":::

2. When you select the policy, the device status shows. It shows a summary of your policy state and the policy properties. You can also change or update your policy in the **Configuration settings** section:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-device-status-report.png" alt-text="Screenshot that shows how to select the settings catalog policy to see the device status, policy state, and properties in Microsoft Intune and Intune admin center.":::

3. Select **View report**. The report shows detailed information, including the device name, the policy status, and more. You can also filter on the deployment status, and **Export** the report to a `.csv` file:

    :::image type="content" source="./media/settings-catalog/settings-catalog-policy-view-report.png" alt-text="Screenshot that shows how to see detailed report information in Microsoft Intune and Intune admin center, including device name, policy status, and more." lightbox="./media/settings-catalog/settings-catalog-policy-view-report.png":::

4. You can also look at the states of each setting using the **per-setting status**. This status shows the total number of devices affected by each setting in the policy.

    You can:

    - See the number of devices with the setting successfully applied, in conflict, or in error.
    - Select the number of devices in compliance, conflict, or error. And, see a list of users or devices in that state.
    - Search, sort, filter, export, and go to the next and previous pages.

5. In the admin center, select **Devices** > **Monitor** > **Assignment failures**. If your Settings Catalog policy failed to deploy because of an error or conflict, it shows in this list. You can also **Export** to a `.csv` file.

6. Select the policy to see the devices. Then, select a specific device to see the setting that failed, and a possible error code.

> [!TIP]
> [Intune reports](../fundamentals/reports.md) is a great resource, and describes all the reporting features you can use. For information on all the reporting data you can view, go to [Intune reports](../fundamentals/reports.md).

For more information on conflict resolution, go to:

- [Monitor device profiles](device-profile-monitor.md#view-conflicts)
- [Common questions and answers with device policies](device-profile-troubleshoot.md)

# [Copilot](#tab/copilot-conflicts)

Copilot can help you find the status of your existing policies, find the status of a specific setting in your policy, and show any potential conflicts.

**To help avoid conflicts**, you can ask questions like:

- Will this policy cause any conflicts?
- Is this setting configured in any other policies?
- Will this setting cause a conflict?

**To get reporting-like information on existing policies**, you can use prompts like:

- Summarize the policy "Contoso Windows 10 security"​.
- Show policies that contain encryption settings​. Describe their impact on end users.
- Describe the impact of this policy on security. Format the output in bullets instead of a table.
- Create a summary of this change for my Change Advisory Board meeting today. Include the full scope (users and devices), summary of the settings in the policy, and possible risks to security or user productivity.

---

## Settings catalog vs. templates

When you create the policy, you have two policy types: **Settings catalog** and **Templates**:

:::image type="content" source="./media/settings-catalog/select-windows-policy-type.png" alt-text="Screenshot that shows when you create a Windows or macOS policy, select settings catalog or templates in Microsoft Intune and Intune admin center.":::

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

When a device checks in to Intune, the device always presents a `deviceID`. The device might or might not present a `userID`, depending on the check-in timing and if a user is signed in.

The following list includes some possible combinations of scope, assignment, and the expected behavior:

- If a device scope policy is assigned to a device, then all users on that device have that setting applied.
- If a device scoped policy is assigned to a user, once that user signs in and an Intune sync occurs, then the device scope settings apply to all users on the device.
- If a user scope policy is assigned to a device, then all users on that device have that setting applied. This behavior is like a [loopback set to merge](/troubleshoot/windows-server/group-policy/loopback-processing-of-group-policy).
- If a user scoped policy is assigned to a user, then only that user has that setting applied.
- There are some settings that are available in the user scope and the device scope. If one of these settings is assigned to both user and device scope, then user scope takes precedence over device scope.

If there isn't a [user hive](/windows/win32/sysinfo/registry-hives) during initial check-ins, then you can see some user scope settings marked as not applicable. This behavior happens in the early moments of a device before a user is present.

## Next steps

- [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md)
- [Create a Universal Print policy in Microsoft Intune](settings-catalog-printer-provisioning.md)
- Be sure to [assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
- [Overview of Microsoft Copilot for Intune](../fundamentals/copilot-intune-overview.md)
