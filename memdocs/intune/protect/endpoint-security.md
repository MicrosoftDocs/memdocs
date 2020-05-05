---
# required metadata

title: Manage endpoint security in Microsoft Intune | Microsoft Docs
description: Learn how Security Administrators can use the Endpoint Security node to manage device security and remediate issues for devices in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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

# Manage endpoint security in Microsoft Intune

As a Security Admin, use the *Endpoint security* node in Intune to configure device security and to manage security tasks for devices when those devices are at risk. The Endpoint security policies are designed to help you focus on the security of your devices and mitigate risk. The tasks that are available help you identify devices that are at risk, to remediate those devices, and restore them to a compliant or more secure state.

The Endpoint security node groups the tools that are available through Intune that you’ll use to keep devices secure:

- **Review the status of all your managed devices**. Use the [All devices](#manage-devices) view where you can view device compliance from a high level and then drill into specific devices to understand which compliance policies weren't met so you can resolve them.

- **Deploy security baselines that establish best practice security configurations for devices**. Intune includes [security baselines](#manage-security-baselines) for Windows devices and a growing list of applications, like Defender ATP and Microsoft Edge.

- **Manage security configurations on devices through tightly focused policies**.  Each [Endpoint security policy](#use-policies-to-manage-device-security) focuses on specific aspects of device security like antivirus, disk encryption, firewalls, and several areas made available through integration with Defender ATP.

- **Establish device and user requirements through compliance policy**. With [compliance policies](../protect/device-compliance-get-started.md), you set the rules that devices and users must meet to be considered compliant. Rules can include OS versions, password requirements, device threat-levels, and more. When you integrate with Azure AD [conditional access policies](#configure-conditional-access) to enforce compliance policies, you can gate access to corporate resources for both managed devices, and devices that aren’t managed yet.

- **Integrate Intune with your Microsoft Defender Advanced Threat Protection (Defender ATP) team**. By [integrating with Defender ATP](#set-up-integration-with-defender-atp) you gain access to [security tasks](#review-security-tasks-from-defender-atp) that closely tie Defender ATP and Intune together to help identify and remediate devices that are at risk.

The following sections of this article discuss the different tasks you can do from the endpoint security node of the admin center, and the role-based access control (RBAC) permissions required to use them.

## Manage devices

The Endpoint security node includes the *All devices* view, which you can use to view a list of all devices from your Azure Active Directory (Azure AD) that are available in Microsoft Endpoint Manager.

From this view you can select devices to drill in for more information like which policies a device isn't compliant with. You can also use access from this view to remediate issues for a device, including, restarting a device, start a scan for malware, or rotate BitLocker keys on a Window 10 device. .

For more information, see [Manage devices with endpoint security in Microsoft Intune](../protect/endpoint-security-manage-devices.md)

## Manage Security baselines

Security baselines in Intune are pre-configured groups of settings that are best practice recommendations from the relevant Microsoft security teams for the applicable product. Intune supports security baselines for Windows 10 device settings, Microsoft Edge, Microsoft Defender Advanced Threat Protection, and more.

You can use security baselines to rapidly deploy a *best practice* configuration of device and application settings to protect your users and devices. Security baselines are supported for devices that run Windows 10 version 1809 and later.

For more information, see [Use security baselines to configure Windows 10 devices in Intune](../protect/security-baselines.md)

## Review Security tasks from Defender ATP

When you integrate Intune with Microsoft Defender Advanced Threat Protection (Defender ATP), you can review *Security tasks* in Intune that identify at-risk devices and provide steps to mitigate that risk. You can then use the tasks to report back to Defender ATP when those risks are successfully mitigated.

- Your Defender ATP team determine what devices are at risk and pass that information to your Intune team as a security task. With one click they create a security task for Intune that identifies the devices at risk, the vulnerability, and that provides guidance on how to mitigate that risk.

- The Intune Admins review security tasks and then act within Intune to remediate those tasks. Once mitigated, they set the task to complete, which communicates that status back to the Defender ATP team.

Through Security tasks both teams remain in synch as to which devices are at risk, and how and when those risks are remediated.

To learn more about using Security tasks, see [Use Intune to remediate vulnerabilities identified by Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## Use policies to manage device security

As a security admin, use the security policies found under *Manage* in the Endpoint security node to configure device security without the overhead of navigating the larger body and range of settings found in device configuration profiles and security baselines.

Included under *Manage* is access to *Device compliance* and *Conditional access* policies. These policies are important tools for managing devices and access to your corporate resources.

![Manage policies](./media/endpoint-security/endpoint-security-policies.png)

To start using security policies, see [Manage device security with endpoint security polices](../protect/endpoint-security-policy.md).

### About policy conflicts

Many of the settings you can configure in the policies for Endpoint security are settings that can also be managed through *endpoint protection* profiles in device configuration policy, and by security baselines. Therefore, it's important to understand how to identify and resolve policy conflicts should a device not adhere to the configurations you expect.

The information at the following links can help you identify and resolve conflicts:

- [Troubleshoot policies and profiles in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitor your security baselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

The following sections introduce the policy groups and the profiles available for each group.

## Use device compliance policy

Use device compliance policy to establish the conditions by which devices and users are allowed to access your network and company resources.

The [available compliance settings](../protect/device-compliance-get-started.md#next-steps) depend on the platform you use, but common policy rules include:

- Requiring devices run a minimum or specific OS version
- Setting password requirements
- Specifying a maximum allowed device threat-level, as determined by Defender ATP or another Mobile Threat Defense partner
- Use of network locations

In addition to setting conditions for compliance, you can configure automatic actions to take when a device isn't compliant. Actions include sending email or notifications to alert device users about non-compliance, remotely locking devices, or even retiring non-compliant devices and removing any company data that might be on it.

When you integrate Intune with Azure AD [conditional access policies](#configure-conditional-access) to enforce compliance policies, Conditional access can use the compliance data to gate access to corporate resources for both managed devices, and devices that aren’t managed yet.

To learn more, see [Set rules on devices to allow access to resources in your organization using Intune](../protect/device-compliance-get-started.md).

## Configure conditional access

To protect your devices and corporate resources, you can use Azure Active Directory (Azure AD) Conditional Access policies with Intune.

Intune passes the results of your device compliance policies to Azure AD, which then uses conditional access policies enforce which devices and apps can access your corporate resources. Conditional access policies can help gate access for devices that aren’t managed by Intune. You can even use compliance details from [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) you integrate with Intune.

The following are two common methods of using conditional access with Intune include:

- Device-based Conditional Access
- App-based conditional access

When you select *Conditional Access* from within the Microsoft Endpoint Manager admin center, the Conditional Access node that opens in the admin center is the node from Azure AD. Your conditional access policies are created in Azure AD.

To learn more about using conditional access with Intune, see [Learn about Conditional Access and Intune](../protect/conditional-access.md).

## Set up Integration with Defender ATP

When you integrate Microsoft Defender Advanced Threat Protection (Defender ATP) with Intune, you improve your ability to identify and respond to risks.

While Intune can integrate with several [Mobile Threat Defense partners](../protect/mobile-threat-defense.md), when you use Defender ATP you gain a tight integration between Defender ATP and Intune with access to deep device protection options, including:

- Security tasks – Seamless communication between ATP and Intune admins about devices at risk, how to remediate them, and confirmation when those risks are mitigated.
- Streamlined onboarding for *Endpoint detection and response* on clients
- Use of ATP device risk signals in Intune compliance policies
- Access to *Tamper protection* capabilities

 To learn more about using Defender ATP with Intune, see [Enforce compliance for Microsoft Defender ATP with Conditional Access in Intune](../protect/advanced-threat-protection.md)

## Role-based access control requirements

To manage tasks in the Endpoint security node of the Microsoft Endpoint Manager admin center, an account must:

1. Be assigned a licence for Intune.
2. Have role-based access control (RBAC) permissions equal to those provided by the built-in Intune role of  **Endpoint Security Manager**. The *Endpoint Security Manager* role grants access to the Microsoft Endpoint Manager admin center and is intended for those who manage security and compliance features, including security baselines, device compliance, conditional access, and Microsoft Defender ATP.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)

### Permissions granted by the *Endpoint Security Manager* role

You can view the following list of permissions in the Microsoft Endpoint Manager admin center by going to **Tenant administration** > **Roles** > **All Roles**, select **Endpoint Security Manager** > **Properties**.

**Permissions:**

- **Android for work**
  - Read
- **Audit data**
  - Read
- **Corporate device identifiers**
  - Read
- **Device compliance policies**
  - Assign
  - Create
  - Delete
  - Read
  - Update
  - View reports
- **Device configurations**
  - Read
- **Device enrollment managers**
  - Read
- **Endpoint protection reports**
  - Read
- **Enrollment programs**
  - Read device
  - Read profile
  - Read token
- **Intune data warehouse**
  - Read
- **Managed apps**
  - Read
- **Managed devices**
  - Delete
  - Read
  - Set primary user
  - Update
- **Mobile apps**
  - Read
- **Organization**
  - Read
- **PolicySets**
  - Read
- **Remote assistance**
  - Read
- **Remote tasks**
  - Get FileVault key.
- **Roles**
  - Read
- **Security baselines**
  - Assign
  - Create
  - Delete
  - Read
  - Update
- **Security tasks**
  - Read
  - Update
- **Telecom expenses**
  - Read
- **Terms and conditions**
  - Read

## Next steps

Configure:

- [Security baselines](../protect/security-baselines.md)
- [Compliance policies](../protect/device-compliance-get-started.md)
- [Conditional access policies](#configure-conditional-access)
- [Integration with Defender ATP](../protect/advanced-threat-protection.md)
