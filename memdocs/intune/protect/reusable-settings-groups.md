---
# required metadata

title: Use reusable groups of settings policies in Microsoft Intune | Microsoft Docs
description: Manage groups of settings for Intune profiles as a single object and then add that settings group object to multiple profile instances. Later changes to the settings group are automatically applied to each profile that includes the reusable settings group.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: laarrizz

---

# Use reusable groups of settings with Intune policies

*This feature is in public preview*.

Intune supports *reusable settings groups* that you can add to configuration policies and profiles to help simplify management of common settings. A good time to use reusable groups is when you need to use the settings with the same configuration in more than a single profile.

When you edit the settings in a reusable group, the changes you make are automatically applied to each profile that includes the group. When you save your changes to the reusable settings group, Intune updates the profiles with those new configurations and deploys the updated profile to devices based on the profile’s assignments.

The following profiles support reusable groups.

- [Microsoft Defender Firewall Rules](../protect/endpoint-security-firewall-policy.md#firewall-profiles)

## Overview of reusable settings groups

Each reusable settings group is a single object that can include multiple settings. After configuring one or more reusable groups for use with a specific profile type, you create or edit a profile to add the groups. Profiles can support multiple groups.

To manage groups of reusable settings, in the Microsoft Endpoint Manager admin center you use the *Reusable settings* tab that’s associated with the policy and profiles you want to use a group with. On the tab, you can create a group, edit the settings in a group, and view the count of policies that inherit settings from each group. Each reusable settings group can be used with only its related profile type.

For example, the following image shows the Reusable settings tab you would use to manage reusable groups for the Microsoft Defender Firewall Rules profile:

:::image type="content" source="./media/reusable-settings-groups/reusable-setting-tab.png" alt-text="Screen shot that shows the Reusable settings tab for Firewall policies in the Microsoft Endpoint Manager admin center.":::

After creating reusable groups, use an option in profiles *Configuration settings* to add groups to that profile. Profiles that include one or more reusable groups use each setting from each included group as if they were directly configured in the profile.

## Prerequisites

The following are prerequisites to use reusable settings groups:

- **Microsoft Defender Firewall rules**:  
  - **Platforms**: Windows 10, Windows 11, and Windows Server
  - **Windows versions**: Devices must run Windows 10 20H2 or later, or Windows 11.

## Create a reusable group

Each reusable settings group includes a subset of settings from the full profile you’re creating the group for. Use the following links to view the settings you can configure in a settings group for each profile:

- [Microsoft Defender Firewall rules](../protect/endpoint-security-firewall-policy.md#add-reusable-settings-groups-to-profiles-for-firewall-rules)

**To create a reusable settings group**:

1. Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), navigate to the policy for which you want to create a reusable group and then select the **Reusable settings (preview)** tab.

2. Select **Add** to open the *Configure reusable settings (preview)* workflow.

3. On the **Basics** page, configure a name. The description is optional.

4. On the *Configuration settings* page, configure settings for this group as if configuring settings directly in the supported profile. Use the information text in the admin center for each setting in the reusable settings group as guidance. Follow the *Learn more* link for a setting to view details about the setting from that settings content source.

5. On the *Review + Add* page, select **Add** to save your reusable settings group.

## Modify a reusable group

When you edit the configuration of a reusable group, each profile that uses that group automatically updates to apply the new configuration to devices.

1. Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), navigate to the policy for which you want to create a reusable group and then select the **Reusable settings (preview)** tab.

2. Select the reusable settings group you want to edit. This opens the configuration workflow that resembles the workflow for creating a new reusable group.

3. On the *Basics* page you can rename the group, and on the *Configuration settings* page you can reconfigure settings. On the last page, select **Save** to save your configuration and update the profiles that use the settings group.

## Add reusable groups to a Microsoft Defender Firewall rule profile

Add reusable settings groups to profiles while editing or creating the profile. On the profiles Configuration settings page, you’ll use an option that supports adding one or more previously created groups.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a new profile or select and edit an existing profile.

2. On the *Configuration settings* page, select **Add** to add a new rule, or **Edit rule** to manage a previously created rule.

3. On the *Configure instance* pane for the rule, configure **Action** to determine how this rule manages settings like IP Addresses or FQDNs. For example, you might set Action to *allow* or *block*. This configuration applies to both settings you add directly to this rule and to settings that are in each reusable group that’s added to this rule.

   **Save** the rule configuration.

4. For the rule you saved, select **Set reusable settings** to open the *Select reusable settings* pane.

   :::image type="content" source="./media/reusable-settings-groups/add-reusable-group-to-profile.png" alt-text="Screen shot of the Configuration settings workflow for configuring a reusable group.":::

5. Select one or more of the available groups to add them to this rule, and then save your selections.

   :::image type="content" source="./media/reusable-settings-groups/select-groups.png" alt-text="Screen shot that shows the Select Reusable settings pane.":::

6. After adding reusable groups to a profile, save your configuration. When saved, Intune includes the settings from the reusable groups and deploys the profile to devices based on the profile’s assignments.

## About policy conflicts

The device settings you can manage through reusable settings groups are applied by Intune the same as settings that are directly configured in a profile. This means that should conflicts or overlaps be introduced by settings from your reusable groups, you can use the same troubleshooting process to identify and resolve those conflicts.

For more information, review guidance that might be specific to the profile types you use. For general guidance, see [Troubleshoot policies and profiles in Microsoft Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune), and [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md).

## Next steps

[Device configuration overview](../configuration/device-profiles.md)