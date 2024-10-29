---
# required metadata

title: Settings list for the Microsoft Edge security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Edge browser. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/26/2024
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

This article is a reference for the settings that are available in the different versions of the Microsoft Edge security baseline that you can deploy with Microsoft Intune. You can use the tabs below to select and view the settings in the current baseline version and a few older versions that might still be in use.

For each setting you’ll find the baselines default configuration, which is also the recommended configuration for that setting provided by the relevant security team. Because products and the security landscape evolve, the recommended defaults in one baseline version might not match the defaults you find in later versions of the same baseline. Different baseline types could also set different defaults.

<!--When the Intune UI includes a *Learn more* link for a setting, you’ll find that here as well. Use that link to view the settings *policy configuration service provider* (CSP) or relevant content that explains the settings operation. -->
Although the settings in the Intune UI for this baseline omit *Learn more* links, this article includes links to relevant content.

When a new version of a baseline becomes available, it replaces the previous version. Profiles instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see [Use security baselines](security-baselines.md). In that article you'll also find information about how to:

<!-- - [Compare baselines](../protect/security-baselines.md) to discover what's changed from version to version.  -->
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format) to update a profile to use the latest version of that baseline.

::: zone pivot="edge-sept-2020"
**Microsoft Edge baseline for September 2020 (Edge version 85)**  
::: zone-end
::: zone pivot="edge-april-2020"
**Microsoft Edge baseline for April 2020 (Edge version 80)**  
::: zone-end
::: zone pivot="edge-october-2019"
**Microsoft Edge baseline for October 2019**

> [!NOTE]
> The Microsoft Edge baseline for October 2019 is in Public Preview.
::: zone-end

## Microsoft Edge

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
