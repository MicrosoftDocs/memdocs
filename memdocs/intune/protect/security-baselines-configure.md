---
# required metadata

title: Create security baseline profiles in Microsoft Intune
description: Create default profiles and customized profiles to deploy security baselines to devices you manage with Intune. Security baselines manage settings on windows devices to help keep your users and devices secure. 
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: 
   - intune-azure
   - contperf-fy21q1
ms.collection:
- tier2
- M365-identity-device-management
---
 
# Manage security baseline profiles in Microsoft Intune

Manage profiles for security baselines to help secure and protect your users and devices. Security baselines are pre-configured groups of Windows settings that represent the recommended security posture from the relevant security teams. You can deploy a default (unmodified) baseline or create a customized profile to enforce the settings you require for your environment.

When you create a security baseline profile in Intune, you're creating a template that consists of multiple *device configuration* settings.

This feature applies to:

- Windows 10 version 1809 and later
- Windows 11

See the list of [available security baselines](../protect/security-baselines.md#available-security-baselines).

Common tasks when working with security baselines include:

- [Create a profile](#create-the-profile) – Configure the settings you want to use and assign the baseline to groups.
- [Change the version](#change-the-baseline-version-for-a-profile) – Change the baseline version in use by a profile.
- [Remove a baseline assignment](#remove-a-security-baseline-assignment) - Learn what happens when you stop managing settings with a security baseline.

## Prerequisites

- To manage baselines in Intune, your account must have the [Policy and Profile Manager](../fundamentals/role-based-access-control.md#built-in-roles) built-in role.

- Use of some baselines might require you to have an active subscription to additional services, like Microsoft Defender for Endpoint.

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines** to view the list of available baselines.

   ![Select a security baseline to configure](./media/security-baselines-configure/available-baselines.png)

3. Select the baseline you'd like to use, and then select **Create profile**.

4. On the **Basics** tab, specify the following properties:

   - **Name**: Enter a name for your security baselines profile. For example, enter *Standard profile for Defender for Endpoint*.

   - **Description**: Enter some text that describes what this baseline does. The description is for you to enter any text you want. It's optional, but recommended.

   Select **Next** to go to the next tab. After you advanced to a new tab, you can select the tab name to return to a previously viewed tab.

5. On the Configuration settings tab, view the groups of **Settings** that are available in the baseline you selected. You can expand a group to view the settings in that group, and the default values for those settings in the baseline. To find specific settings:
   - Select a group to expand and review the available settings.
   - Use the *Search* bar and specify keywords that filter the view to display only those groups that contain your search criteria.

   Each setting in a baseline has a default configuration for that baseline version. Reconfigure the default settings to meet your business needs. Different baselines might contain the same setting, and use different default values for the setting, depending on the intent of the baseline.

   ![Expand a group to view the settings for that group](./media/security-baselines-configure/sample-list-of-settings.png)

6. On the **Scope tags** tab, select **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.

7. On the **Assignments** tab, select **Select groups to include** and then  assign the baseline to one or more groups. Use **Select groups to exclude** to fine-tune the assignment.

> [!NOTE]
> Security baselines must be assigned to either user groups or device groups based on scope of the settings being used. Because of this, multiple baselines may be needed when assigning both user and device based settings.

   ![Assign a profile](./media/security-baselines-configure/assignments.png)

8. When you're ready to deploy the baseline, advance to the **Review + create** tab and review the details for the baseline. Select **Create** to save and deploy the profile.

   As soon as you create the profile, it's pushed to the assigned group and might apply immediately.

   > [!TIP]
   > If you save a profile without first assigning it to groups, you can later edit the profile to do so.

   ![Review the baseline](./media/security-baselines-configure/review.png)

9. After you create a profile, edit it by going to **Endpoint security** > **Security baselines**, select the baseline type that you configured, and then select **Profiles**. Select the profile from the list of available profiles, and then select **Properties**. You can edit settings from all the available configuration tabs, and select **Review + save** to commit your changes.

## Change the baseline version for a profile

When a new version for a baseline is released, plan to update your existing profiles to the new version:

- Existing profiles don’t upgrade to new versions automatically.
- Settings in baseline profiles that don’t use the latest version become read-only. You can continue using those older profiles, including editing their name, description and assignments, but you won't be able to edit settings for them or create new profiles based on the older versions.

We recommend you [test the version](#test-the-conversion-and-updated-baseline) update on a copy of your existing profiles before you update your live profiles.

When you change the profile version:

- You select the latest instance of the same baseline. You can't change between two different baseline types, such as changing a profile from using a baseline for Defender for Endpoint to using the MDM security baseline.
- You have the option to download a CSV file that lists the changes between the two baseline versions involved.
- You choose how to update the profile:
  - You can keep all your customizations from the original baseline version.
  - You can choose to use the default values for all settings in the new baseline version.

  You don't have the option to change only some settings in a profile during the update.

During conversion:

- New settings that weren't in the older version you were using are added. Any new settings from the new version will use their default values.

- Settings that aren't in the new baseline version you select are removed and no longer enforced by this security baseline profile.

  When a setting is no longer managed by a baseline profile, that setting doesn't reset on the device. Instead, the setting on the device remains set to its last configuration until some other process manages the setting to change it. Examples of processes that can change a setting after you stop managing it include a different baseline profile, a group policy setting, or manual configuration that's made on the device.

After the conversion to the new baseline version is complete:

- The baseline immediately redeploys to assigned groups.
- You can edit the baseline to change individual settings.

### Test the conversion and updated baseline

Before you update a baseline profile to a new version, create a copy of it so you can test the new version of your profile on a group of devices. See [Duplicate a security baseline](#duplicate-a-security-baseline) later in this article.

- When you create a copy, group assignments are not included. This means your baseline copy won’t deploy to any devices at the time you make a copy, or at the time you update it to a new version.
- After you update the profile to the latest version, you can edit its settings. You can assign the updated copy to a group of devices and edit it to introduce changes to individual settings in the profile.

### To change the baseline version for a profile

Before you update the version of a profile that's assigned to groups, [test the version update](#test-the-conversion-and-updated-baseline) on a copy of profile so you can then validate the new baselines settings on test group of devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines**, and then select the tile for the baseline type that has the profile you want to change.

3. Next, select **Profiles**, and then select the check box for the profile you want to edit, and then select **Change Version**.

   ![select a baseline](./media/security-baselines-configure/select-baseline.png)

4. On the **Change Version** pane, use the **Select a security baseline to update to** dropdown, and select the version instance you want to use.

   ![select a version](./media/security-baselines-configure/select-instance.png)

5. Select **Review update** to download a CSV file that displays the difference between the profiles current instance version and the new version you've selected. Review this file so that you understand which settings are new or removed, and what the default values for these settings are in the updated profile.

   When ready, continue to the next step.

6. Choose one of the two options for **Select a method to update the profile**:
   - **Accept baseline changes but keep my existing setting customizations** - This option keeps the customizations you made to the baseline profile and applies them to the new version you've selected to use.
   - **Accept baseline changes and discard existing setting customizations** - This option overwrites your original profile completely. The updated profile will use the default values for all settings.

7. Select **Submit**. The profile updates to the selected baseline version and after the conversion is complete, the baseline immediately redeploys to assigned groups.

## Remove a security baseline assignment

When a security baseline setting no longer applies to a device, or settings in a baseline are set to *Not configured*, those settings on a device might not revert to a pre-managed configuration depending on the settings in the security baseline. The settings are based on CSPs, and each CSP can handle the change removal differently.

Other processes that might later change settings on the device include a different or new security baseline, device configuration profile, Group Policy configurations, or manual edit of the setting on the device.

## Duplicate a security baseline

You can create duplicates of your security baselines. Duplicating a baseline can be useful when you want to assign a similar but distinct baseline to a subset of devices. By creating a duplicate, you won't need to manually recreate the entire baseline. Instead, you can duplicate any of your current baselines and then introduce only the changes the new instance requires. You might only change a specific setting and the group the baseline is assigned to.

When you create a duplicate, you'll give the copy a new name. The copy is made with the same setting configurations and scope tags as the original, but won't have any assignments. You'll need to edit the new baseline to add assignments.

All security baselines support creating a duplicate.

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

3. After you’ve made changes, select **Save** to save your edits. You save edits to one category before you can introduce edits to additional categories.

## Older baseline versions

Microsoft Endpoint Manager updates the versions of built-in Security Baselines depending on the changing needs of a typical organization. Each new release results in a version update to a particular baseline. The expectation is that customers will be using the latest baseline version as a starting point to their Device Configuration profiles.

When there are no longer any profiles that use an older baseline listed in your tenant, Microsoft Endpoint Manager will only list the latest baseline version available.

If you have a profile associated with an older baseline, that older baseline will continue to be listed.

## Co-managed devices

Security baselines on Intune-managed devices are similar to co-managed devices with Configuration Manager. Co-managed devices use Configuration Manager and Microsoft Intune to manage the Windows 10/11 devices simultaneously. It lets you cloud-attach your existing Configuration Manager investment to the benefits of Intune. [Co-management overview](/configmgr/comanage/overview) is a great resource if you use Configuration Manager, and also want the benefits of the cloud.

When using co-managed devices, you must switch the **Device configuration** workload (its settings) to Intune. [Device configuration workloads](/configmgr/comanage/workloads#device-configuration) provides more information.

## Next steps

- Check the status and monitor the [baseline and profile](security-baselines-monitor.md)

- View the settings in the latest versions of the available baselines:
  - [MDM security baseline](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender for Endpoint baseline](security-baseline-settings-defender-atp.md)
  - [Microsoft Edge Baseline](security-baseline-settings-edge.md)

