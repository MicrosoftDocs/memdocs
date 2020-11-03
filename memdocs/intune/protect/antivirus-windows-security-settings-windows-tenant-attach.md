---
# required metadata

title: Windows 10 Antivirus policy settings from Windows security settings for tenant attached devices | Microsoft Docs
description: Review the settings in the *Windows Security experience* profile for tenant attached devices. To use this Endpoint security Antivirus policy, you must first configure tenant attach for Configuration Manager for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---

# Settings for Windows Security experience Antivirus policy for tenant attached devices in Microsoft Intune

View the Windows Security experience settings you can manage with the **Windows Security experience (preview)** profile from Intune.

The profile is available when you configure [Intune Endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md). This profile supports devices you manage with Configuration Manager after configuring the [tenant attach](../protect/tenant-attach-intune.md) scenario for Intune.

**Windows Security**  

- **Enable tamper protection to prevent Microsoft Defender being disabled**  
  [Learn about Tamper Protection](/windows/security/threat-protection/microsoft-defender-antivirus/prevent-changes-to-security-settings-with-tamper-protection)  

  By default, no value is configured, and you must select an option: 
  - **Not configured** (*default*) - When the *Enable* or *Disable* state exists on a client, deploying *Not configured* has no impact on the setting.
  - **Enable** - Enable the Tamper Protection restriction. To change the state from either enabled or disabled, deploy the opposite setting to have effect.
  - **Disable** - Disable the Tamper Protection restrictions. To change the state from either enabled or disabled, deploy the opposite setting to have effect.