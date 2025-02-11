---
title: Common Education privacy configuration
description: Learn about common privacy configuration used by Education organizations in Intune.
ms.date: 5/2/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows, Autopatch, Autopilot]
ms.collection: 
- graph-interactive
ms.service: microsoft-intune
ms.subservice: education
---

# Windows privacy

Microsoft Intune and Intune for Education can configure privacy settings for Windows 10 and later. This article summarizes the configurations that are most commonly used for student and teacher devices.

> [!IMPORTANT]
> The settings in this article configure user privacy. These settings should only be deployed after careful consideration.

> [!NOTE]
> This is an optional policy

To learn more, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## [**Settings**](#tab/settings)

| **Category** | **Name** | **Value** | **Notes** | **CSP** |
|---|---|---|---|---|
| Privacy | **:::no-loc text="Let Apps Access Location":::** | Force allow. | Windows apps are allowed to access location. You can specify either a default setting for all apps or a per-app setting by specifying a Package Family Name. You can get the Package Family Name for an app by using the Get-AppPackage Windows PowerShell cmdlet. A per-app setting overrides the default setting. | [:::no-loc text="Privacy/LetAppsAccessLocation":::](/windows/client-management/mdm/policy-csp-privacy#letappsaccesslocation) |
| System | **:::no-loc text="Allow Location":::** | Force Location On. All Location Privacy settings are toggled on and grayed out. Users can't change the settings and all consent permissions will be automatically suppressed. | Required to invoke **Locate device** action on Windows devices in Intune. | [:::no-loc text="System/AllowLocation":::](/windows/client-management/mdm/policy-csp-system#allowlocation) |

## [:::image type="icon" source="../../../media/icons/graph.svg"::: **Create policy using Graph Explorer**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **:::no-loc text="_MSLearn_Example_CommonEDU - Windows - Privacy":::**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_CommonEDU - Windows - Privacy","description":"https://aka.ms/ManageEduDevices","platforms":"windows10","technologies":"mdm","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_privacy_letappsaccesslocation","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_privacy_letappsaccesslocation_1","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_system_allowlocation","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_system_allowlocation_2","children":[]}}}]}
```

[!INCLUDE [graph-explorer-steps](../../../includes/graph-explorer-steps.md)]

---
