---
# required metadata

title: Use custom compliance settings in Microsoft Intune
description: Use PowerShell and JSON files to define custom settings for device compliance policies in Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/15/2022
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

# Use custom compliance settings with Intune

To expand on Intune’s built-in device compliance options, you can add custom compliance settings to compliance policies for managed devices.
This feature applies to:

- Windows 10/11

Custom compliance uses JSON files and PowerShell scripts that you create and upload to Intune to add custom settings to your compliance policies. Your custom compliance settings can then deploy in the same policies as the built-in compliance settings that are available from within the Microsoft Endpoint Manager admin center. Custom settings provide flexibility to base compliance on the settings that are available on a device without having to wait for those settings to be added to Intune.

Before you can add custom settings to a policy, you’ll need to prepare the PowerShell script and JSON file:

- The PowerShell script runs on a device to discover and report on the settings defined in the JSON. You upload scripts to the Microsoft Endpoint Manager admin center before you create a policy, and then select a single script when configuring the policy. The policy assigns the script to the device at the time the policy is evaluated. Each compliance policy supports a single script, and each script can detect multiple settings.

- The JSON file defines the settings you want to base your custom compliance on, and the acceptable values for those settings. You can also configure messages for users to tell them how to restore compliance for each setting. You'll upload the file when you create a compliance policy that includes custom compliance settings.

After you’ve deployed custom compliance settings and devices have reported back, you'll be able to view the results alongside the built-in compliance setting details in the Microsoft Endpoint Manager admin center.  Custom compliance settings can be used for conditional access decisions, the same way built-in compliance settings are.  Together they form a compound rule set, equally affecting the device compliance state.

## Prerequisites

- **Azure Active Directory (Azure AD) joined** devices, *including* hybrid Azure AD-joined devices. 

  Hybrid Azure AD-joined devices are devices that are joined to Azure AD and also joined to on-premises Active Directory. For more information, see [Plan your hybrid Azure AD join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan).
  
  Devices that aren't Azure AD joined or aren't hybrid Azure AD-joined are evaluated as not applicable.

- **PowerShell discovery script** - A script that you create that runs on a device to discover the custom settings defined in your JSON file. The script returns the configuration value of those settings to Intune. You need to upload your script to the Microsoft Endpoint Manager admin center before you create a compliance policy and then select the script you want to use when creating a policy.

  To create a custom compliance script, see [Custom PowerShell scripts for discovery](../protect/compliance-custom-script.md).

- **JSON file** - The  JSON file defines the custom settings and the value that is to be considered as compliant and can contain messages for users on how to restore the device to compliance for the setting. You upload your JSON file while creating a compliance policy, just after you select a discovery script for that policy.

  To create a JSON file for compliance, see [Custom compliance JSON files](../protect/compliance-custom-json.md)

## Create a policy with custom compliance settings

Before starting:

1. Create and upload a PowerShell script to use for discovery.  See [Custom PowerShell scripts for  discovery](../protect/compliance-custom-script.md).

2. Prepare a JSON file that you’ll upload while creating the policy. See [Custom compliance JSON files](../protect/compliance-custom-json.md).

3. When both the script and JSON are ready, start with your normal procedure to create a compliance policy, and on the *Configuration settings* page, configure custom compliance by following the steps in the following procedure.

### Configure custom compliance settings

Configure custom settings during the workflow to create a compliance policy:

1. On the *Compliance settings* page, expand the *Custom Compliance* category.

2. Set *Custom compliance* to **Require**.

3. For *Select your discovery script*, select *Click to select* and then specify a script that’s been [previously added](../protect/compliance-custom-script.md) to the Microsoft Endpoint Manager admin center. This script must be uploaded before you begin to create the policy.

4. For *Upload and validate the JSON file with your custom compliance settings*,  select the folder icon and then locate and add the JSON file you want to use with this policy. To create your JSON, see [Custom compliance JSON files](../protect/compliance-custom-json.md).

   The JSON you select is validated and any problems are displayed. After validation of the JSON contents, the rules from the JSON are displayed in table format.

5. Complete the compliance policy creation task and assign the policy to devices.

> [!NOTE]  
> When a Windows device receives a compliance policy with custom settings, it checks for the presence of [Intune Management Extensions](../apps/intune-management-extension.md). If not found, the device runs an MSI that installs the extensions, enabling the client to download and run PowerShell scripts that are part of a compliance policy, and to upload compliance results. Actions managed by the services include:
>
> - Checking for new or updated PowerShell scripts every eight hours.
> - Running the discovery scripts every eight hours.
> - Running scripts that download when a user selects Check Compliance on the device. However, there is no check for new or updated scripts when Check Compliance is run.
> 
> It is not possible to push notifications to a device to enable custom compliance to run on demand.

## Monitor custom compliance policy

You can view per-setting device compliance details for custom compliance settings.

For more information on monitoring, see [Monitor Intune Device compliance policies](../protect/compliance-policy-monitor.md).

## Troubleshooting

### Custom settings aren’t evaluated

Check the device compliance reports for the following error codes and insight into the problem:

- 65007: Script returned failure  
- 65008: Setting missing in the script result
- 65009: Invalid json for the discovered setting
- 65010: Invalid datatype for the discovered setting

To see errors related to the PowerShell script, ensure the following line is at the end of the PowerShell script file: `return $hash | ConvertTo-Json -Compress`

### PowerShell scripts aren’t visible to select, or remain visible after being deleted

Refresh the current view. If the issue persists, cancel the policy creation flow, and start again.

### After an issue on a device is fixed, subsequent syncs don’t identify the issue as resolved and compliant

It can take up to eight hours before a noncompliant status shows as compliant after a change to the device.

### Can a user manually check for compliance after fixing an issue on a device in order to identify if the issue is resolved and compliant? 

Yes, a user can go to the [Company Portal website](https://portal.manage.microsoft.com) and trigger a sync to update the device status after fixing a non-compliant custom compliance setting. 

### Why aren’t more operators and operands supported?

Contact your account manager to request the addition of specific operators and operands. They can then be considered for a future update.

### Why can’t I apply multiple PowerShell discovery scripts to one custom compliance policy?

Policies support the use of a single PowerShell script. However, each script supports checking for multiple compliance values.

## Next steps

- [Create a JSON for custom compliance](../protect/compliance-custom-json.md)
- [Create a PowerShell script for discovery of custom compliance settings](../protect/compliance-custom-script.md)
- [Create a compliance policy](../protect/create-compliance-policy.md)
