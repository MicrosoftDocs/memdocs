---
# required metadata

title: Use Microsoft Defender for Endpoint in Microsoft Intune
description: Use Microsoft Defender for Endpoint with Intune, including setup and configuration, onboarding of your Intune devices, and then use a devices Defender for Endpoint risk assessment with your Intune device compliance and conditional access policies to protect network resources.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 11/09/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---


# Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune

You can integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense solution. Integration can help you prevent security breaches and limit the impact of breaches within an organization.

Microsoft Defender for Endpoint works with devices that run:

- Android
- iOS/iPadOS
- Windows 10
- Windows 11
- macOS
- Windows Server 2008 R2
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server Semi-Annual Enterprise Channel
- Windows Server 2019 and later
- Windows Server 2019 Core edition
- Windows Server 2022

To be successful, you'll use the following configurations in concert:

- **Establish a service-to-service connection between Intune and Microsoft Defender for Endpoint**. This connection lets Microsoft Defender for Endpoint collect data about machine risk from supported devices you manage with Intune.
- **Use a device configuration profile to onboard devices with Microsoft Defender for Endpoint**. You onboard devices to configure them to communicate with Microsoft Defender for Endpoint and to provide data that helps assess their risk level.
- **Use a device compliance policy to set the level of risk you want to allow**. Risk levels are reported by Microsoft Defender for Endpoint. Devices that exceed the allowed risk level are identified as noncompliant.
- **Use a conditional access policy** to block users from accessing corporate resources from devices that are noncompliant.

When you integrate Intune with Microsoft Defender for Endpoint, you can take advantage of Microsoft Defender for Endpoints Threat & Vulnerability Management (TVM) and [use Intune to remediate endpoint weakness identified by TVM](atp-manage-vulnerabilities.md).

## Example of using Microsoft Defender for Endpoint with Intune

The following example helps explain how these solutions work together to help protect your organization. For this example, Microsoft Defender for Endpoint and Intune are already integrated.

Consider an event where someone sends a Word attachment with embedded malicious code to a user within your organization.

- The user opens the attachment, and enables the content.
- An elevated privilege attack starts, and an attacker from a remote machine has admin rights to the victim's device.
- The attacker then remotely accesses the user's other devices. This security breach can impact the entire organization.

Microsoft Defender for Endpoint can help resolve security events like this scenario.

- In our example, Microsoft Defender for Endpoint detects that the device executed abnormal code, experienced a process privilege escalation, injected malicious code, and issued a suspicious remote shell.
- Based on these actions from the device, Microsoft Defender for Endpoint [classifies the device as high-risk](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) and includes a detailed report of suspicious activity in the Microsoft Defender Security Center portal.

You can integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense solution. Integration can help you prevent security breaches and limit the impact of breaches within an organization.

Because you have an Intune device compliance policy to classify devices with a *Medium* or *High* level of risk as noncompliant, the compromised device is classified as noncompliant. This classification allows your conditional access policy to kick in and block access from that device to your corporate resources.

For devices that run Android, you can use Intune policy to modify the configuration of Microsoft Defender for Endpoint on Android. For more information, see [Microsoft Defender for Endpoint web protection](../protect/advanced-threat-protection-manage-android.md).

## Prerequisites

**Subscriptions**:  
To use Microsoft Defender for Endpoint with Intune, you must have the following subscriptions:

- **Microsoft Defender for Endpoint** - This subscription provides you access to the Microsoft Defender Security Center (ATP portal).  

  For Defender for Endpoint licensing options, see **Licensing requirements** in [Minimum requirements for Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements) and [How to set up a Microsoft 365 E5 Trial Subscription](/microsoft-365/security/defender/setup-m365deval#enable-microsoft-365-trial-subscription).

- **Microsoft Intune** – A *Microsoft Intune Plan 1* subscription provides access to Intune and the Microsoft Intune admin center.

  For Intune licensing options, see [Microsoft Intune licensing](../fundamentals/licenses.md).

**Devices managed with Intune**:  
The following platforms are supported for Intune with Microsoft Defender for Endpoint:

- Android
- iOS/iPadOS
- Windows 10/11 (Hybrid Azure Active Directory Joined or Azure Active Directory Joined)

For the system requirements for Microsoft Defender for Endpoint, see [Minimum requirements for Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/minimum-requirements).

## Next steps

- To connect Microsoft Defender for Endpoint to Intune, onboard devices, and configure conditional access policies, see [Configure Microsoft Defender for Endpoint in Intune](../protect/advanced-threat-protection-configure.md).

Learn more from the Intune documentation:

- [Use security tasks with Defender for Endpoints Vulnerability Management to remediate issues on devices](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)

Learn more from the Microsoft Defender for Endpoint documentation:

- [Microsoft Defender for Endpoint Conditional Access](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender for Endpoint risk dashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
