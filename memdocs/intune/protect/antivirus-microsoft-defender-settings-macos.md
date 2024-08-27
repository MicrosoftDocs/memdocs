---
title: macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile for macOS. This profile is s part of Endpoint security Antivirus policy for macOS in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/10/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-secure-endpoints
ms.reviewer: laarrizz 
---

# Settings for Microsoft Defender for Endpoint for Mac in Microsoft Intune

View the *Microsoft Defender Antivirus* profile settings you can configure for Microsoft Defender for Endpoint for Mac in Microsoft Intune. For more information about these settings, see [Microsoft Defender for Endpoint for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) in the Windows documentation.

Learn about using [Endpoint security policies](../protect/endpoint-security-policy.md) in Intune.

## Cloud delivered protection preferences

For details about these settings, see the settings entry in [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) in the Microsoft Defender for Endpoint documentation.

- **Enable / disable cloud delivered protection**
  - *Not configured* (*default*)
  - *Enabled*
  - *Disabled*

- **Enable / disable automatic sample submissions**
  - *Not configured* (*default*)
  - *Enabled*
  - *Disabled*

- **Diagnostic collection level**
  - *Not configured* (*default*)
  - *Optional*
  - *Required*

- **Automatic security intelligence updates**
  - *Not configured* (*default*)
  - *Enabled*
  - *Disabled*

## Antivirus engine

For details about these settings, see the settings entry in [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) in the Microsoft Defender for Endpoint documentation.

- **Enable real-time protection (deprecated)**  - This setting is replaced by *Enforcement level*.
  - *Not configured* (*default*)
  - *Enabled*
  - *Disabled*

- **Enable passive mode (deprecated)** - This setting is replaced by *Enforcement level*.
  - *Not configured* (*default*)
  - *Enabled*
  - *Disabled*

- **Enforcement level**  
  - *Passive* (*default*)
  - *Real time*
  - *On Demand*

- **Scan history size**
  - *Not configured* (*default*)
  - *Configured* - When configured, specify a number of entries to keep in scan history.

- **Scan results retention**
  - *Not configured* (*default*)
  - *Configured* - When configured, specify the number of days that results are retained in the scan history on the device.

- **Exclusions merge**
  - *Not configured* (*default*)
  - *Admin_only*
  - *Merge*

- **Scan exclusions**
  - *Configured* (*default*)
  - *Not configured*

- **Threat type settings**
  - *Configured* (*default*)
  - *Not configured*

- **Threat type settings merge**
  - *Not configured* (*default*)
  - *Admin_only*
  - *Merge*

- **Allowed threats**
  - *Not configured* (*default*)
  - *Configured*

- **Disallowed threat actions**
  - *Not configured* (*default*)
  - *Configured*

- **Degree of parallelism for on-demand scans**
  - *Configured* (*default*) (2)
  - *Not configured*

- **Enable file hash computation**
  - *False* (*default*)
  - *True*
  - *Not configured*

- **Run a scan after definitions are  updated**
  - *Enabled* (*default*)
  - *Disabled*
  - *Not configured*

- **Scanning inside archive files**
  - *False* (*default*)
  - *True*
  - *Not configured*

## Network protection

- **Enforcement level**
  - *Audit* (*default*)
  - *Disabled*
  - *Block*
  - *Not configured*

## Tamper protection

- **Enforcement level**
  - *Audit* (*default*)
  - *Disabled*
  - *Block*
  - *Not configured*

## User interface preferences

For details about these settings, see the settings entry in [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) in the Microsoft Defender for Endpoint documentation.

- **Control sign-in to consumer version**
  - *Enabled* (*default*)
  - *Disabled*
  - *Not configured*

- **Show / hide status menu icon**
  - *Disabled* (*default*)
  - *Enabled*
  - *Not configured*

- **User initiated feedback**
  - *Enabled* (*default*)
  - *Disabled*
  - *Not configured*
