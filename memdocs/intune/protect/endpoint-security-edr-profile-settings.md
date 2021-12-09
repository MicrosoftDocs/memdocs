---
# required metadata

title: Intune endpoint security Endpoint detection and response settings | Microsoft Docs
description: Endpoint security Endpoint detection and response policy settings in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2020
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
ms.reviewer: mattcall

---
# Endpoint detection and response policy settings for endpoint security in Intune

View the settings you can configure in profiles for [Endpoint detection and response policy](../protect/endpoint-security-edr-policy.md) in the endpoint security node of Intune.

Applies to:

- Windows 10
- Windows 11

Supported platforms and profiles:

- **Windows 10 and later**: Use this platform for policy you deploy to Windows 10 and Windows 11 devices managed with Intune.
  - Profile: **Endpoint detection and response (MDM)**

- **Windows 10, Windows 11, and Windows Server (ConfigMgr)**: Use this platform for policy you deploy to devices managed by Configuration Manager.
  - Profile: **Endpoint detection and response (ConfigMgr)**

## Endpoint detection and response (MDM)

**Endpoint detection and response**:

- **Microsoft Defender for Endpoint client configuration package type**

  Upload a signed configuration package that will be used to onboard the Microsoft Defender for Endpoint client.

  - **Not configured** (*default*)
  - **Onboarding blob**  
  - **Offboarding blob**  

  When set to *Onboarding blob*, you can configure the following settings:

  - **Defender for Endpoint onboarding blob**  
    Click **Select onboarding file** to open the *Select onboarding File* pane, where you specify a `.onboarding` file.

  When set to *Offboarding blob*, you can configure the following settings:
  
  - **Defender for Endpoint offboarding blob**  
     Click **Select offboarding file** to open the *Select offboarding File* pane, where you specify a `.offboarding` file.

- **Sample sharing for all files**  

  Returns or sets the Microsoft Defender for Endpoint Sample Sharing configuration parameter.  Sample Sharing sends a file to Microsoft for deep analysis. Organizations can disable sample sharing on specific devices that are considered too sensitive.

  - **Not configured**   (*default*)
  - **Yes**

- **Expedite telemetry reporting frequency**

  - **Not configured**   (*default*)
  - **Yes** - Increase the Microsoft Defender for Endpoint telemetry reporting frequency.

## Endpoint detection and response (ConfigMgr)

**Endpoint detection and response**:

- **Sample sharing for all files**  

  Returns or sets the Microsoft Defender for Endpoint Sample Sharing configuration parameter.  
  - **Not configured**   (*default*)
  - **Yes**

- **Expedite telemetry reporting frequency**

  - **Not configured**   (*default*)
  - **Yes** - Increase the Microsoft Defender for Endpoint telemetry reporting frequency.

## Next steps

[Endpoint security policy for EDR](../protect/endpoint-security-edr-policy.md)
