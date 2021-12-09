---
title: macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile for macOS. This profile is s part of Endpoint security Antivirus policy for macOS in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2020
ms.topic: conceptual
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
ms.reviewer: samyada

---

# Settings for Microsoft Defender for Endpoint for Mac in Microsoft Intune

View the *Antivirus* profile settings you can configure for Microsoft Defender for Endpoint for Mac in Microsoft Intune. For more information about these settings, see [Microsoft Defender for Endpoint for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) in the Windows documentation.

Learn about using [Endpoint security policies](../protect/endpoint-security-policy.md) in Intune.

**Microsoft Defender for Endpoint**

- **Real-time protection**  
  Require Defender on macOS devices to use the real-time Monitoring functionality. Real-time monitoring locates and stops malware from installing or running on your device. You can turn off this setting for a short time before it turns back on automatically.

  - **Not configured** (*default*) - The setting is restored to the system default
  - **Enabled** - Enforce use of real-time monitoring. Device users can't change this setting.
  - **Disabled** - The setting is disabled. Device users can't change this setting.

- **Cloud-delivered protection**  
  By default, Defender sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions. Protection Works best when *Automatic sample submission* is set on.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Enabled** - Cloud-delivered protection is turned on. Device users can't change this setting.
  - **Disabled** - The setting is disabled. Device users can't change this setting.

- **Automatic sample submission**  
  Sends sample files to Microsoft to help protect device users and your organization from potential threats.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Enabled** - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Disabled** - The setting is disabled. Device users can't change this setting.

- **Diagnostic data collection**

  Configure how diagnostic and usage data is shared with Microsoft.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **Required**
  - **Optional**

- **Folders excluded from scan**  
  Select **Add** and then specify folders to ignore during a scan.

- **Files excluded from scan**  
  Select **Add** and then specify files to ignore during a scan.

- **File types excluded from scan**  
  Select **Add** and then specify file extensions to ignore during a scan.

- **Processes excluded from scan**  
  Select **Add** and then specify processes to ignore during a scan.