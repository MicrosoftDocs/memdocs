---
title: Scenarios for using Conditional Access with Microsoft Intune
description: Learn how Conditional Access is commonly used with Intune compliance policy for devices and apps
ms.date: 03/19/2025
ms.topic: article
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- conditional-access
- sub-device-compliance
---

# Common ways to use Conditional Access with Intune

There are two types of Conditional Access policies you can use with Intune: device-based and app-based. This article covers common scenarios for both types.

The information in this article can help you understand how to use both the Intune mobile device compliance capabilities and the Intune mobile application management (MAM) capabilities.  

> [!NOTE]
> Conditional Access is a Microsoft Entra capability that is included with a Microsoft Entra ID P1 or P2 license. The Conditional Access node accessed from the Microsoft Intune admin center is the same node as accessed from Microsoft Entra ID.

## Applications available in Conditional Access for controlling Microsoft Intune

When you configure Conditional Access in the Microsoft Entra admin center, you have two applications to choose from:

- **Microsoft Intune** - This application controls access to the Microsoft Intune admin center and data sources. Configure grants/controls on this application when you want to target the Microsoft Intune admin center and data sources.
- **Microsoft Intune Enrollment** - This application controls the enrollment workflow. Configure grants/controls on this application when you want to target the enrollment process. For more information, see [Require multifactor authentication for Intune device enrollments](../../device-enrollment/configure-multifactor-authentication.md).

## Device-based Conditional Access

Intune and Microsoft Entra ID work together to make sure only managed and compliant devices can access your organization's email, Microsoft 365 services, software as a service (SaaS) apps, and [on-premises apps](/entra/identity/app-proxy). Additionally, you can set a policy in Microsoft Entra ID to only enable domain-joined computers or mobile devices that are enrolled in Intune to access Microsoft 365 services.

With Intune, you deploy device compliance policies to determine if a device meets your expected configuration and security requirements. The compliance policy evaluation determines the device's compliance status, which is reported to both Intune and Microsoft Entra ID. It's in Microsoft Entra ID that Conditional Access policies can use a device's compliance status to make decisions on whether to allow or block access to your organization's resources from that device.

Device-based Conditional Access policies for Exchange online and other Microsoft 365 products are configured through the [Microsoft Intune admin center](../../fundamentals/what-is-intune.md).

- Learn more about [Require managed devices with Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/policy-all-users-device-compliance).

- Learn more about [Intune device compliance](../compliance/overview.md).

- Learn more about [Supported browsers with Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/concept-conditional-access-conditions#supported-browsers).

The following scenarios build on device-based Conditional Access to show how it applies in specific contexts.

### Conditional Access based on network access control

Intune integrates with partners like Cisco ISE, Aruba Clear Pass, and Citrix NetScaler to provide access controls based on the Intune enrollment and the device compliance state.

Users can be allowed or denied access to corporate Wi-Fi or VPN resources based on whether the device they're using is managed and compliant with Intune device compliance policies.

- Learn more about the [NAC integration with Intune](../integrate-network-access-control.md).

### Conditional Access based on device risk

Intune partners with mobile threat defense vendors that provide a security solution to detect malware, Trojans, and other threats on mobile devices. When mobile devices have the mobile threat defense agent installed, the agent sends compliance state messages back to Intune reporting when a threat is found. This integration plays a factor in Conditional Access decisions based on device risk.

- Learn more about [Intune mobile threat defense](../mobile-threat-defense/overview.md).

### Conditional Access for Windows PCs

Conditional Access for PCs provides capabilities similar to those available for mobile devices. The following options are available when managing PCs with Intune.

#### Corporate-owned

- **Microsoft Entra hybrid joined:** This option is commonly used by organizations that are reasonably comfortable with how they're already managing their PCs through AD group policies or Configuration Manager.

- **Microsoft Entra domain joined and Intune management:** This scenario is for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure). Microsoft Entra join works well in a hybrid environment, enabling access to both cloud and on-premises apps and resources. The device joins to the Microsoft Entra ID and gets enrolled to Intune, which can be used as a Conditional Access criteria when accessing corporate resources.

#### Bring your own device (BYOD)

- **Workplace join and Intune management:** Here the user can join their personal devices to access corporate resources and services. You can use Workplace join and enroll devices into Intune MDM to receive device-level policies, which are another option to evaluate Conditional Access criteria.

Learn more about [Device Management in Microsoft Entra ID](/entra/identity/devices/overview).

## App-based Conditional Access

App-based Conditional Access protects access at the app level rather than the device level, making it well-suited for unenrolled devices. The following articles cover app-based Conditional Access scenarios for Intune:

- [Use app-based Conditional Access policies with Intune](./app-based-policies.md)
- [Require approved app or app protection policy (Microsoft Entra)](/entra/identity/conditional-access/policy-all-users-approved-app-or-app-protection)

## Next steps

[How to configure Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/concept-conditional-access-policy-common)

[Set up device-based Conditional Access policies](./device-based-policies.md)

[Set up app-based Conditional Access policies](./app-based-policies.md)
