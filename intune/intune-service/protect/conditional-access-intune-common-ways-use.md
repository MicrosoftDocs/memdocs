---
title: Scenarios for using Conditional Access with Microsoft Intune
description: Learn how Conditional Access is commonly used with Intune compliance policy for devices and apps
author: lenewsad
ms.author: lanewsad
ms.date: 03/19/2025
ms.topic: article
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- highpri
- conditional-access
- sub-device-compliance
---

# Common ways to use Conditional Access with Intune

There are two types of Conditional Access policies you can use with Intune: device-based Conditional Access and app-based Conditional Access. To support each, you need to configure the related Intune policies. When the Intune policies are in place and deployed, you can then use Conditional Access to do things like allow or block access to Exchange, control access to your network, or integrate with a Mobile Threat Defense solution.

The information in this article can help you understand how to use the Intune mobile *device* compliance capabilities and the Intune mobile *application* management (MAM) capabilities.

> [!NOTE]
> Conditional Access is a Microsoft Entra capability that is included with a Microsoft Entra ID P1 or P2 license. Intune enhances this capability by adding mobile device compliance and mobile app management to the solution. The Conditional Access node accessed from *Intune* is the same node as accessed from *Microsoft Entra ID*.

## Device-based Conditional Access

Intune and Microsoft Entra ID work together to make sure only managed and compliant devices can access your organization's email, Microsoft 365 services, Software as a service (SaaS) apps, and [on-premises apps](/entra/identity/app-proxy/). Additionally, you can set a policy in Microsoft Entra ID to only enable domain-joined computers or mobile devices that are enrolled in Intune to access Microsoft 365 services.

With Intune, you deploy device compliance policies to determine if a device meets your expected configuration and security requirements. The compliance policy evaluation determines the device's compliance status, which is reported to both Intune and Microsoft Entra ID. It's in Microsoft Entra ID that Conditional Access policies can use a device's compliance status to make decisions on whether to allow or block access to your organization's resources from that device.

Device-based Conditional Access policies for Exchange online and other Microsoft 365 products are configured through the [Microsoft Intune admin center](../fundamentals/what-is-intune.md).

- Learn more about [Require managed devices with Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/policy-all-users-device-compliance).

- Learn more about [Intune device compliance](device-compliance-get-started.md).

- Learn more about [Supported browsers with Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/concept-conditional-access-conditions#supported-browsers).

> [!NOTE]
> When you enable Device Based Access for content that users access from browser apps on their Android personally owned work profile devices, users that enrolled before January 2021 must enable browser access as follows:
>
> 1. Launch the **Company Portal** app.
> 2. Go to the **Settings** page from the menu.
> 3. In the **Enable Browser Access** section, tap the **ENABLE** button.
> 4. Close and then restart the browser app.
>
> This enables access in browser apps, but not to browser WebViews that open within apps.

## Applications available in Conditional Access for controlling Microsoft Intune

When you configure Conditional Access in the Microsoft Entra admin center, you have two applications to choose from:

1. **Microsoft Intune** - This application controls access to the Microsoft Intune admin center and data sources. Configure grants/controls on this application when you want to target the Microsoft Intune admin center and data sources.
2. **Microsoft Intune Enrollment** - This application controls the enrollment workflow. Configure grants/controls on this application when you want to target the enrollment process. For more information, see [Require multifactor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md).

## Conditional Access based on network access control

Intune integrates with partners like Cisco ISE, Aruba Clear Pass, and Citrix NetScaler to provide access controls based on the Intune enrollment and the device compliance state.

Users can be allowed or denied access to corporate Wi-Fi or VPN resources based on whether the device they're using is managed and compliant with Intune device compliance policies.

- Learn more about the [NAC integration with Intune](network-access-control-integrate.md).

## Conditional Access based on device risk

Intune partners with Mobile Threat Defense vendors that provide a security solution to detect malware, Trojans, and other threats on mobile devices.

### How the Intune and Mobile Threat Defense integration works

When mobile devices have the Mobile Threat Defense agent installed, the agent sends compliance state messages back to Intune reporting when a threat is found on the mobile device itself.

The Intune and mobile threat defense integration plays a factor in the Conditional Access decisions based on device risk.

- Learn more about [Intune mobile threat defense](mobile-threat-defense.md).

## Conditional Access for Windows PCs

Conditional Access for PCs provides capabilities similar to those available for mobile devices. Let's talk about the ways you can use Conditional Access when managing PCs with Intune.

### Corporate-owned

- **Microsoft Entra hybrid joined:** This option is commonly used by organizations that are reasonably comfortable with how they're already managing their PCs through AD group policies or Configuration Manager.

- **Microsoft Entra domain joined and Intune management:** This scenario is for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure). Microsoft Entra join works well in a hybrid environment, enabling access to both cloud and on-premises apps and resources. The device joins to the Microsoft Entra ID and gets enrolled to Intune, which can be used as a Conditional Access criteria when accessing corporate resources.

### Bring your own device (BYOD)

- **Workplace join and Intune management:** Here the user can join their personal devices to access corporate resources and services. You can use Workplace join and enroll devices into Intune MDM to receive device-level policies, which are another option to evaluate Conditional Access criteria.

Learn more about [Device Management in Microsoft Entra ID](/azure/active-directory/devices/overview).

## App-based Conditional Access

Intune and Microsoft Entra ID work together to make sure only managed apps can access corporate e-mail or other Microsoft 365 services. Learn more about [app-based Conditional Access with Intune](app-based-conditional-access-intune.md).



## Next steps

[How to configure Conditional Access in Microsoft Entra ID](/entra/identity/conditional-access/concept-conditional-access-policy-common)

[Set up app-based Conditional Access policies](app-based-conditional-access-intune-create.md)
