---
title: Configure security baseline policies in Microsoft Intune
description: Deploy security baselines that establish a default and recommended security postures on Windows devices you manage with Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 06/02/2025
ms.topic: concept-article
ms.reviewer: juidaewo
  - intune-azure
ms.collection:
- M365-identity-device-management
- ContentEnagagementFY24
- sub-secure-endpoints
---

# Manage security baseline profiles in Microsoft Intune

To help protect your users and Windows devices, you can configure and deploy distinct instances of Microsoft Intune security baseline profiles to different groups of Windows devices and users. There are different baselines for different products, and each is a group of preconfigured settings that represent the recommended security posture from that products security team. You can deploy a default (unmodified) baseline or customize your profiles to configure devices with the settings that your organization requires.

For a list of available security baselines, see [Security baselines overview](../protect/security-baselines.md#available-security-baselines).

This feature applies to:

- Windows 11
- Windows 10 version 1809 and later

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

## Overview of security baselines

When you create a security baseline profile in Intune, you're creating a template that consists of multiple *device configuration* settings.

When multiple versions for a security baseline exist, only the most recent version can be used to create a new instance of that baseline. You can continue to use instances of older baselines that you previously created and edit the groups they're assigned to. However, outdated versions don't support changes to their setting configurations. Instead, create new baselines that use the most recent baseline version, or update your older baselines to that newest version if you need to introduce new configurations for settings.

We recommend updating older baseline versions to the latest version as soon as it's practical to do so. A newer version can:

- Include new settings that weren't available in the older versions.
- Retire and remove old settings that are no longer supported.
- Change the default configuration for settings to align to the current security recommendations for the applicable product.

Common tasks when working with security baselines include:

- [Create a new profile instance](#create-a-profile-for-a-security-baseline) – Configure the settings you want to use and assign the baseline to groups.
- [Update an older version baseline to the most current baseline version](#update-a-baseline-profile-to-the-latest-version) – Change the baseline version in use by a profile.
- [Remove a baseline assignment](#remove-a-security-baseline-assignment) - Learn what happens when you stop managing settings with a security baseline.

## Prerequisites

Find out what you need to manage Intune security baselines.

### Licensing

- Use of Intune to deploy security baselines requires a Microsoft Intune Plan 1 subscription. See [Microsoft Intune licensing](../fundamentals/licenses.md).

  > [!TIP]
  >
  > Intune provides an easy-to-use user interface to configure and deploy security baselines but doesn't create nor define the security baselines. Outside of Intune, other options to deploy security baselines are available, like those available from the [***Security Compliance Toolkit***](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/security-compliance-toolkit-10).

- Use of baselines through Intune requires you to have an active subscription for the managed product, when applicable. For example, use of the Microsoft Defender for Endpoint baseline doesn't grant rights to use Microsoft Defender. Instead, the baseline provides a method to configure and manage settings that are present on devices that are licensed for and managed by Microsoft Defender for Endpoint.

### Role-based access controls for managing Intune security baselines

To manage security baselines in Intune, your account must be assigned an Intune role-based access control (RBAC) role that includes following categories and permissions sufficient to complete the desired task:

- **Organization**:
    - Read

- **Security baselines**:
  - Assign
  - Create
  - Delete
  - Read
  - Update

You can add these permissions to your own [custom RBAC roles](../fundamentals/create-custom-role.md) or use an Intune [built-in RBAC role](../fundamentals/role-based-access-control-reference.md).

The least privileged built-in Intune role that supports managing security baselines is the [Policy and Profile Manager](../fundamentals/role-based-access-control.md#built-in-roles).

## Create a profile for a security baseline

The following guidance can be used anytime you create a new security baseline profile.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines** to view the list of available baselines.

   ![Select a security baseline to configure](./media/security-baselines-configure/available-baselines.png)

3. Select the baseline you'd like to use, and then select **Create policy**.

4. On the **Basics** tab, specify the following properties:

   - **Name**: Enter a name for your security baselines profile. For example, enter *Standard profile for Defender for Endpoint*.

   - **Description**: Enter some text that describes what this baseline does. The description is for you to enter any text you want. It's optional but recommended.

   Select **Next** to move to the next tab. After you advance to a new tab, you can select the tab name to return to a previously viewed tab.

5. On the Configuration settings tab, view the groups of **Settings** that are available in the baseline you selected. You can expand a group to view the settings in that group, and the default values for those settings in the baseline. To find specific settings:

   - Select a group to expand and review the available settings.
   - The insights for a setting are available beside a light bulb icon. Settings insights provide confidence in configurations by adding insights that similar organizations adopted successfully. Insights are available for some settings and not all settings. For more information, see [Settings insight](../fundamentals/settings-insight.md).
   - Use the *Search* bar and specify keywords that filter the view to view only those groups that contain your search criteria.

   Each setting in a baseline has a default configuration preset for that baseline version. Some aren't configured, while others are set to configure specific values or conditions on a device. The default presets found in a baseline represent the recommended security posture from that product's security team. When configuring a baseline:

   - Be sure to review each setting and when necessary, reconfigure a default preset when your business needs require a different configuration.
   - Be aware that different baseline types and versions can include settings that are also in other baselines, and each might recommend a different default value for a setting.

   ![Expand a group to view the settings for that group](./media/security-baselines-configure/sample-list-of-settings.png)

6. On the **Scope tags** tab, select **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.

7. On the **Assignments** tab, select **Select groups to include** and then assign the baseline to one or more groups. Use **Select groups to exclude** to fine-tune the assignment.

   > [!NOTE]
   > Security baselines are assigned to either user groups or device groups based on scope of the settings being used. Because of this, multiple baselines might be needed when assigning both user and device-based settings.

   ![Assign a profile](./media/security-baselines-configure/assignments.png)

8. When you're ready to deploy the baseline, advance to the **Review + create** tab and review the details for the baseline. Select **Create** to save and deploy the profile.

   As soon as you create the profile, Intune pushes it to the assigned group, which applies it immediately.

   > [!TIP]
   > If you save a profile without first assigning it to groups, you can later edit the profile to do so.

   ![Review the baseline](./media/security-baselines-configure/review.png)

9. After you create a profile, edit it by going to **Endpoint security** > **Security baselines**, select the baseline type that you configured, and then select **Profiles**. Select the profile from the list of available profiles, and then select **Properties**. You can edit settings from all the available configuration tabs and select **Review + save** to commit your changes.

## Update a baseline profile to the latest version

> [!NOTE]
> The information in this section applies to updating a baseline profile that was created in *May 2023  or later* to a more recent version of that same baseline.
>
> The format of security baselines changed in May 2023. Due to this change, the update process for baseline profiles created before May 2023 to later versions represent separate scenarios. For updates to baselines created before May 2023, see the following content in this article that applies to your baseline update scenario:
> - [Update baselines made before May 2023 to a baseline version released in May 2023 or later](#update-baselines-made-before-may-2023-to-a-baseline-version-released-in-may-2023-or-later)
> - [Update older baselines to newer versions when the newest version predates May 2023](#update-older-baselines-to-a-newer-version-when-the-newest-version-predates-may-2023)

When a new version for a baseline becomes available, plan to update your existing profiles to the new version.

**When a new version of any baseline type is released:**
- Existing profiles for that baseline type don’t automatically upgrade to the new version.
- The settings in your existing profiles become read-only. While you can continue to use those profiles and edit their name, description, and assignments, you can’t modify the configuration of any settings in them.

**When you update the version of a baseline profile:**
- Updates always use the latest available version of the same baseline type. You can't update a baseline to anything other than the most recently released version.
- The update process creates a new instance of the baseline based on the latest version as a side-by-side copy of the original profile. As part of the update, you have the choice to:

  - **Keep customizations** – Intune applies all the settings customizations from the original baseline that you're upgrading to the new baselines template. The result is that the new  baseline instance retains (includes) all your organization's specific modifications.
  - **Discard customizations** – Intune creates a new 'default' baseline instance using the new version. None of your settings customizations are automatically applied.

- During the update, you must provide the new instance with a *name* but can't edit the other details in the profile until after it's created. Both scope tags and assignments aren't carried over and remain blank. However, you can review the configuration settings of the profile before saving it.

**After the update process completes:**
- You can edit the new baseline instance including customizing settings, adding assignments, and configuring scope tags.
- The original baseline is left unchanged and retains its setting configurations, name, scope tags, and assignments. To avoid configuration conflicts, be sure to remove configurations like scope tags and assignments from the original baseline instance when adding the same to the updated baseline.
- Once the older baseline version is no longer assigned to any groups, you can delete it from your tenant if you choose.

### Update a baseline to the latest version
*Applies to updating a baseline profile that was created in May 2023 or later.*

1. Sign in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Endpoint security** > **Security baselines** > *select the baseline type* with the profile you want to update. On the baselines Profiles page, select the checkbox for the baseline instance that you want to update and then select **Update Version**. Intune displays the *Update Version* pane.

2. On the *Update Version* pane, select the update method to use:
   - **Accept baseline changes but keep my existing setting customizations** - Creates a new instance of the baseline profile using the latest version. Your current custom settings are preserved and applied to the new profile.
   - **Accept baseline changes and discard existing setting customizations** - Creates a new instance of the baseline profile using the latest version. None of the customizations from the profile being updated are added to the new profile. The new profile uses its default settings configuration.

   After selecting an update method, select **Create** to open the *Upgrade Policy* workflow for the new baseline profile you're creating.

3. On the **Basics** tab, specify a *Name* for this new profile. The *Description* field is already populated but can be edited at this time.

4. On the **Configuration settings** tab, you can review the configuration of the baseline's settings. If you choose to keep existing setting customizations, you see them here and can make other customizations if you choose.

5. For **Scope tags**, configuration is optional. The update process doesn't apply the scope tags from the older profile to this new profile. You can choose to configure scope tags now or return to edit the profile to add them later.

6. For **Assignments**, plan to assign the new profile to user groups or device groups. The update process doesn't apply the assignments from the older profile to this new profile. You can choose to configure assignments for this profile now and also return to edit the profile and add them later.

   If you do configure assignments at this time, plan to revisit the older profiles assignments to remove or modify them as necessary to avoid creating [conflicts](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines) between the old and new profiles.

   > [!NOTE]
   > Security baselines are assigned to either user groups or device groups based on scope of the settings being used. Because of this, multiple baselines might be needed when assigning both user and device-based settings.

7. On the **Review** tab, review the details for the baseline, and then select **Create** to save the new profile.

   When saved, a profile immediately deploys to all assigned groups.

### Test the updated baseline

During the update of a baseline, Intune creates a copy of the original profile but doesn’t include the group assignments. This means the new baseline instance doesn’t deploy to any devices at the time you make a copy or at the time you update it to a new version.
After you update the profile to the latest version, you can edit the settings in that new profile instance. This includes assigning the new baseline profile to groups of devices and editing the profiles settings to meet your organization’s expectations.

## Update baselines made before May 2023 to a baseline version released in May 2023 or later

> [!NOTE]
> The information in this section applies to updating baseline profiles created before May 2023 when the most recent baseline version that is available was released in May 2023 or later.

After May 2023, when a new version for a baseline is released, plan to update your existing profiles to the new version. When moving from an older format to the new baseline format (from a version released before May 2023 to one released in May 2023 or later):

- All new profiles for the baseline type, like Microsoft Edge, use the new format. Creating a new baseline that uses an older baseline version isn't supported.

- Baseline versions released before May 2023 don’t upgrade to the new format. Instead, create a new profile that uses the new format and configure the settings from the old baseline in that new baseline format. Recreation of the profile is a one-time process that is required to move a baseline from the old format to the new baseline format.

  To assist you in this process, Intune can export the old profile to a CSV format that identifies each setting based on the name of the setting as it appears in the new profile version, along with its configuration.

- After creating a new baseline that can replace your older baseline version, the older profile remains unchanged, and you can continue to use it. You can continue to deploy, reassign, and edit the settings in the older baseline format.

  > [!TIP]
  >
  > Support to edit settings in an older baseline version after updating to a new version is a change from past behavior. This behavior is possible only when moving from baselines versions created before May 2023 to versions created in May 2023 or later because the new baseline format exists side-by-side with the older baseline format instead of replacing it. Later, when updating a baseline instance that was created in May 2023 or later to a newer version, the original behavior where you can't edit settings in the older version returns.

  We recommend planning to discontinue use of the older format and deploy a profile based on the latest version as soon as possible. The older profiles don't receive updates while the newer versions released in May 2023:

  - Use the new settings format in the Intune UI that directly aligns to the configuration service provider (CSP) source for each setting.
  - Are preconfigured with default configurations that the relevant security teams recommend.

### Update a baseline to the new format

To update a baseline that was created before May 2023 to the new format, you must create a new baseline instance. To assist you in recreating the original baselines configuration, you can have Intune export your current baselines configuration as a .CSV file. Exports include:

- Each setting from the older baseline is identified by using the name of the setting as it appears in the new baseline. While the name of the setting isn't presented verbatim in the .csv, you can find the path for the setting, which contains part of the setting name in it.
- How each setting in the older baseline was configured.
- If the configuration of a setting from the old baseline matches the default configuration from the new baseline.

With the information from an export, you can rapidly reconfigure the new baseline to use the same values as the older baseline instance.

1. Sign in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Endpoint security** > **Security baselines** > *select the baseline type*, and then select the checkbox for the baseline profile (instance) that you want to replicate in the new baseline format, and then select **Change Version**. Intune displays the *Change Version* pane.

   The following screenshot displays a view of the *Security Baseline for Microsoft Edge*. We have two profiles at this time. One is a new profile for Microsoft Edge v112, and the other is an older profile from September 2020. The older profile also displays an arrow icon to indicate that there's a newer version to replace it.

   :::image type="content" source="./media/security-baselines-configure/select-a-baseline-profile-to-update.png" alt-text="Screen shot that shows the navigation path in the Intune admin center, to open the Change Version pane." lightbox="./media/security-baselines-configure/select-a-baseline-profile-to-update.png":::

2. On the *Change Version* pane, there are instructions for moving the configuration details from the older baseline to a profile that uses the new format. The pane also identifies the selected baselines name and version, and what the latest baseline version is.

   1. Select **Export Profile Settings** to create a .csv file that lists the settings in the selected baseline along with their current configurations if they aren't set to the baselines default. When you select the option to export the baseline details, Intune prepares the export, and then requires you to agree to continue. Select **Yes** to download the .CSV file export.

   2. After the file downloads, you can open it to view the older baselines current configuration.

   The *Change Version* pane also includes a button to **Create** a new profile for the selected baseline, which has the same function as the *Create profile* option that is more commonly used to create new baseline instances.

   The following screen capture shows an export for the Microsoft Edge profile version 85, as viewed in Microsoft Excel. Of the new Microsoft Edge baselines 17 settings that were found in the older profile, only one setting is changed: **Enable site isolation for every site** was set to **Disabled** in the older baseline. In the newer baseline, the setting now defaults to **Enabled**:

   :::image type="content" source="./media/security-baselines-configure/csv-export-of-baseline-configuration.png" alt-text="Screen shot that shows an export of the Microsoft Edge baseline profile as a .csv file." lightbox="./media/security-baselines-configure/csv-export-of-baseline-configuration.png":::

   In the preceding image, there are three columns of information. The information identifies the settings in the old profile, and the configuration for each of them that you had in the old profile.

   - **DefinitionId** – This column displays the settings registry name. The information after the underscore ( _ ) identifies the settings name as it appears in the old baseline profile and format, but without spaces in the name. This value is also the name of the CSP setting that this baseline setting manages.

     For example, our modified setting of *Enable site isolation for every site* appears in this export as *admx--microsoftedge_SitePerProcess*. The last portion, *SitePerProcess*, helps identify the setting.

   - **defaultJson** – This column identifies the default configuration for this setting as seen in the new baseline format. Our sample setting for the **SitePerProcess** CSP is set to **enabled** by default.

   - **customizedJson** – The final column displays the configuration of each setting from the older profile version. This information helps you understand which settings in the new profile require modification to match the older profiles’ configuration. Our sample setting was set to **disabled**. All other settings display "NotApplicable" as they weren't modified from the default configuration in the older baseline version we have been using.

   You might note that the updated Microsoft Edge baseline profile has more than the 17 settings found in the older profile. The baseline export doesn’t identify these new settings, as they weren't available in the older baseline version you're reviewing.

   Later, when you create and configure the new profile, you can use the list from the CSV export to ensure each setting from the previous profile is set in the new profile with the same configuration.

## Update older baselines to a newer version when the newest version predates May 2023

> [!NOTE]
> The information in this section applies to updating a baseline profile that was created before May 2023 when the most recent baseline version that is available was also released before May 2023.

When a new version for a baseline becomes available, plan to update your existing profiles to the new version:

- Existing profiles don’t upgrade to new versions automatically.
- Settings in baseline profiles that don’t use the latest version become read-only. You can continue using those older profiles, including editing their name, description, and assignments. However, you can't edit the settings in them or create new profiles based on those older versions.

We recommend you [test the version](#test-the-conversion-and-updated-baseline) update on a copy of your existing profiles before you update your live profiles.

When you change the profile version:

- You select the latest instance of the same baseline. You can't change between two different baseline types, such as changing a profile from using a baseline for Defender for Endpoint to using the MDM security baseline.
- You can export and download a CSV file that lists the changes between the two baseline versions involved.
- You choose how to update the profile:
  - You can keep all your customizations from the original baseline version.
  - You can choose to use the default values for all settings in the new baseline version.

  You don't have the option to change only some settings in a profile during the update.

During conversion:

- New settings that weren't in the older version you were using are added. Any new settings from the new version use their default values.

- Settings that aren't in the new baseline version you select are removed and no longer enforced by this security baseline profile.

  When a setting is no longer managed by a baseline profile, that setting doesn't reset on the device. Instead, the setting on the device remains set to its last configuration until some other process manages the setting to change it. Examples of processes that can change a setting after you stop managing it include a different baseline profile, a group policy setting, or manual configuration that's been applied on the device.

After the conversion to the new baseline version is complete:

- The baseline immediately redeploys to assigned groups.
- You can edit the baseline to change individual settings.

### Test the conversion and updated baseline

Before you update a baseline profile to a new version, create a copy of it so you can test the new version of your profile on a group of devices. See [Duplicate a security baseline](#duplicate-a-security-baseline) later in this article.

- When you create a copy, group assignments aren't included, which means your baseline copy doesn't deploy to any devices at the time you make a copy or at the time you update it to a new version.
- After you update the profile to the latest version, you can edit its settings. You can assign the updated copy to a group of devices and edit it to introduce changes to individual settings in the profile.

### To change the baseline version for a profile

Before you update the version of a profile that has assigned groups, [test the version update](#test-the-conversion-and-updated-baseline) on a copy of profile so you can then validate the new baselines settings on test group of devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines**, and then select the tile for the baseline type that has the profile you want to change.

3. Next, select **Profiles**, and then select the check box for the profile you want to edit, and then select **Change Version**.

   :::image type="content" source="./media/security-baselines-configure/select-baseline.png" alt-text="Screen capture that shows selection of a baseline.":::

4. On the **Change Version** pane, use the **Select a security baseline to update to** dropdown, and select the version instance you want to use.

   ![select a version](./media/security-baselines-configure/select-instance.png)

5. Select **Review update** to download a CSV file that displays the difference between the profile's current version and the new version. Review this file so that you understand which settings are new or removed, and what the default values for these settings are in the updated profile.

   When ready, continue to the next step.

6. Choose one of the two options for **Select a method to update the profile**:
   - **Accept baseline changes but keep my existing setting customizations** - This option keeps the customizations you made to the baseline profile and applies them to the new version you've selected to use.
   - **Accept baseline changes and discard existing setting customizations** - This option overwrites your original profile completely. The updated profile uses the default values for all settings.

7. Select **Submit**. The profile updates to the selected baseline version and after the conversion is complete, the baseline immediately redeploys to assigned groups.

## Remove a security baseline assignment

When a security baseline setting no longer applies to a device, or settings in a baseline are set to *Not configured*, those settings on a device might not revert to a premanaged configuration depending on the settings in the security baseline. The settings are based on CSPs, and each CSP can handle the change removal differently.

Other processes that might later change settings on the device include a different or new security baseline, device configuration profile, Group Policy configurations, or manual edit of the setting on the device.

## Duplicate a security baseline

You can create duplicates of your security baselines. Duplicating a baseline can be useful when you want to assign a similar but distinct baseline to a subset of devices. By creating a duplicate, you don't need to manually recreate the entire baseline. Instead, you can duplicate any of your current baselines and then introduce only the changes the new instance requires. You might only change a specific setting and the group the baseline is assigned to.

When you create a duplicate, give the copy a new name. The copy is made with the same setting configurations and scope tags as the original but doesn't have any assignments. You must edit the new baseline to add assignments.

All security baselines support creating duplicates.

After you duplicate a baseline, review and edit the new instance to make changes to its configuration.

### To duplicate a baseline

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Endpoint security** > **Security baselines**, select the type of baseline you want to duplicate, and then select **Profiles**.
3. Right-click on the profile you want to duplicate and select **Duplicate**, or select the ellipsis (**…**) to the right of the baseline and select **Duplicate**.
4. Provide a **New name** for the baseline, and then select **Save**.

After a *Refresh*, the new baseline profile appears in the admin center.

### To edit a baseline

1. Select the baseline, and then select **Properties**.
2. From this view you can select **Edit** for the following categories to modify the profile:

   - Basics
   - Assignments
   - Scope tags
   - Configuration settings

   You can *Edit* a profiles *Configuration settings* only when that profile uses the latest version of that security baseline. For profiles that use older versions, you can expand **Settings** to view the configuration of settings in the profile, but you can't modify them. After a profile is updated to the most recent baseline version, you'll be able to edit the profiles settings.

3. After you make changes, select **Save** to save your edits. You must save edits to one category before you can introduce edits to other categories.

## About older baseline versions

Microsoft Intune updates the versions of built-in security baselines depending on the changing needs of a typical organization. Each new release results in a version update to a particular baseline. The expectation is that customers use the latest baseline version as a starting point for their Device Configuration profiles.
<!--
When there are no longer any profiles that use an older baseline listed in your tenant, Microsoft Intune lists the latest baseline version available.
-->

If you have a baseline profile associated with an older baseline version in use, that older baseline profile continues to be listed.

## Co-managed devices

Security baselines on Intune-managed devices are similar to co-managed devices with Configuration Manager. Co-managed devices use Configuration Manager and Microsoft Intune to manage the Windows devices simultaneously. It lets you cloud-attach your existing Configuration Manager investment to the benefits of Intune. [Co-management overview](/configmgr/comanage/overview) is a great resource if you use Configuration Manager and also want the benefits of the cloud.

When using co-managed devices, you must switch the **Device configuration** workload (its settings) to Intune. [Device configuration workloads](/configmgr/comanage/workloads#device-configuration) provides more information.

## Next steps

- Check the status and monitor the [baseline and profile](security-baselines-monitor.md)

- View the settings in the latest versions of the available baselines:
  - [Windows 10 and later - MDM security baseline](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender for Endpoint baseline](security-baseline-settings-defender.md)
  - [Microsoft 365 Apps for Enterprise (Office baseline)](security-baseline-v2-office-settings.md)
  - [Microsoft Edge (Version 112 and later)](security-baseline-v2-edge-settings.md)
  - [Windows 365 Security Baseline](security-baseline-settings-windows-365.md)
