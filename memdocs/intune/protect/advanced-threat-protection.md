---
# required metadata

title: Use Microsoft Defender for Endpoint in Microsoft Intune - Azure | Microsoft Docs
description: Use Microsoft Defender for Endpoint (formerly Microsoft Defender ATP) with Intune, including setup and configuration, onboarding of your Intune devices, and then use a devices Defender for Endpoint risk assessment with your Intune device compliance and conditional access policies to protect network resources.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 10/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---


# Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune

You can integrate Microsoft Defender for Endpoint (formerly Microsoft Defender ATP) with Microsoft Intune as a Mobile Threat Defense solution. Integration can help you prevent security breaches and limit the impact of breaches within an organization.

Microsoft Defender for Endpoint works with devices that run:
- Android
- iOS/iPadOS
- Windows 10 or later

To be successful, you'll use the following configurations in concert:

- **Establish a service-to-service connection between Intune and Microsoft Defender ATP**. This connection lets Microsoft Defender ATP collect data about machine risk from supported devices you manage with Intune.
- **Use a device configuration profile to onboard devices with Microsoft Defender ATP**. You onboard devices to configure them to communicate with Microsoft Defender ATP and to provide data that helps assess their risk level.
- **Use a device compliance policy to set the level of risk you want to allow**. Risk levels are reported by Microsoft Defender ATP. Devices that exceed the allowed risk level are identified as noncompliant.
- **Use a conditional access policy** to block users from accessing corporate resources from devices that are noncompliant.

When you integrate Intune with Microsoft Defender ATP, you can take advantage of Microsoft Defender ATPs Threat & Vulnerability Management (TVM) and [use Intune to remediate endpoint weakness identified by TVM](atp-manage-vulnerabilities.md).

## Example of using Microsoft Defender ATP with Intune

The following example helps explain how these solutions work together to help protect your organization. For this example, Microsoft Defender ATP and Intune are already integrated.

Consider an event where someone sends a Word attachment with embedded malicious code to a user within your organization.

- The user opens the attachment, and enables the content.
- An elevated privilege attack starts, and an attacker from a remote machine has admin rights to the victim's device.
- The attacker then remotely accesses the user's other devices. This security breach can impact the entire organization.

Microsoft Defender ATP can help resolve security events like this scenario.

- In our example, Microsoft Defender ATP detects that the device executed abnormal code, experienced a process privilege escalation, injected malicious code, and issued a suspicious remote shell.
- Based on these actions from the device, Microsoft Defender ATP [classifies the device as high-risk](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) and includes a detailed report of suspicious activity in the Microsoft Defender Security Center portal.

You can integrate Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) with Microsoft Intune as a Mobile Threat Defense solution. Integration can help you prevent security breaches and limit the impact of breaches within an organization.

Because you have an Intune device compliance policy to classify devices with a *Medium* or *High* level of risk as noncompliant, the compromised device is classified as noncompliant. This classification allows your conditional access policy to kick in and block access from that device to your corporate resources.

For devices that run Android, you can use Intune policy to modify the configuration of Microsoft Defender ATP on Android. For more information, see [Microsoft Defender ATP web protection](../protect/advanced-threat-protection-manage-android.md).

## Prerequisites

To use Microsoft Defender ATP with Intune, be sure you have the following configured, and ready for use:

- Licensed tenant for Enterprise Mobility + Security E3 and Windows E5 (or Microsoft 365 Business Premium)
- Microsoft Intune environment, with [Intune managed](../enrollment/windows-enroll.md) devices that are Azure AD joined and run:
  - Android
  - iOS/iPadOS
  - Windows 10
- [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) environment which will give you access to the Microsoft Defender Security Center (ATP portal)

> [!NOTE]
> Microsoft Defender ATP is not supported with Intune app protection policies.

## Next steps

- To connect Microsoft Defender ATP to Intune, onboard devices, and configure conditional access policies, see [Configure Microsoft Defender ATP in Intune](../protect/advanced-threat-protection-configure.md).

Learn more from the Intune documentation:

- [Use security tasks with ATPs Vulnerability Management to remediate issues on devices](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)

Learn more from the Microsoft Defender ATP documentation:

- [Microsoft Defender ATP Conditional Access](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP risk dashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)