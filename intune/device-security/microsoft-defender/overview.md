---
title: Integrate Microsoft Defender for Endpoint with Intune for Device Compliance
description: Integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense (MTD) solution to enforce device compliance and prevent security breaches.
author: brenduns
ms.author: brenduns
ms.date: 03/24/2026
ms.topic: article
ms.reviewer: aanavath
ai-usage: ai-assisted

ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
---

# Integrate Microsoft Defender for Endpoint with Intune for Device Compliance

Integrating Microsoft Defender for Endpoint with Microsoft Intune lets you assess device risk in real time and block compromised devices from corporate resources by automatically marking them as noncompliant.

For example, if malware compromises a user's device, Microsoft Defender for Endpoint flags that device as high-risk and Intune can automatically cut off its access to corporate resources.

This article explains how the integration works, what capabilities it enables for device compliance, and when to use each option. For step-by-step configuration, see [Configure Microsoft Defender for Endpoint in Intune](./configure-integration.md).

## Integration workflow

At a high level, the integration for devices enrolled with Intune works as follows. For detailed instructions, see [Configure Microsoft Defender for Endpoint in Intune](./configure-integration.md):

1. [Establish a service-to-service connection](./configure-integration.md#connect-microsoft-defender-for-endpoint-to-intune) between Intune and Microsoft Defender for Endpoint.
2. [Onboard devices](./configure-integration.md#onboard-devices) with Microsoft Defender for Endpoint using Intune policy.
3. [Create a device compliance policy](./configure-integration.md#create-and-assign-compliance-policy-to-set-device-risk-level) to set acceptable risk levels.
4. [Configure Conditional Access policy](./configure-integration.md#create-a-conditional-access-policy) to block noncompliant devices.

**Extend the integration:** Once configured, you can [use Microsoft Defender Vulnerability Management](./remediate-vulnerabilities.md) to remediate endpoint weaknesses identified by Defender.

## Additional integration options

The following options extend the integration beyond traditional device compliance and may be useful in mixed enrollment or unenrolled environments.

**App protection policies**: You can use [app protection policies](./configure-integration.md#create-and-assign-app-protection-policy-to-set-device-risk-level) to set device risk levels for both enrolled and unenrolled devices. This provides app-level protection based on Defender threat assessments.

**Unenrolled devices**: For devices that aren't or can't enroll in Intune, use Intune's [security management for Microsoft Defender for Endpoint](./security-settings-management.md) to manage Defender settings via endpoint security policies without requiring full device enrollment.

## Prerequisites

### Role-based access control

To configure this integration end-to-end, you need permissions to manage the Intune–Defender connection, device onboarding, and compliance policies. Specifically, your Intune role-based access control (RBAC) role must include:

- **Mobile Threat Defense**: *Modify* and *Read* – Required to establish the service-to-service connection between Intune and Defender.
- **Endpoint Detection and Response**: *Assign*, *Create*, *Read*, and *Update* – Required to onboard devices using Intune EDR policy.
- **Device compliance policies**: *Assign*, *Create*, *Read*, and *Update* – Required to configure risk-level compliance policies.

You can add these permissions to a [custom Intune role](../../intune-service/fundamentals/create-custom-role.md), or use the built-in **Endpoint Security Manager** role, which is the least-privileged built-in Intune role that includes all required permissions. For details, see [Role-based access control for Microsoft Intune](../../intune-service/fundamentals/role-based-access-control.md).

> [!NOTE]
> Conditional Access policies are configured in Microsoft Entra ID and require a separate Entra ID role, such as [Conditional Access Administrator](../../intune-service/protect/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).

### Intune requirements

**Subscription**: Microsoft Intune Plan 1 subscription provides access to Intune and the Microsoft Intune admin center.

For licensing options, see [Microsoft Intune licensing](../../fundamentals/licensing/index.md).

**Supported platforms**:

| Platform | Requirements |
|----------|--------------|
| Android  | Intune-managed devices |
| iOS/iPadOS | Intune-managed devices |
| Windows  | Microsoft Entra ID hybrid joined or Microsoft Entra ID joined |

### Microsoft Defender for Endpoint requirements

**Subscription**: Microsoft Defender for Endpoint subscription provides access to the [Microsoft Defender XDR portal](https://go.microsoft.com/fwlink/p/?linkid=2077139).

For licensing and system requirements, see [Minimum requirements for Microsoft Defender for Endpoint](../../intune-service/protect/defender-endpoint/minimum-requirements).

## Example: Automatic threat containment

The following example shows how the integration automatically contains a threat, assuming it's already configured:

1. **Detection**: Microsoft Defender for Endpoint detects threat activity on a device and classifies it as high-risk.
2. **Compliance enforcement**: Intune receives the risk signal and automatically marks the device as noncompliant based on your compliance policy thresholds.
3. **Access blocking**: Conditional Access policies immediately block the noncompliant device from accessing corporate resources.
4. **Containment**: The threat is contained while your security team investigates and remediates in the Microsoft Defender XDR portal.

## Platform-specific capabilities

Different platforms offer unique configuration options when integrating with Microsoft Defender for Endpoint:

**Android**: Deploy Defender for Endpoint to Android devices through Managed Google Play using Intune app deployment and app configuration policies. See [Deploy Microsoft Defender for Endpoint on Android](./deploy-android.md) for the complete deployment guide. After deployment, use Intune device configuration policies to configure [Microsoft Defender for Endpoint web protection](./configure-web-protection-android.md) settings, including the ability to enable or disable VPN-based scanning.

**iOS/iPadOS**: Enable [vulnerability assessment of apps](../../intune-service/protect/defender-endpoint/ios-configure-features#configure-vulnerability-assessment-of-apps) to allow Defender to scan installed apps for known vulnerabilities.

**Windows**: Benefit from automatic onboarding capabilities and use [Microsoft Defender for Endpoint security baselines](../security-baselines/overview.md) for comprehensive, prescriptive security configurations.

## Next steps

### Configure the integration

[Configure Microsoft Defender for Endpoint in Intune](./configure-integration.md): complete step-by-step instructions for connecting Intune and Defender, onboarding devices, and setting up Conditional Access policies.

### Related content

**Intune resources**:

- [Get started with device compliance policies](../compliance/overview.md)

**Microsoft Defender for Endpoint resources**:

- [Microsoft Defender for Endpoint Conditional Access](../../intune-service/protect/defender-endpoint/conditional-access)
- [Microsoft Defender XDR portal](../../intune-service/protect/defender-xdr/microsoft-365-defender-portal)