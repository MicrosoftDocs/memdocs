---
# required metadata

title: Create a JSON file for custom compliance settings in Microsoft Intune
description: Create the JSON file that defines custom settings and values for use with device compliance policies in Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2024
ms.topic: concept-article
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- compliance
- sub-device-compliance
---

# Custom compliance JSON files for Microsoft Intune

To support [custom settings for compliance](../protect/compliance-use-custom-settings.md) for Microsoft Intune, you create a JSON file that identifies the settings and value pairs that you want to use for custom compliance. The JSON defines what a discovery script evaluates for compliance on the device.

You include the JSON file in a compliance policy when you configure a policy to assess custom compliance settings.

This feature applies to:

- Linux – Ubuntu Desktop, version 20.04 LTS and 22.04 LTS
- Windows 10/11

A correctly formatted JSON file must include the following information:

- **SettingName** - The name of the custom setting to use for base compliance. This name is case-sensitive.
- **Operator** - Represents a specific action that is used to build a compliance rule. For options, see the following list of *supported operators*.
- **DataType** - The type of data that you can use to build your compliance rule. For options, see the following list of *supported DataTypes*.
- **Operand** - Represent the values that the operator works on.
- **MoreInfoURL** - A URL that device users can view and use to learn more about the compliance requirement should their device be noncompliant for a setting. You can also use this URL to link to instructions to help users bring their device into compliance for this setting.
- **RemediationStrings** - Information that gets displayed in the Company Portal when a device is noncompliant to a setting. This information is intended to help users understand the remediation options to bring a device to a compliant state. There must be at least one string for the language `en_US`. Other remediation string languages can then be added as needed, as demonstrated in the [example](#example-json-file) provided later in this article.

Your policy can be up to 100 KB and include 100 rules.

**Supported operators**:

- IsEquals
- NotEquals
- GreaterThan
- GreaterEquals
- LessThan
- LessEquals

**Supported DataTypes**:

- Boolean
- Int64
- Double
- String
- DateTime
- Version

**Supported Languages**:

- cs_CZ
- da_DK
- de_DE
- el_GR
- en_US
- es_ES
- fi_FI
- fr_FR
- hu_HU
- it_IT
- ja_JP
- ko_KR
- nb_NO
- nl_NL
- pl_PL
- pt_BR
- ro_RO
- ru_RU
- sv_SE
- tr_TR
- zh_CN
- zh_TW

For more information, see [Available languages for Windows](/windows-hardware/manufacture/desktop/available-language-packs-for-windows).

## Example JSON file

```json
{
"Rules":[ 
    { 
       "SettingName":"BiosVersion",
       "Operator":"GreaterEquals",
       "DataType":"Version",
       "Operand":"2.3",
       "MoreInfoUrl":"https://bing.com",
       "RemediationStrings":[ 
          { 
             "Language":"en_US",
             "Title":"BIOS Version needs to be upgraded to at least 2.3. Value discovered was {ActualValue}.",
             "Description": "BIOS must be updated. Please refer to the link above"
          },
          {
             "Language":"de_DE",
             "Title":"BIOS-Version muss auf mindestens 2.3 aktualisiert werden. Der erkannte Wert lautet {ActualValue}.",
             "Description": "BIOS muss aktualisiert werden. Bitte beziehen Sie sich auf den obigen Link"
          }
       ]
    },
    { 
       "SettingName":"TPMChipPresent",
       "Operator":"IsEquals",
       "DataType":"Boolean",
       "Operand":true,
       "MoreInfoUrl":"https://bing.com",
       "RemediationStrings":[ 
          {
             "Language": "en_US",
             "Title": "TPM chip must be enabled.",
             "Description": "TPM chip must be enabled. Please refer to the link above"
          },
          {
             "Language": "de_DE",
             "Title": "TPM-Chip muss aktiviert sein.",
             "Description": "TPM-Chip muss aktiviert sein. Bitte beziehen Sie sich auf den obigen Link"
          }
       ]
    },
    {
       "SettingName":"Manufacturer",
       "Operator":"IsEquals",
       "DataType":"String",
       "Operand":"Microsoft Corporation",
       "MoreInfoUrl":"https://bing.com",
       "RemediationStrings":[ 
          { 
             "Language": "en_US",
             "Title": "Only Microsoft devices are supported.",
             "Description": "You are not currently using a Microsoft device."
          },
          {
             "Language": "de_DE",
             "Title": "Nur Microsoft-Geräte werden unterstützt.",
             "Description": "Sie verwenden derzeit kein Microsoft-Gerät."
          }
       ]
    }
 ]
}
```

## Next steps

- [Use custom compliance settings](../protect/compliance-use-custom-settings.md)  
- [Create a discovery script for custom compliance settings](../protect/compliance-custom-script.md)  
- [Create a compliance policy](../protect/create-compliance-policy.md)
