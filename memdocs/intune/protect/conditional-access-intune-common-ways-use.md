---
# required metadata

title: Scenarios for using Conditional Access with Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn how Conditional Access is commonly used with Intune compliance policy for devices and apps
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/14/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; seodec18
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Common ways to use Conditional Access with Intune

There are two types of Conditional Access policies you can use with Intune: device-based Conditional Access and app-based Conditional Access. To support each, you'll need to configure the related Intune compliance policies. When the Intune policies are in place and deployed, you can then use Conditional Access to do things like allow or block access to Exchange, control access to your network, or integrate with a Mobile Threat Defense solution.

The information in this article can help you understand how to use the Intune mobile *device* compliance capabilities and the Intune mobile *application* management (MAM) capabilities.

> [!NOTE]
> Conditional Access is an Azure Active Directory (Azure AD) capability that is included with an Azure AD Premium license. Intune enhances this capability by adding mobile device compliance and mobile app management to the solution. The Conditional Access node accessed from *Intune* is the same node as accessed from *Azure AD*.  

## Device-based Conditional Access

Intune and Azure AD work together to make sure only managed and compliant devices can access your organization's email, Microsoft 365 services, Software as a service (SaaS) apps, and [on-premises apps](/azure/active-directory/active-directory-application-proxy-get-started). Additionally, you can set a policy in Azure AD to only enable domain-joined computers or mobile devices that are enrolled in Intune to access Microsoft 365 services.

With Intune, you deploy device compliance policies to determine if a device meets your expected configuration and security requirements. The compliance policy evaluation determines the devices compliance status, which is reported to both Intune and Azure AD. It's in Azure AD that Conditional Access policies can use a device's compliance status to make decisions on whether to allow or block access to your organization's resources from that device.

Device-based Conditional Access policies for Exchange online and other Microsoft 365 products are configured through the [Microsoft Endpoint Manager admin center](../fundamentals/what-is-intune.md).

- Learn more about [Require managed devices with Conditional Access in Azure Active Directory](/azure/active-directory/conditional-access/require-managed-devices).

- Learn more about [Intune device compliance](device-compliance-get-started.md).

- Learn more about [Supported browsers with Conditional Access in Azure Active Directory](/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> When you enable Device Based Access for content that users access from browser apps on their Android personally-owned work profile devices, users that enrolled before January 2021 must enable browser access as follows:
>
> 1. Launch the **Company Portal** app.
> 2. Go to the **Settings** page from the menu.
> 3. In the **Enable Browser Access** section, tap the **ENABLE** button.
> 4. Close and then restart the browser app.
>
> This enables access in browser apps, but not to browser WebViews that open within apps.

## Applications available in Conditional Access for controlling Microsoft Intune

When you configure Conditional Access in the Azure AD portal, you have two applications to choose from:

1. **Microsoft Intune** - This application controls access to the Microsoft Endpoint Manager console and data sources. Configure grants/controls on this application when you want to target the Microsoft Endpoint Manager console and data sources.
2. **Microsoft Intune Enrollment** - This application controls the enrollment workflow. Configure grants/controls on this application when you want to target the enrollment process. For more information, see [Require multi-factor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md).

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

- **Hybrid Azure AD joined:** This option is commonly used by organizations that are reasonably comfortable with how they're already managing their PCs through AD group policies or Configuration Manager.

- **Azure AD domain joined and Intune management:** This scenario is for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure). Azure AD Join works well in a hybrid environment, enabling access to both cloud and on-premises apps and resources. The device joins to the Azure AD and gets enrolled to Intune, which can be used as a Conditional Access criteria when accessing corporate resources.

### Bring your own device (BYOD)

- **Workplace join and Intune management:** Here the user can join their personal devices to access corporate resources and services. You can use Workplace join and enroll devices into Intune MDM to receive device-level policies, which are another option to evaluate Conditional Access criteria.

Learn more about [Device Management in Azure Active Directory](/azure/active-directory/devices/overview).

## App-based Conditional Access

Intune and Azure AD work together to make sure only managed apps can access corporate e-mail or other Microsoft 365 services.

- Learn more about [app-based Conditional Access with Intune](app-based-conditional-access-intune.md).

## Intune Conditional Access for Exchange on-premises

Conditional Access can be used to allow or block access to **Exchange on-premises** based on the device compliance policies and enrollment state. When Conditional Access is used in combination with a device compliance policy, only compliant devices are allowed access to Exchange on-premises.

You can configure advanced settings in Conditional Access for more granular control such as:

- Allow or block certain platforms.

- Immediately block devices that aren't managed by Intune.

Any device used to access Exchange on-premises is checked for compliance when device compliance and Conditional Access policies are applied.

When devices don't meet the conditions set, the end user is guided through the process of enrolling the device to fix the issue that is making the device noncompliant.

> [!NOTE]
> Beginning in July of 2020, support for the Exchange connector is deprecated, and replaced by Exchange [hybrid modern authentication](/office365/enterprise/hybrid-modern-auth-overview) (HMA). Use of HMA does not require Intune to setup and use the Exchange Connector. With this change, the UI to configure and manage the Exchange Connector for Intune has been removed from the Microsoft Endpoint Manager admin center, unless you already use an Exchange connector with your subscription.
>
> If you have an Exchange Connector set up in your environment, your Intune tenant remains supported for its use, and you’ll continue to have access to UI that supports its configuration. For more information, see [Install Exchange on-premises connector](../protect/exchange-connector-install.md). You can continue to use the connector or configure HMA and then uninstall your connector.
>
> Hybrid Modern Authentication provides functionality that was previously provided by the Exchange Connector for Intune: Mapping of a device identity to its Exchange record.  This mapping now happens outside of a configuration you make in Intune or the requirement of the Intune connector to bridge Intune and Exchange. With HMA, the requirement to use the ‘Intune' specific configuration (the connector) has been removed.

### What's the Intune role?

Intune evaluates and manages the device state.

### What's the Exchange server role?

Exchange server provides API and infrastructure to move devices to quarantine.

> [!IMPORTANT]
> Keep in mind that the user who's using the device must have a compliance profile and Intune license assigned to them so the device can be evaluated for compliance. If no compliance policy is deployed to the user, the device is treated as compliant and no access restrictions are applied.

## Next steps

[How to configure Conditional Access in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)

[Set up app-based Conditional Access policies](app-based-conditional-access-intune-create.md)

[How to create a Conditional Access policy for Exchange on-premises](conditional-access-exchange-create.md)
