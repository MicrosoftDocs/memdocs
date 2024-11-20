---
title: Common Education Start menu configuration
description: Learn about common Start menu configuration used by Education organizations in Intune.
ms.date: 5/2/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows, Autopatch, Autopilot]
ms.collection: 
- graph-interactive
---

# Start menu customization

Microsoft Intune and Intune for Education can configure settings for a customized Start menu for Windows 10 and later. This article summarizes the configurations that are most commonly used for student and teacher devices.

Students can benefit from a Start menu that is customized to provide access to educational tools and resources while restricting distractions. By configuring policy settings, educational institutions can create a focused and conducive learning environment.

> [!NOTE]
> This is an optional policy

To learn more, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)
- [Customize the Start menu and taskbar layout on Windows 10 and later devices](/windows/configuration/start/windows-10-start-layout-options-and-policies)
- [Customize and export the Start layout](/en-us/windows/configuration/start/customize-and-export-start-layout)
- [Configure Windows Taskbar](/en-us/windows/configuration/taskbar/?pivots=windows-11)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## [**Settings**](#tab/settings)

| **Name** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **:::no-loc text="Start Layout":::** | A custom XML string | Create and deploy a custom Start menu and taskbar layout. Please refer to articles in the learn more section above. | [:::no-loc text="StartLayout":::](/windows/client-management/mdm/policy-csp-start#startlayout) |
| **:::no-loc text="Hide App List":::** | None | | [:::no-loc text="Start/HideAppList":::](/windows/client-management/mdm/policy-csp-start#hideapplist) |
| **:::no-loc text="Hide Change Account Settings":::** | Disabled | | [:::no-loc text="Start/HideChangeAccountSettings":::](/windows/client-management/mdm/policy-csp-start#hidechangeaccountsettings) |
| **:::no-loc text="Hide Frequently Used Apps":::** | Enabled | | [:::no-loc text="Start/HideFrequentlyUsedApps":::](/windows/client-management/mdm/policy-csp-start#hidefrequentlyusedapps) |
| **:::no-loc text="Hide Power Button":::** | Disabled | | [:::no-loc text="Start/HidePowerButton":::](/windows/client-management/mdm/policy-csp-start#hidepowerbutton) |
| **:::no-loc text="Hide Recent Jumplists":::** | Enabled | | [:::no-loc text="Start/HideRecentJumplists":::](/windows/client-management/mdm/policy-csp-start#hiderecentjumplists) |
| **:::no-loc text="Hide Recently Added Apps":::** | Enabled | | [:::no-loc text="Start/HideRecentlyAddedApps":::](/windows/client-management/mdm/policy-csp-start#hiderecentlyaddedapps) |
| **:::no-loc text="Hide User Tile":::** | Disabled | | [:::no-loc text="Start/HideUserTile":::](/windows/client-management/mdm/policy-csp-start#hideusertile) |
| **:::no-loc text="Hide Lock":::** | Disabled | | [:::no-loc text="Start/HideLock":::](/windows/client-management/mdm/policy-csp-start#hidelock) |
| **:::no-loc text="Hide Sign Out":::** | Disabled | | [:::no-loc text="Start/HideSignOut":::](/windows/client-management/mdm/policy-csp-start#hidesignout) |

## [:::image type="icon" source="../../../media/icons/graph.svg"::: **Create policy using Graph Explorer**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **_MSLearn_Example_CommonEDU - Windows - Start menu**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_CommonEDU - Windows - Start menu","description":"https://aka.ms/ManageEduDevices","platforms":"windows10","technologies":"mdm","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hideapplist","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hideapplist_0","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hidechangeaccountsettings","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hidechangeaccountsettings_0","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hidefrequentlyusedapps","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hidefrequentlyusedapps_1","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hidepowerbutton","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hidepowerbutton_0","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hiderecentjumplists","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hiderecentjumplists_1","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hiderecentlyaddedapps","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hiderecentlyaddedapps_1","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hideusertile","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hideusertile_0","children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hidelock","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hidelock_0","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_hidesignout","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_start_hidesignout_0","children":[]}}]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_start_startlayout","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationStringSettingValue","value":""}}}]}
```

[!INCLUDE [graph-explorer-steps](../../../includes/graph-explorer-steps.md)]

---
