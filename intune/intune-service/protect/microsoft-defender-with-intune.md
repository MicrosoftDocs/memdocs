---
title: Use Microsoft Defender for Endpoint in Microsoft Intune
description: Integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense solution.
author: brenduns
ms.author: brenduns
ms.date: 08/28/2025
ms.topic: article
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
---


# Use Microsoft Defender for Endpoint to enforce device compliance with Microsoft Intune
When you integrate Microsoft Defender for Endpoint with Microsoft Intune you can use Intune to enforce device compliance, configure devices to help prevent security breaches, and limit the impact of threats from devices that run Defender for Endpoint.

To get started, implement the following configurations, which are detailed in depth in [Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md):

- **Establish a service-to-service connection between Intune and Microsoft Defender for Endpoint**. This connection lets Microsoft Defender for Endpoint collect data about machine risk from supported devices you manage with Intune. See [Connect Microsoft Defender for Endpoint to Intune](../protect/microsoft-defender-integrate.md#connect-microsoft-defender-for-endpoint-to-intune).

- **Use an Intune policy to onboard devices with Microsoft Defender for Endpoint**. You onboard devices to configure them to communicate with Microsoft Defender for Endpoint and to provide data that helps assess their risk level. See [Onboard devices](../protect/microsoft-defender-integrate.md#onboard-devices).

- **Use a device compliance policy to set the level of risk you want to allow**. Risk levels are reported by Microsoft Defender for Endpoint. Devices that exceed the allowed risk level are identified as noncompliant. See [Create and assign compliance policy to set device risk level](../protect/microsoft-defender-integrate.md#create-and-assign-compliance-policy-to-set-device-risk-level) and [Create and assign app protection policy to set device risk level](../protect/microsoft-defender-integrate.md#create-and-assign-app-protection-policy-to-set-device-risk-level).

- **Use a Conditional Access policy** to block users from accessing corporate resources from devices that are noncompliant. See [Create a Conditional Access policy](../protect/microsoft-defender-integrate.md#create-a-conditional-access-policy).

- Take advantage of Microsoft Defender for Endpoints Threat & Vulnerability Management (TVM) and [use Intune security tasks to remediate endpoint weakness identified by TVM](atp-manage-vulnerabilities.md).

- Use [Intune endpoint security policies to manage Microsoft Defender for Endpoint on devices that are not enrolled with Intune](mde-security-integration.md).

When you integrate Intune with Microsoft Defender for Endpoint, you can take advantage of Microsoft Defender for Endpoints Threat & Vulnerability Management (TVM) and [use Intune to remediate endpoint weakness identified by TVM](../protect/atp-manage-vulnerabilities.md).

## Prerequisites

### Intune

**Subscription**:
- **Microsoft Intune** – A *Microsoft Intune Plan 1* subscription provides access to Intune and the Microsoft Intune admin center.

  For Intune licensing options, see [Microsoft Intune licensing](../fundamentals/licenses.md).

**Devices managed with Intune**:
The following platforms are supported for Intune with Microsoft Defender for Endpoint:

- Android
- iOS/iPadOS
- Windows (Microsoft Entra hybrid joined or Microsoft Entra joined)

### Microsoft Defender

**Subscription**:

- **Microsoft Defender for Endpoint** - This subscription provides you access to the Microsoft [Defender Security Center](https://go.microsoft.com/fwlink/p/?linkid=2077139).

  For Defender for Endpoint licensing options, see **Licensing requirements** in [Minimum requirements for Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements) and [How to set up a Microsoft 365 E5 Trial Subscription](/microsoft-365/security/defender/setup-m365deval#enable-microsoft-365-trial-subscription).

  For the list of operating systems and versions supported by Defender for Endpoint, see the Microsoft Defender for Endpoint [requirements](/defender-endpoint/minimum-requirements#hardware-and-software-requirements).

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

Because you have an Intune device compliance policy to classify devices with a *Medium* or *High* level of risk as noncompliant, the compromised device is classified as noncompliant. This classification allows your Conditional Access policy to kick in and block access from that device to your corporate resources.

For devices that run Android, you can use Intune policy to modify the configuration of Microsoft Defender for Endpoint on Android. For more information, see [Microsoft Defender for Endpoint web protection](../protect/microsoft-defender-configure-android.md).

## Next steps

- To connect Microsoft Defender for Endpoint to Intune, onboard devices, and configure Conditional Access policies, see [Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md).

Learn more from the Intune documentation:

- [Use security tasks with Defender for Endpoints Vulnerability Management to remediate issues on devices](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)

Learn more from the Microsoft Defender for Endpoint documentation:

- [Microsoft Defender for Endpoint Conditional Access](/defender-endpoint/conditional-access)
- [Microsoft Defender portal](/defender-xdr/microsoft-365-defender-portal)