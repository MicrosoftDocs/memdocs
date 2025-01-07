---
# required metadata

title: List of settings for the Microsoft Edge security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline version 112 and later, for the Microsoft Edge browser. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/027/2025
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

zone_pivot_groups: dcv2-edge-baselines

---

<!-- Pivot details: 

- id: dcv2-edge-baselines
  title: Microsoft Edge baseline versions
  prompt: Choose a version
  pivots:
    - id: edge-v128
      title: Edge v128 (January 2025)
    - id: edge-v112
      title: Edge v112 (May 2023)
    - id: edge-v117
      title: Edge v117 (November 2023)
-->

# Microsoft Edge security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft Edge security baseline for Microsoft Intune and applies to versions of that baseline that released in May 2023 or later.

If you use a security baseline for Microsoft Edge version 85 or earlier, see [List of the settings in the Microsoft Edge security baseline in Intune](../protect/security-baseline-settings-edge.md).

> [!NOTE]  
> Beginning in May 2023, all new security baseline versions use a new settings format that replaces previous versions. While the last version instance for a baseline that uses the older setting format remains available to use, the older format will no longer receive updates for new settings, or updated default configurations.

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

The details that are displayed in this article are based on baseline version that is selected at the top of the article. For each selection, this article displays:

- A list of each setting in that baseline version.
- The default configuration of each setting in that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation, or other related content from the relevant product group that provides context and possibly additional details for the settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.

  > [!TIP]  
  > Because the new baselines versions introduced in May 2023 or later exist side-by-side with the last baseline version from the older format, baselines for the last available version of that older format remain accessible to use and to edit.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:

- [Use security baselines](../protect/security-baselines.md)
- [Manage security baselines](../protect/security-baselines-configure.md).

::: zone pivot="edge-v128"
## Microsoft Edge baseline for version 128 (January 2025) 

For information about the most recent baseline versions and settings from Microsoft, including versions of this baseline that might not be available through Intune, download the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center.


- **Allow unconfigured sites to be reloaded in Internet Explorer mode**  
  Baseline default: *Disabled*
  
- **Allow users to proceed from the HTTPS warning page**  
  Baseline default: *Disabled*

- **Automatically open downloaded MHT or MHTML files from the web in Internet Explorer mode**  
  Baseline default: *Disabled*

- **Dynamic Code Settings**  
  Baseline default: *Enabled*

  - **Dynamic Code Settings (Device)**  
    Baseline default: *Default dynamic code settings*

- **Enable Application Bound Encryption**  
  Baseline default: *Enabled*

- **Enable browser legacy extension point blocking**  
  Baseline default: *Enabled*

- **Enable site isolation for every site**  
  Baseline default: *Enabled*

- **Show the Reload in Internet Explorer mode button in the toolbar**  
  Baseline default: *Disabled*

- **Specifies whether SharedArrayBuffers can be used in a non cross-origin-isolated context**  
  Baseline default: *Disabled*

### Extensions

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*

  - **Extension IDs the user should be prevented from installing (or * for all) (Device)**  
    Baseline default: *
  
### HTTP authentication

- **Allow Basic authentication for HTTP**  
  Baseline default: *Disabled*

- **Supported authentication schemes**  
  Baseline default: *Enabled*  
  [Learn more](/deployedge/microsoft-edge-policies#authschemes)

  - **Supported authentication schemes (Device)**  
    Baseline default: *ntlm,negotiate*

### Native Messaging

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*

### Private Network Request Settings

- **Specifies whether to allow insecure websites to make requests to more-private network endpoints**  
  Baseline default: *Disabled*

### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

### Typosquatting Checker settings

- **Configure Edge Typo Protection**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="edge-v117"

## Microsoft Edge baseline for version 117 (November 2023)

For information about the most recent baseline versions and settings from Microsoft, including versions of this baseline that might not be available through Intune, download the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center.

- **Allow unconfigured sites to be reloaded in Internet Explorer mode**  
  Baseline default: *Disabled*
  
- **Allow users to proceed from the HTTPS warning page**  
  Baseline default: *Disabled*

- **Automatically open downloaded MHT or MHTML files from the web in Internet Explorer mode**  
  Baseline default: *Disabled*

- **Enable browser legacy extension point blocking**  
  Baseline default: *Enabled*

- **Enable site isolation for every site**  
  Baseline default: *Enabled*

- **Enhance images enabled**  
  Baseline default: *Disabled*

- **Force WebSQL to be enabled**  
  Baseline default: *Disabled*

- **Show the Reload in Internet Explorer mode button in the toolbar**  
  Baseline default: *Disabled*

- **Specifies whether SharedArrayBuffers can be used in a non cross-origin-isolated context**  
  Baseline default: *Disabled*

### Extensions

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*

  - **Extension IDs the user should be prevented from installing (or * for all) (Device)**  
    Baseline default: *\**  
  
### HTTP authentication

- **Allow Basic authentication for HTTP**  
  Baseline default: *Disabled*

- **Supported authentication schemes**  
  Baseline default: *Enabled*  
  [Learn more](/deployedge/microsoft-edge-policies#authschemes)

### Native Messaging

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*

### Private Network Request Settings

- **Specifies whether to allow insecure websites to make requests to more-private network endpoints**  
  Baseline default: *Disabled*

### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

- **Configure Edge TyposquattingChecker**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="edge-v112"

## Microsoft Edge baseline for version 112 (May 2023) 

For information about the most recent baseline versions and settings from Microsoft, including versions of this baseline that might not be available through Intune, download the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center.

- **Allow unconfigured sites to be reloaded in Internet Explorer mode**  
  Baseline default: *Disabled*
  
- **Allow users to proceed from the HTTPS warning page**  
  Baseline default: *Disabled*

- **Enable browser legacy extension point blocking**  
  Baseline default: *Enabled*

- **Enable site isolation for every site**  
  Baseline default: *Enabled*

- **Enhance images enabled**  
  Baseline default: *Disabled*

- **Force WebSQL to be enabled**  
  Baseline default: *Disabled*

- **Minimum TLS version enabled**  
  Baseline default: *Enabled*

  - **Minimum SSL version enabled (Device)**  
    Baseline default: *TLS 1.2*  

- **Show the Reload in Internet Explorer mode button in the toolbar**  
  Baseline default: *Disabled*

- **Specifies whether SharedArrayBuffers can be used in a non cross-origin-isolated context**  
  Baseline default: *Disabled*

### Extensions 

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*

  - **Extension IDs the user should be prevented from installing (or * for all) (Device)**  
    Baseline default: *\**  
  
### HTTP authentication

- **Allow Basic authentication for HTTP**  
  Baseline default: *Disabled*

- **Supported authentication schemes**  
  Baseline default: *Enabled*  
  [Learn more](/deployedge/microsoft-edge-policies#authschemes)

- **Supported authentication schemes (Device)**  
    Baseline default: *ntlm,negotiate*  

### Native Messaging

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*

### Password manager and protection

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

### Private Network Request Settings

- **Specifies whether to allow insecure websites to make requests to more-private network endpoints**  
  Baseline default: *Disabled*

### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

::: zone-end

- [Learn about security baselines](../protect/security-baselines.md)
- [Avoid conflicts](../protect/security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
