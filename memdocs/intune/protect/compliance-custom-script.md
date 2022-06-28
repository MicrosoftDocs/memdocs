---
# required metadata

title: Create a PowerShell script to use for discover of custom compliance settings in Microsoft Intune
description: Create the PowerShell script that runs discovery on devices that receive device compliance policies for custom settings in Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/16/2021
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

# Custom PowerShell scripts for discovery

Before you can use [custom settings for compliance](../protect/compliance-use-custom-settings.md) with Intune, you must define a PowerShell script for discovery of custom compliance settings on devices.

The discovery script:

- Is added to Intune before you create a compliance policy. After it's added, it will be available to select when you create a compliance policy with custom settings.
- Runs on a device that receives the compliance policy. The script evaluates the conditions of the JSON file you upload to the same policy.
- Identifies one or more settings, as defined in the JSON, and returns a list of discovered values for those settings. A single script can be assigned to each policy, and supports discovery of multiple settings.
- Must be compressed to output results in one line. For example: `$hash = @{ ModelName = "Dell"; BiosVersion = "1.24"; TPMChipPresent = $true}`
- Must include the following line at the end of the script: `return $hash | ConvertTo-Json -Compress`

## Sample discovery script

The following example is a sample PowerShell script.

```powershell
$WMI_ComputerSystem = Get-WMIObject -class Win32_ComputerSystem
$WMI_BIOS = Get-WMIObject -class Win32_BIOS 
$TPM = Get-Tpm

$hash = @{ ModelName = $WMI_ComputerSystem.Model; BiosVersion = $WMI_BIOS.SMBIOSBIOSVersion; TPMChipPresent = $TPM.TPMPresent}
return $hash | ConvertTo-Json -Compress
```

The following example is the output of the sample script:

```powershell
PS C:\Users\apervaiz\Documents> .\sample.ps1
{"ModelName":  "Dell","BiosVersion":  1.24,"TPMChipPresent":  true}
```

## Add a discovery script to Intune

1. Sign into Microsoft Endpoint Manager admin center and go to  **Endpoint security** > **Device compliance** > **Scripts** > **Add** > **Windows 10 and later**.
2. On **Basics**, provide a *Name*.
3. On **Settings**, add your script to *Detection script*. Review your script carefully. Intune doesn’t validate the script for syntax or programmatic errors.
4. On **Settings**, configure the following behavior for the script:

   - **Run this script using the logged on credentials** – By default, the script runs in the System context on the device. Set this value to Yes to have it run in the context of the logged-on user. If the user isn’t logged in, the script defaults back to the System context.
   - **Enforce script signature check** – For more information, see [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing?view=powershell-7.1&preserve-view=true) in the PowerShell documentation.
   - **Run script in 64 bit PowerShell Host** – By default, the script runs using the 32-bit PowerShell host. Set this value to *Yes* to force the script to run using the 64-bit host instead.

5. Complete the script creation process. The script is now visible in the *Scripts* pane of the Microsoft Endpoint Manager admin center and will be available to select when configuring compliance policies.

## Next steps

- [Use custom compliance settings](../protect/compliance-use-custom-settings.md)  
- [Create a JSON for custom compliance](../protect/compliance-custom-json.md)
- [Create a compliance policy](../protect/create-compliance-policy.md)
