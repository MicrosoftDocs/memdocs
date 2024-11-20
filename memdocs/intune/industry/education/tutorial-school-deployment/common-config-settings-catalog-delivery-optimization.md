---
title: Common Education Windows Delivery Optimization configuration
description: Learn about common Windows Delivery Optimization configuration used by Education organizations in Intune.
ms.date: 5/2/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows, Autopatch, Autopilot]
ms.collection: 
- graph-interactive
---

# Delivery Optimization

There are many configuration options you can set in Delivery Optimization to customize the content delivery experience specific to your environment needs. This article summarizes the configurations that are most commonly used for student and teacher devices.

Windows Delivery Optimization helps you get Windows updates and Microsoft Store apps more quickly and reliably. It works by letting you get Windows updates and Microsoft Store apps from sources in addition to Microsoft, like other PCs on your local network, or PCs on the internet that are downloading the same files. Delivery Optimization also sends updates and apps from your PC to other PCs on your local network or PCs on the internet, based on your settings. Sharing this data between PCs helps reduce the internet bandwidth that's needed to keep more than one device up to date or can make downloads more successful if you have a limited or unreliable internet connection. Delivery Optimization creates a local cache, and stores files that it has downloaded in that cache for a short period of time.

To learn more, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)
- [Delivery Optimization reference](/windows/deployment/do/waas-delivery-optimization-reference)
- [YouTube: Delivery Optimization](https://www.youtube.com/playlist?list=PLMuDtq95SdKtN9lntgTcuhsYCsSQR4Dyl)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## [**Settings**](#tab/settings)

| **Name** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **:::no-loc text="DO Delay Background Download From Http":::** | 3600 | 1 hour in seconds. After the max delay is reached, the download will resume using HTTP, either downloading the entire payload or complementing the bytes that couldn't be downloaded from Peers. | [:::no-loc text="DODelayBackgroundDownloadFromHttp":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodelaybackgrounddownloadfromhttp) |
| **:::no-loc text="DO Download Mode":::** | HTTP blended with peering behind the same NAT. | Delivery Optimization enables peer sharing on the same network between clients that connect to the Internet using the same public IP.  | [:::no-loc text="DODownloadMode":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodownloadmode) |
| **:::no-loc text="DO Max Cache Age":::** | 1209600 | 14 days in seconds. Specifies the maximum time in seconds that each file is held in the Delivery Optimization cache after downloading successfully. | [:::no-loc text="DOMaxCacheAge":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#domaxcacheage) |
| **:::no-loc text="DO Min Disk Size Allowed To Peer":::** | 100 | Specifies the required minimum disk size (capacity in GB) for the device to use Peer Caching. Recommended values: 64 GB to 256 GB.Adjust as necessary according to your hardware. | [:::no-loc text="DOMinDiskSizeAllowedToPeer":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#domindisksizeallowedtopeer) |
| **:::no-loc text="DO Min File Size To Cache":::** | 5 | Specifies the minimum content file size in MB enabled to use Peer Caching. | [:::no-loc text="DOMinFileSizeToCache":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominfilesizetocache) |
| **:::no-loc text="DO Min RAM Allowed To Peer":::** | 2 | Specifies the minimum RAM size in GB required to use Peer Caching. | [:::no-loc text="DOMinRAMAllowedToPeer":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominramallowedtopeer) |
| **:::no-loc text="DO Restrict Peer selection By":::** | Subnet mask | Set this policy to restrict peer selection | [:::no-loc text="DORestrictPeerSelectionBy":::](/windows/client-management/mdm/policy-csp-deliveryoptimization#dorestrictpeerselectionby) |

## [:::image type="icon" source="../../../media/icons/graph.svg"::: **Create policy using Graph Explorer**](#tab/graph)

[!INCLUDE [graph-explorer-introduction](../../../includes/graph-explorer-intro.md)]

This will create a policy in your tenant with the name **_MSLearn_Example_CommonEDU - Windows - Delivery Optimization**.

```msgraph-interactive
POST https://graph.microsoft.com/beta/deviceManagement/configurationPolicies
Content-Type: application/json

{"name":"_MSLearn_Example_CommonEDU - Windows - Delivery Optimization","description":"https://aka.ms/ManageEduDevices","platforms":"windows10","technologies":"mdm","roleScopeTagIds":["0"],"settings":[{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_dodelaybackgrounddownloadfromhttp","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","value":3600}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_dodownloadmode","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_deliveryoptimization_dodownloadmode_1","children":[]}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_domaxcacheage","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","value":1209600}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_domindisksizeallowedtopeer","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","value":100}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_dominfilesizetocache","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","value":5}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSimpleSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_dominramallowedtopeer","simpleSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationIntegerSettingValue","value":2}}},{"@odata.type":"#microsoft.graph.deviceManagementConfigurationSetting","settingInstance":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingInstance","settingDefinitionId":"device_vendor_msft_policy_config_deliveryoptimization_dorestrictpeerselectionby","choiceSettingValue":{"@odata.type":"#microsoft.graph.deviceManagementConfigurationChoiceSettingValue","value":"device_vendor_msft_policy_config_deliveryoptimization_dorestrictpeerselectionby_1","children":[]}}}]}
```

[!INCLUDE [graph-explorer-steps](../../../includes/graph-explorer-steps.md)]

---
