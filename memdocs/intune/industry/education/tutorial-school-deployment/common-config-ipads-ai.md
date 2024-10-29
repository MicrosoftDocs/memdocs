---
title: Common Education iPads Apple Intelligence configuration
description: Learn about common iPads Apple Intelligence configuration used by Education organizations in Intune.
ms.date: 10/16/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Apple]
ms.collection: 
- graph-interactive
---

# Apple Intelligence

This article summarizes restrictions for Apple Intelligence introduced in iPadOS 18.

To learn more, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](/mem/intune/configuration/settings-catalog)
- [Restrictions payload](https://developer.apple.com/documentation/devicemanagement/restrictions)
- [iPadOS 18](https://www.apple.com/ipados/ipados-18)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## [**Settings**](#tab/settings)

| **Category** | **Property** | **Value** | **Notes** | **Payload property** |
|---|---|:---:|---|---|
| Restrictions | **:::no-loc text="Allow Genmoji":::** | False | Prohibits creating new Genmoji | [:::no-loc text="allowGenmoji":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Image Playground":::** | False | Prohibits the use of image generation | [:::no-loc text="allowImagePlayground":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Image Wand":::** | False | Prohibits the use of Image Wand | [:::no-loc text="allowImageWand":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Personalized Handwriting Results":::** | False | | [:::no-loc text="allowPersonalizedHandwritingResults":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Writing Tool":::** | False | Disables Apple Intelligence writing tools | [:::no-loc text="allowWritingTools":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |

## [:::image type="icon" source="../../../media/icons/graph.svg"::: **Create policy using Graph Explorer**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **_MSLearn_Example_CommonEDU - iPads - Appple Intelligence**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_CommonEDU - iPads - Apple Intelligence","description":"","platforms":"iOS","technologies":"mdm,appleRemoteManagement","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.applicationaccess_com.apple.applicationaccess","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowgenmoji","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowgenmoji_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowimageplayground","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowimageplayground_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowimagewand","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowimagewand_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowpersonalizedhandwritingresults","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowpersonalizedhandwritingresults_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowwritingtools","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowwritingtools_false","children":[]}}]}]}}]}
```

[!INCLUDE [graph-explorer-steps](../../../includes/graph-explorer-steps.md)]

---
