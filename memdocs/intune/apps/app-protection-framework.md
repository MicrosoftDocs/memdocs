---
# required metadata

title: Data protection framework using app protection policies 
titleSuffix: Microsoft Intune
description: Learn how App Protection Policies (APP) ensure an organization's data remains safe or contained in a managed app, regardless of whether the device is enrolled. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/12/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- M365-identity-device-management
---

# Data protection framework using app protection policies 

As more organizations implement mobile device strategies for accessing work or school data, protecting against data leakage becomes paramount. Intune's mobile application management solution for protecting against data leakage is App Protection Policies (APP). APP are rules that ensure an organization's data remains safe or contained in a managed app, regardless of whether the device is enrolled. For more information, see [App protection policies overview](app-protection-policy.md).

When configuring App Protection Policies, the number of various settings and options enable organizations to tailor the protection to their specific needs. Due to this flexibility, it may not be obvious which permutation of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening endeavors, Microsoft has introduced a new taxonomy for [security configurations in Windows 10](https://aka.ms/secconframework), and Intune is leveraging a similar taxonomy for its APP data protection framework for mobile app management.  

The APP data protection configuration framework is organized into three distinct configuration scenarios:

- Level 1 enterprise basic data protection – Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

- Level 2 enterprise enhanced data protection – Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

- Level 3 enterprise high data protection – Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely high risk (users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

## APP Data Protection Framework deployment methodology

As with any deployment of new software, features or settings, Microsoft recommends investing in a ring methodology for testing validation prior to deploying the APP data protection framework. Defining deployment rings is generally a one-time event (or at least infrequent), but IT should revisit these groups to ensure that the sequencing is still correct.

Microsoft recommends the following deployment ring approach for the APP data protection framework:

| Deployment ring  | Tenant  | Assessment teams  | Output  | Timeline  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Quality Assurance  | Preproduction tenant  | Mobile capability owners, Security, Risk Assessment, Privacy, UX  | Functional scenario validation, draft documentation  | 0-30 days  |
| Preview  | Production tenant  | Mobile capability owners, UX  | End-user scenario validation, user facing documentation  | 7-14 days, post Quality Assurance  |
| Production  | Production tenant  | Mobile capability owners, IT help desk  | N/A  | 7 days to several weeks, post Preview  |

As the above table indicates, all changes to the App Protection Policies should be first performed in a preproduction environment to understand the policy setting implications. Once testing is complete, the changes can be moved into production and applied to a subset of production users, generally, the IT department and other applicable groups. And finally, the rollout can be completed to the rest of the mobile user community. Roll out to production may take a longer amount of time depending on the scale of impact regarding the change. If there's no user impact, the change should roll out quickly, whereas, if the change results in user impact, rollout may need to go slower due to the need to communicate changes to the user population.

When testing changes to an APP, be aware of the [delivery timing](app-protection-policy-delivery.md). The status of APP delivery for a given user can be monitored. For more information, see [How to monitor app protection policies](app-protection-policies-monitor.md).

Individual APP settings for each app can be validated on devices using Microsoft Edge and the URL *about:Intunehelp*. For more information, see [Review client app protection logs](app-protection-policy-settings-log.md) and [Use Microsoft Edge for iOS and Android to access managed app logs](manage-microsoft-edge.md#use-microsoft-edge-for-ios-and-android-to-access-managed-app-logs).

## APP Data Protection Framework settings

The following App Protection Policy settings should be enabled for the applicable apps and assigned to all mobile users. For more information on each policy setting, see [iOS app protection policy settings](app-protection-policy-settings-ios.md) and [Android app protection policy settings](app-protection-policy-settings-android.md).

Microsoft recommends reviewing and categorizing usage scenarios, and then configuring users using the prescriptive guidance for that level. As with any framework, settings within a corresponding level may need to be adjusted based on the needs of the organization as data protection must evaluate the threat environment, risk appetite, and impact to usability.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [Intune App Protection Policy Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

> [!NOTE]
> When using MAM for Windows, see [App protection policy settings for Windows](../apps/app-protection-policy-settings-windows.md).

### Conditional Access Policies

To ensure that only apps supporting App Protection Poliies access work or school account data, Microsoft Entra Conditional Access policies are required. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

 See **Require approved client apps or app protection policy with mobile devices** in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection) for steps to implement the specific policies. Finally, implement the steps in [Block legacy authentication](/azure/active-directory/conditional-access/block-legacy-authentication) to block legacy authentication capable iOS and Android apps.

> [!NOTE]
> These policies leverage the grant controls [Require approved client app](/azure/active-directory/conditional-access/concept-conditional-access-grant#require-approved-client-app) and [Require app protection policy](/azure/active-directory/conditional-access/concept-conditional-access-grant#require-app-protection-policy).

### Apps to include in the App Protection Policies  

For each App Protection Policy, the Core Microsoft Apps group is targeted, which includes the following apps:

- Microsoft Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- SharePoint
- Teams
- To Do
- Word

The policies should include other Microsoft apps based on business need, additional third-party public apps that have integrated the Intune SDK used within the organization, as well as line-of-business apps that have integrated the [Intune SDK](../developer/app-sdk.md) (or have been wrapped).

[!INCLUDE [app-protection-framework-level1](../includes/app-protection-framework-level1.md)]

[!INCLUDE [app-protection-framework-level2](../includes/app-protection-framework-level2.md)]

[!INCLUDE [app-protection-framework-level3](../includes/app-protection-framework-level3.md)]

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [Intune App Protection Policy Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## See also

- [How to create and deploy app protection policies with Microsoft Intune](app-protection-policies.md)
- [Available Android app protection policy settings with Microsoft Intune](app-protection-policy-settings-android.md)
- [Available iOS/iPadOS app protection policy settings with Microsoft Intune](app-protection-policy-settings-ios.md)
