---
# required metadata

title: Settings list for the Microsoft Edge security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Edge browser. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/09/2025
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.assetid:

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
zone_pivot_groups: edge-baseline-versions
---

# List of the settings in the Microsoft Edge security baseline in Intune

This article is a reference for the settings that are available in the Microsoft Edge security baseline for Microsoft Intune.

In May 2023, the settings for the Microsoft Edge baselines updated to a new format. This article provides a reference for Microsoft Edge baselines version 85 and earlier. To view the settings reference for newer baselines, see [Microsoft Edge security baseline settings reference for Microsoft Intune](../protect/security-baseline-v2-edge-settings.md).

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

The details that display in this article are based on baseline version you select at the top of the article. For each version, this article displays:

- A list of each setting with its configuration as found in the default instance of that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and possibly additional details for a settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:
- [Use security baselines](../protect/security-baselines.md)
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format)
- [Manage security baselines](../protect/security-baselines-configure.md)



::: zone pivot="edge-sept-2020"
## Microsoft Edge baseline for September 2020 (Edge version 85)

::: zone-end
::: zone pivot="edge-april-2020"
## Microsoft Edge baseline for April 2020 (Edge version 80)
::: zone-end
::: zone pivot="edge-october-2019"
## Microsoft Edge baseline for October 2019

> [!NOTE]
> The Microsoft Edge baseline for October 2019 is a Public Preview.
::: zone-end

### Microsoft Edge

::: zone pivot="edge-sept-2020,edge-april-2020"

- **Supported authentication schemes**  
  Baseline default: *Enabled*  
  [Learn more](/deployedge/microsoft-edge-policies#authschemes)
  
  - **Supported authentication schemes**  
    Baseline defaults: Two items: *NTLM* and *Negotiate*

- **Default Adobe Flash setting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)

  - **Default Adobe Flash setting**  
    Baseline default: *Block the Adobe Flash plugin*  
    [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*  

  - **Extension IDs the user should be prevented from installing (or * for all)**  
    Baseline default: *Not configured by default. Manually add one or more Extension IDs*

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*  

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

- **Enable site isolation for every site**  
  Baseline default: *Enabled*  

  *Microsoft Edge also supports [IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) policy that can isolate additional, finer-grained origins.  Intune doesn't support configuring the IsolateOrigins policy.*
  
- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  

  *This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.*

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*  

  *This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.*

- **Allow users to proceed from the SSL warning page**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

- **Minimum SSL version enabled**  
  Baseline default: *Enabled*  

  - **Minimum SSL version enabled**  
    Baseline default: *TLS 1.2*  

::: zone-end
::: zone pivot="edge-october-2019"

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Minimum SSL version enabled**  
  Baseline default: *Enabled*  

  - **Minimum SSL version enabled**  
    Baseline default: *TLS 1.2*

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

- **Allow users to proceed from the SSL warning page**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

- **Default Adobe Flash setting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)

  - **Default Adobe Flash setting**  
    Baseline default: *Block the Adobe Flash plugin*  
    [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

- **Enable site isolation for every site**  
  Baseline default: *Enabled*  

  *Microsoft Edge also supports [IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) policy that can isolate additional, finer-grained origins.  Intune doesn't support configuring the IsolateOrigins policy.*

- **Supported authentication schemes**  
  Baseline default: *Enabled*  
  [Learn more](/deployedge/microsoft-edge-policies#authschemes)
  
  - **Supported authentication schemes**  
    Baseline defaults: Two items: *NTLM* and *Negotiate*

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*  

  - **Extension IDs the user should be prevented from installing (or * for all)**  
    Baseline default: *Not configured by default. Manually add one or more Extension IDs*

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  *This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management*.

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*  

::: zone-end
::: zone pivot="edge-sept-2020"

- **Allow certificates signed using SHA-1 when issued by local trust anchors (deprecated)**  
  Baseline default: *Disabled*  

  > [!IMPORTANT]
  > This setting is deprecated. It is currently supported but will become obsolete in a future release.

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
