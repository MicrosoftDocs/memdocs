---
# required metadata

title: List of settings for the Microsoft 365 Apps for Enterprise security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Office apps. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/24/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
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

---

<!-- Add when pivots are needed:
 
Metadata:
zone_pivot_groups: dcv2-office-baselines

Pivot yml: 
- id: dcv2-office-baselines
  title: Microsoft 365 Apps for Enterprise baseline versions
  prompt: Choose a version
  pivots:
    - id: office-may2023
      title: May 2023
    - id: office-future
      title: Future version
-->
# Microsoft  365 Apps for Enterprise security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft 365 Apps for Enterprise security baseline for Microsoft Intune and applies to versions of that baseline that released in May 2023 or later.


## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

The details that are displayed in this article are based on baseline version that is selected at the top of the article. For each selection, this article displays:

- A list of each setting in that baseline version.
- The default configuration of each setting in that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation, or other related content from the relevant product group that provides context and possibly additional details for the settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:

- [Use security baselines](../protect/security-baselines.md)
- [Manage security baselines](../protect/security-baselines-configure.md).



## Microsoft 365 Apps for Enterprise

<!-- >::: zone pivot="office-may2023" -->

**Microsoft 365 Apps for Enterprise security baseline for May 2023**

- **Name**  
  Baseline default: *Disabled*  
  [Learn more]()
  
<!-- ::: zone-end  -->


## Next steps

- [Learn about security baselines](../protect/security-baselines.md)
- [Avoid conflicts](../protect/security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
