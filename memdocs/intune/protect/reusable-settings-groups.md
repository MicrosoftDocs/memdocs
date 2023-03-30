---
# required metadata

title: Use reusable groups of settings policies in Microsoft Intune | Microsoft Docs
description: Manage groups of settings for Intune profiles as a single object and then add that settings group object to multiple profile instances. Later changes you make to the settings groups  automatically apply to each profile that includes the reusable settings group.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
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
ms.collection:
- tier1
- M365-identity-device-management
- highpri
ms.reviewer: laarrizz

---

# Use reusable groups of settings with Intune policies

*This feature is in public preview*.

Intune supports *reusable settings groups* that you can add to configuration policies and profiles to help simplify management of common settings. A good time to use reusable groups is when you need to use the settings with the same configuration in more than a single profile.

When you edit the settings in a reusable group, the changes you make automatically apply to each profile that includes the group. When you save your changes to the reusable settings group, Intune updates the profiles with those new configurations and deploys the updated profile to devices based on the profile’s assignments.

The following profiles support reusable groups.

- [Device control](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) (Attack Surface Reduction policy)
- [Microsoft Defender Firewall Rules](../protect/endpoint-security-firewall-policy.md#firewall-profiles) (Firewall policy)

## Overview of reusable settings groups

Each reusable settings group is a single object that can include multiple settings. After configuring one or more reusable groups for use with a specific profile type, you create or edit a profile to add the groups. Profiles can support multiple groups.

To manage groups of reusable settings, in the Microsoft Intune admin center you use the *Reusable settings* tab that’s associated with the policy and profiles you want to use a group with. On the tab, you can create a group, edit the settings in a group, and view the count of policies that inherit settings from each group. Each reusable settings group is used with only its related profile type.

For example, the following image shows the Reusable settings tab you would use to manage reusable groups for the Microsoft Defender Firewall Rules profile:

:::image type="content" source="./media/reusable-settings-groups/reusable-setting-tab.png" alt-text="Screenshot that shows the Reusable settings tab for Firewall policies in the Microsoft Intune admin center.":::

After creating reusable groups, you use an option in a profiles *Configuration settings* page to add groups to that profile. Profiles that include one or more reusable groups use each setting from each included group as if the settings were directly configured in the profile.

## Prerequisites

The following profiles support use of reusable settings groups:

**Endpoint security policy**

- **Antivirus** > **Microsoft Defender Firewall rules**:  
  - Platforms: Windows 10, Windows 11, and Windows Server
  - Windows versions: Devices must run Windows 10 20H2 or later, or Windows 11.

- **Attack surface reduction** > **Device control**:
  - Platforms: Windows 10 and later

**Endpoint Privilege Management**

- Windows elevation rules policy




## Create a reusable group

Each reusable settings group includes a subset of settings from the full profile you’re creating the group for. Use the following links to view the settings you can configure in a settings group for each profile:

- [Device Control](../protect/endpoint-security-asr-policy.md#add-reusable-settings-groups-to-profiles-for-device-control)
- [Microsoft Defender Firewall rules](../protect/endpoint-security-firewall-policy.md#add-reusable-settings-groups-to-profiles-for-firewall-rules)

**To create a reusable settings group**:

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), navigate to the policy for which you want to create a reusable group and then select the **Reusable settings (preview)** tab.

2. Select **Add** to open the *Configure reusable settings (preview)* workflow.

3. On the **Basics** page, configure a name. The description is optional.

4. On the *Configuration settings* page, select **Add** and then configure settings for this group as if configuring settings directly in the supported profile.

   For Device Control, when you select *Add* you then must choose the type of group settings to configure, and then select **Edit instance** to continue. If you add more than one instance, review the **Match type** configuration for the group.

   There's a limit of 100 instances per group. Use the information text in the admin center for each setting in the reusable settings group as guidance. Follow the *Learn more* link for a setting to view details about the setting from that settings content source.

   > [!TIP]  
   > Carefully *Name* each reusable group you create to ensure you can identify it later. This is important because each reusable group that you create, for any policy type, is visible when adding reusable groups to a policy, even if the group contains settings that would not normally apply to the policy you’re configuring. For example, if you have a reusable group created for Microsoft Defender Firewall rules, that group will be visible and can be selected when adding reusable groups to Device Control policies.

5. On the *Review + Add* page, select **Add** to save your reusable settings group.

## Modify a reusable group

When you edit the configuration of a reusable group, each profile that uses that group automatically updates to apply the new configuration to devices.

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), navigate to the policy for which you want to create a reusable group and then select the **Reusable settings (preview)** tab.

2. Select the reusable settings group you want to edit. This opens the configuration workflow that resembles the workflow for creating a new reusable group.

3. On the *Basics* page you can rename the group, and on the *Configuration settings* page you can reconfigure settings. On the last page, select **Save** to save your configuration and update the profiles that use the settings group.

## Add reusable groups to a Microsoft Defender Firewall rule profile

Add reusable settings groups to profiles while editing or creating the profile. On the profiles Configuration settings page, use an option that supports adding one or more previously created groups.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a new profile or select and edit an existing profile.

2. On the *Configuration settings* page, select **Add** to add a new rule, or **Edit rule** to manage a previously created rule.

3. On the *Configure instance* pane for the rule, configure **Action** to determine how this rule manages settings like IP Addresses or FQDNs. For example, you might set Action to *allow* or *block*. This configuration applies to both the settings you add directly to this rule and to the settings that are in each reusable group that is added to this rule.

   **Save** the rule configuration.

4. For the rule you saved, select **Set reusable settings** to open the *Select reusable settings* pane.

   :::image type="content" source="./media/reusable-settings-groups/add-reusable-group-to-profile.png" alt-text="Screenshot of the Configuration settings workflow for configuring a reusable group.":::

5. Select one or more of the available groups to add them to this rule, and then save your selections. 

   :::image type="content" source="./media/reusable-settings-groups/select-groups.png" alt-text="Screenshot that shows the Select Reusable settings pane.":::

6. After adding reusable groups to a profile, save your configuration. When saved, Intune includes the settings from the reusable groups and deploys the profile to devices based on the profile’s assignments.

## Add reusable groups to a Device Control profile

Add reusable settings groups to profiles while editing or creating the profile. Reusable groups for Device Control profiles support the following types of settings:

- Printer device
- Removable storage

On the profiles Configuration settings page, use an option that supports adding one or more previously created groups.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a new profile or select and edit an existing profile.

2. On the *Configuration settings* page, expand the Device Control category and select **Add** to add a new rule, or **Edit Entry** to manage a previously created rule.

   - Select Add to add more rules.
   - Select **Edit Entry** to open the *Configure Entry* pane to further configure use of the group.

3. On the *Configure Entry* pane, give the entry a **Name**, and then configure the following and then select **OK** to save the rule:

   - **Type**: Defines the action for the removable storage groups. When there are conflicts for Type for the same media, the first type that’s defined in the policy is applied.
   - **Options**: Defines whether to display a notification to the device user. The options available depend on the Type that is selected.
   - **Access mask**: Choose one or more from Read, Write, Execute.
   - **Sid**:  Local user Sid or user Sid group or the Sid of the AD object, defines whether to apply this policy over a specific user or user group; one entry can have a maximum of one Sid and an entry without any Sid means it applies the policy over the machine.
   - **Computer Sid**: Local computer Sid or computer Sid group or the Sid of the AD object, defines whether to apply this policy over a specific machine or machine group; one entry can have a maximum of one ComputerSid and an entry without any ComputerSid means it applies the policy over the machine. If you want to apply an Entry to a specific user and specific machine, add both Sid and ComputerSid into the same Entry.

   For more information about these options, see the following articles in the Microsoft Defender for Endpoint documentation:

   - [Microsoft Defender for Endpoint Device Control Removable Storage Access Control](/microsoft-365/security/defender-endpoint/device-control-removable-storage-access-control) in the Microsoft Defender for Endpoint documentation.
   - [Printer Protection Overview](/microsoft-365/security/defender-endpoint/printer-protection-overview)

4. For the rule you saved, select **Set reusable settings** for *Included ID* and *Excluded ID* to meet your needs. Both selections open a *Select reusable settings* pane.

   :::image type="content" source="./media/reusable-settings-groups/add-reusable-group-for-device-control.png" alt-text="Screenshot that shows the Select Reusable settings pane for device control profiles.":::

5. Select one or more of the available groups to add them to this rule, and then save your selections.
The following shows a configuration with only one group selected for Excluded ID:

   :::image type="content" source="./media/reusable-settings-groups/one-excluded-id-for-device-control.png" alt-text="Screenshot that shows the result of selecting a group for only an excluded ID.":::

6. After adding reusable groups to a profile, complete the policy configuration. When saved, Intune includes the settings from the reusable groups and deploys the profile to devices based on the profile’s assignments. A maximum of 100 reusable groups can be added per profile.

If you have an E5 license, you can use Microsoft Defender for Endpoint to view device control events under the *Device Control report* and *Advanced hunting*. See [Protect your organization's data with device control | Microsoft Docs](/microsoft-365/security/defender-endpoint/device-control-report) in the Defender for Endpoint documentation.

## Use reusable groups for Endpoint Privilege Manager

For information about support for using reusable groups for Endpoint Privilege Manager, see [Policies for Endpoint Privilege Manager](../protect/epm-policies.md)

## About policy conflicts

The device settings you can manage through reusable settings groups are applied by Intune the same as settings that are directly configured in a profile. If conflicts or overlaps are introduced by settings from your reusable groups, you can use the same troubleshooting process to identify and resolve those conflicts.

For more information, review guidance that might be specific to the profile types you use. For general guidance, see [Troubleshoot policies and profiles in Microsoft Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune), and [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md).

## Next steps

[Device configuration overview](../configuration/device-profiles.md)
