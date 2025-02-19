---
title: Common Education iPads with no user affinity configuration
description: Learn about common iPads with no user affinity configuration used by Education organizations in Intune.
ms.date: 10/16/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Apple]
ms.collection: 
- graph-interactive
ms.service: microsoft-intune
ms.subservice: education
---

# iPads with no user affinity

iPads used in earlier grades are commonly enrolled with no user affinity to simplify the user experience for younger students and to allow sharing of devices. For more information, please refer to [Enroll devices with Automated Device Enrollment](/mem/intune/industry/education/tutorial-school-deployment/enroll-ios-ade).

These iPads generally have additional restrictions that are not suitable for 1:1 devices.

To learn more, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](/mem/intune/configuration/settings-catalog)
- [Restrictions payload](https://developer.apple.com/documentation/devicemanagement/restrictions)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## [**Settings**](#tab/settings)

| **Category** | **Property** | **Value** | **Notes** | **Payload property** |
|---|---|:---:|---|---|
| Restrictions | **:::no-loc text="Allow Account Modification":::** | False | Disables modification of accounts such as Apple IDs and Internet-based accounts such as Mail, Contacts, and Calendar. | [:::no-loc text="allowAccountModification":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Bookstore":::** | False | Removes the Book Store tab from the Books app. | [:::no-loc text="allowBookstore":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Enterprise Book Backup":::** | False | Disables backup of Enterprise books. | [:::no-loc text="allowEnterpriseBookBackup":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Enterprise Book Metadata Sync":::** | False | Disables sync of Enterprise books, notes, and highlights. | [:::no-loc text="allowEnterpriseBookMetadataSync":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Fingerprint For Unlock":::** | False | Prevents Touch ID or Face ID from unlocking a device. | [:::no-loc text="allowFingerprintForUnlock":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Fingerprint Modification":::** | False | Prevents the user from modifying Touch ID or Face ID. | [:::no-loc text="allowFingerprintModification":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Passcode Modification":::** | False | Prevents adding, changing, or removing the passcode. | [:::no-loc text="allowPasscodeModification":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Allow Password Auto Fill":::** | False | | [:::no-loc text="allowPasswordAutoFill":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |
| Restrictions | **:::no-loc text="Safari Allow Autofill":::** | False | Disables Safari AutoFill for passwords, contact info, and credit cards and also prevents using the Keychain for AutoFill. | [:::no-loc text="safariAllowAutoFill":::](https://developer.apple.com/documentation/devicemanagement/restrictions) |

## [:::image type="icon" source="../../../media/icons/graph.svg"::: **Create policy using Graph Explorer**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **:::no-loc text="_MSLearn_Example_CommonEDU - iPads - No user affinity":::**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_CommonEDU - iPads - No user affinity","description":"","platforms":"iOS","technologies":"mdm,appleRemoteManagement","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationGroupSettingCollectionInstance","settingDefinitionId":"com.apple.applicationaccess_com.apple.applicationaccess","groupSettingCollectionValue":[{"children":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowaccountmodification","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowaccountmodification_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowbookstore","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowbookstore_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowenterprisebookbackup","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowenterprisebookbackup_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowenterprisebookmetadatasync","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowenterprisebookmetadatasync_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowfingerprintforunlock","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowfingerprintforunlock_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowfingerprintmodification","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowfingerprintmodification_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowpasscodemodification","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowpasscodemodification_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_allowpasswordautofill","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_allowpasswordautofill_false","children":[]}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"com.apple.applicationaccess_safariallowautofill","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"com.apple.applicationaccess_safariallowautofill_false","children":[]}}]}]}}]}
```

[!INCLUDE [graph-explorer-steps](../../../includes/graph-explorer-steps.md)]

---
