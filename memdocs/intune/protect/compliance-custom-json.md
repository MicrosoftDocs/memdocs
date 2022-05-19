---
# required metadata

title: Create a JSON file for custom compliance settings in Microsoft Intune
description: Create the JSON file that defines custom settings and values for use with device compliance policies in Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/08/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Custom compliance JSON files

To support [custom settings for compliance](../protect/compliance-use-custom-settings.md), you create a JSON file that identifies the settings and value pairs that you want to use for custom compliance. The JSON defines what a PowerShell discovery script will evaluate for compliance on the device.

You’ll upload the JSON file when you create a compliance policy that includes custom compliance settings. 

A correctly formatted JSON file must include the following information:

- **SettingName** - The name of the custom setting to use for base compliance.
- **Operator** - Represents a specific action that is used to build a compliance rule. For options, see the following list of supported operators.
- **DataType** - The type of data that you can use to build your compliance rule. For options, see the following list of supported DataTypes.
- **Operand** - Represent the values that the operator works on.
- **MoreInfoURL** - A URL that’s shown to device users so they can learn more about the compliance requirement when their device is noncompliant for a setting. You can also use this to link to instructions to help users bring their device into compliance for this setting.
- **RemediationStrings** - Information that gets displayed in the Company Portal when a device is noncompliant to a setting. This information is intended to help users understand the remediation options to bring a device to a compliant state.

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
          }
       ]
    },
    { 
       "SettingName":"ModelName",
       "Operator":"IsEquals",
       "DataType":"String",
       "Operand":"Inspiron",
       "MoreInfoUrl":"https://bing.com",
       "RemediationStrings":[ 
          { 
             "Language": "en_US",
             "Title": "Only Inspiron is supported.",
             "Description": "Only desktop model Inspiron is allowed."
          }
       ]
    }
 ]
}
```

## Next steps

- [Use custom compliance settings](../protect/compliance-use-custom-settings.md)  
- [Create a PowerShell script for discovery of custom compliance settings](../protect/compliance-custom-script.md)  
- [Create a compliance policy](../protect/create-compliance-policy.md)  
