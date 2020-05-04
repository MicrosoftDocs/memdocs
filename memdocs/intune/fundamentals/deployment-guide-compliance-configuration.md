---
# required metadata

title: Deploy device compliance and configuration policies in Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Deployment guide: Create compliance policy and configure devices in Microsoft Intune

THIS GUIDE IS STILL BEING WRITTEN, AND MAY CONTAIN INCORRECT INFORMATION.

This deployment guide shows how to move from on-premises group policy objects (GPO) to Intune. It also gets you started with compliance policies and device configuration profiles.

In this guide, you create a baseline compliance policy that all devices must have. When combined with conditional access, you can allow and block access to your organization's resources, including email. Many organizations create and configure compliance policies as part of the initial enrollment in Intune.

This guide also 

high level as there's no magic Intune button to migrate

Device configuration profiles configure settings and features on the device. For example, you can block the device camera, configure Internet Explorer settings, deploy certificates, and configure a Wi-Fi connection.

For more information on the profiles you can configure, see [Apply features and settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).

## Prerequisites

- Intune is set up. Be sure:

  - The [MDM Authority](../fundamentals/mdm-authority-set.md) is set to Intune, even when using [co-management](https://docs.microsoft.com/configmgr/comanage/overview) with Intune + Configuration Manager.
  - [Intune licenses are assigned](../fundamentals/licenses-assign.md).

  For more information, see [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](../fundamentals/supported-devices-browsers.md), and enrolled in Intune. This requirement includes devices that are co-managed, or hybrid Azure Active Directory (Azure AD) joined devices.

- Sign in as a member of the **Policy and Profile Manager** or **Intune Role Administrator** Intune roles. Or, sign in as a member of the **Global Administrator** or **Intune Service Administrator** Azure AD roles. [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information.

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the profile to more pilot groups.

Using a staged approach, you can get feedback from a wide range of user types.

For more information and suggestions, see the [Planning guide: Task 5: Create a rollout plan](../fundamentals/intune-planning-guide.md#task-5-create-a-rollout-plan).

## On-premises group policy (GPO)

On-premises Active Directory (AD) group policies (GPOs) can't be used on Azure AD joined devices. To manage Azure AD joined devices, you must use an MDM solution, such as Intune. When moving devices from group policy, it's recommended to reset the devices, and enroll them in Intune. Once enrolled, they'll receive the policies and profiles you create. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

- If you use group policy to manage devices, and don't use Configuration Manager, then we recommend going to Microsoft Intune. There are some tools and Intune features that can help with this move. For more information, see [create a priority list](#create-a-priority-list) (in this article).

- If you use group policy to manage devices, and use Configuration Manager, then you have some options:
  - Use [co-management](https://docs.microsoft.com/mem/configmgr/comanage/overview) to cloud-attach your Configuration Manager investment to Intune. With this option, you use Configuration Manager (on-premises) for some workflows, and Intune (cloud) for other workflows. Co-managed devices are considered "enrolled" in Intune. They can benefit from cloud features, including compliance, conditional access, and device configuration.

    For more information, see [Intune setup deployment guide](deployment-guide-intune-setup.md).

  - Move to Intune. For more information, see [Intune setup deployment guide](deployment-guide-intune-setup.md).

## Create a priority list

Create a list of the policies and features your devices must have. If you use a third-party MDM, track what you want to bring to Intune. This list is your priority list. For more information on the settings and features you can configure in Intune, see:

- [Compliance policies in Intune](../protect/device-compliance-get-started.md)
- [Device configuration profiles in Intune](../configuration/device-profiles.md).

If you have existing policies, you'll probably need to recreate these policies in Intune. Remember, it's possible old policies don't apply anymore. Instead of looking at what you've always done, determine the goal. If you haven't reviewed your existing policies, and want some guidance, then see [Task 4: Review existing policies and infrastructure](intune-planning-guide.md#task-4-review-existing-policies-and-infrastructure).

The following tools and Intune features can help:

- Use the [MDM Migration Analysis Tool (MMAT)](https://github.com/WindowsDeviceManagement/MMAT) to get a list of group policies that target the user or device. MMAT also cross-references these policies against its built-in list of supported MDM policies.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), use **Group policy analytics** (**Devices** > **Group policy analytics**) to analyze your on-premises group policy objects (GPO). This feature shows the policy settings that Intune supports. If a policy setting isn't supported, then that policy may not apply in the cloud, may be outdated, or may not be exposed to MDM providers. Most platforms also support using a custom OMA-URI to add settings that aren't exposed by the operating systems.
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), use [ADMX templates](../configuration/administrative-templates-windows.md) to configure settings for Microsoft Office, Microsoft Edge version 77 and later, and Windows. You don't install anything, as the templates are automatically built in.

  If you currently use ADMX templates on-premises, then using [ADMX templates](../configuration/administrative-templates-windows.md) in Intune is a natural migration. Although the user interfaces (cloud vs. on-premises) are different, the setting names and values are the same.

## Create a compliance security baseline

1. Create [compliance policies](../protect/device-compliance-get-started.md) that focus on security. This initial set of policies is your baseline or minimum set of security rules that all devices must have. In [create a priority list](#create-a-priority-list) (in this article), you created a list of policies devices must have. To get started, use this list. Also consider:

    - In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), use [Security Baselines](../protect/security-baselines.md). These security settings are pre-configured by security experts at Microsoft. You create a template, and assign the template to your groups. You can also change any setting to a different value, if you want.

      If you're brand new to the cloud, or want automatically configured Microsoft-recommended security settings, then [Security Baselines](../protect/security-baselines.md) is your answer.

    - Use resource access profiles (Wi-Fi, VPN, and email certificates). Resource access profiles supply certificates and access configurations to enrolled devices. If you're using certificate-based authentication, then [configure certificates](../protect/certificates-configure.md).

    - When you create your policies, look for patterns. There may be settings that apply to only Windows devices, or only Android devices, or settings that apply to all platforms. The following list includes the most commonly configured compliance settings for each platform:

      **Android/Android Enterprise**

      - Block rooted devices
      - Require a password
      - Set a minimum password length
      - Set the required password type
      - Set the maximum minutes of inactivity until screen locks

      **macOS**

      - Require a password
      - Require storage encryption
      - Set a minimum password length
      - Require system integrity protection
      - Block simple passwords

      **iOS/iPadOS**

      - Block jailbroken devices
      - Require a passcode
      - Set a minimum passcode length
      - Set the maximum minutes of inactivity until screen locks
      - Block simple passwords

      **Windows 10 and newer**

      - Require antivirus
      - Require BitLocker
      - Require a firewall
      - Require anti-spyware
      - Require a password

2. If you're using [conditional access](../protect/conditional-access.md), then configure it to enforce your baseline compliance settings. Block access for users and devices that aren't compliant with your compliance policies. For example, if there are iOS/iPadOS devices that are jailbroken, then block access to all organization apps, such as SharePoint, Teams, and email. If Windows 10 devices exceed a threat level you set, then block access to all organization resources, including VPN and your organization Wi-Fi.

    - If you're not using conditional access, Intune shows the devices that aren't compliant. Use this information so you know and are aware of these devices in your organization. When you use compliance policies without conditional access, there aren't any access restrictions to organization resources. What happens next with these devices, is up to you.

    - Before conditional access blocks access, many organizations give users 3 days to get compliant. This timeframe depends on the security implications in your organization. If you access government, personally identifiable information (PII), or highly sensitive data, you can shorten the timeframe to immediately. In other organizations, you may want to extend it.

## Add device features

1. Create [configuration profiles](../configuration/device-profiles.md) to configure, allow, and block features and settings on devices. The features you manage depend on what you want to achieve. For example, you can deploy authentication certificates, add a VPN connection, restrict apps, block the device camera, configure Windows Hello, add a Wi-Fi connection, and more. In [create a priority list](#create-a-priority-list) (in this article), you created a list of features devices must have. To get started, use this list.

    For more information on the profiles you can configure, see [Apply features and settings on your devices](../configuration/device-profiles.md).

    The following list includes the most commonly configured configuration settings for each platform:

    **Android/Android Enterprise**: Requested info from Chris Baldwin.


    **macOS**: Requested info from Anya and Katelynn.


    **iOS/iPadOS**: Requested info from Anya and Katelynn.


    **Windows 10 and newer**: Requested info from Mike Danoski.

2. Import iOS/iPadOS configuration profiles.

    - **Apple Configurator iOS profiles (iOS 7.1 and later)**: If your existing MDM solution uses Apple Configurator profiles (.mobileconfig files), then you can import them directly in Intune as custom configuration policies.

    - **iOS Mobile Application Configuration policies**: If your existing MDM solution uses iOS/iPadOS Mobile Application Configuration policies, then you can import them directly in Intune. The policies must meet the XML format specified by Apple for property lists.

    For more information, see [add a custom iOS/iPadOS policy](../configuration/custom-settings-ios.md).

## Use a third party or partner MDM

In this section, need info from CSS and PFE teams. I assume admins need to recreate the settings. Some questions to possibly answer:

- Do third-party MDMs have tools to export their policies?
- Are there common practices for third-party MDMs, such as AirWatch, MobileIron, or MaaS 360?
- Any other good info to share with customers, specific to compliance and device configuration?

## Move from Office 365

Need info from Office 365/M365, specifically:

- Office 365 subscription upgrade to M365
- I *think* O365 device management creates app protection or app configuration policies to protect/configure Outlook apps (email, SharePoint, Teams).
- Do these policies "carry over" to Intune? Or, do they need to be recreated within Intune?

## Assign and monitor

[Assign your policies and profiles](../configuration/device-profile-assign.md), and monitor your [compliance policies](../protect/compliance-policy-monitor.md) and [configuration profiles](../configuration/device-profile-monitor.md).

## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

[Common questions and answers](../configuration/device-profile-troubleshoot.md)

## Next steps

[Enrollment deployment guide](deployment-guide-enrollment.md)  
[Intune setup deployment guide](deployment-guide-intune-setup.md)  
App deployment guide
