---
# required metadata

title: Getting started with Microsoft Intune
description: Learn about the Microsoft Intune deployment, enrollment, configuration, policies, service updates, and more.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/27/2022
ms.topic: overview
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
  - get-started
  - intro-get-started
ms.collection:
  - M365-identity-device-management
  - highpri
  - highseo
---

# Get started with Microsoft Intune

As part of your Microsoft 365 license, you also get Microsoft Intune for cloud-based app management, device management, and security. 

This article provides an overview of the Microsoft Intune architecture, deployment, enrollment, configuration, policies, service updates, and more.


For more information about what Microsoft Intune can do for your organization, go to [What is Microsoft Intune](what-is-intune.md).

## Cloud attach with Configuration Manager

Microsoft Endpoint Configuration Manager helps you protect on-premises Windows Server, devices, apps, and data. If you need to manage only cloud-based endpoints, you can use Microsoft Intune. If you need to manage only on-premises endpoints, such as the computers your organization has attached to your internal network, you can use Configuration Manager. However, if you need to manage a combination of both cloud and on-premises endpoints, you can use cloud attach to use both Intune and Configuration Manager from Microsoft Endpoint Manager.

There are two steps to cloud attach your on-premises devices:

1. [Tenant attach](./configmgr/tenant-attach/index.yml): Register your Intune tenant with your Configuration Manager deployment.
2. [Co-management](./configmgr/comanage/index.yml): Concurrently managing Windows client devices with both Configuration Manager and Microsoft Intune.

These steps are incremental steps on the journey to having full cloud attachment. You get immediate value through tenant attach and you get more value through co-management.

## Step 1 - Plan your Intune deployment

A successful adoption or migration to Microsoft Intune starts with a plan. This plan depends on your organization's current device management solution, business goals, and technical requirements. Additionally, you should include key stakeholders who will support and collaborate with the plan.

The following resources will help you plan your Intune deployment:

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)
- [Set up Microsoft Intune](setup-steps.md)

> [!TIP]
> To step through some online training, go to:
>
> - [Microsoft Endpoint Manager fundamentals](/training/paths/endpoint-manager-fundamentals/)
> - [Plan your migration to Microsoft Endpoint Manager](/training/modules/paths-to-modern-endpoint-management/)
> - [Determine your endpoint management implementation](/training/modules/determine-endpoint-implementation/)

## Enroll your devices

Using Intune, you can manage devices and apps, and how they access organization data. To use Intune mobile device management (MDM), the devices must enroll in the Intune service. When they're enrolled, these devices are managed by your organization, and can receive your app and device policies, security policies, and compliance policies.

When a device enrolls, it's issued a secure MDM certificate. This certificate communicates with the Intune service.

Devices can be enrolled on the following platforms. For the specific versions, see [Supported operating systems](supported-devices-browsers.md):

- Android
- iOS/iPadOS
- macOS
- Windows

Different platforms may have other requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md).

The following resources will help you learn more about device enrollment for each platform:

- [What is device enrollment in Intune?](../enrollment/device-enrollment.md)
- [Enrolled device management capabilities of Microsoft Intune](../enrollment/device-management-capabilities.md)
- [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS/iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Configure device features

Microsoft Intune includes settings and features you can enable or disable on the many different devices in your organization. These settings and features are added to configuration profiles. When the profiles are ready, you use Intune to apply, or "assign" the profiles to your devices.

The following resources will help you understand how to configure device settings:

- [Apply features and settings on your devices using device profiles](../configuration/device-profiles.md)
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Assign device profiles in Microsoft Intune](../configuration/device-profile-assign.md)
- [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md)
- Security configuration framework with recommendations for [Android Enterprise](../enrollment/android-configuration-framework.md) and [iOS/iPadOS](../enrollment/ios-ipados-configuration-framework.md)
- [Windows security baselines](/windows/security/threat-protection/windows-security-baselines)

## Check for compliance

MDM solutions like Intune can set rules that devices should meet, and can report the compliance states of these rules. These rules are called compliance policies. When combine compliance policies with conditional access, you can require that devices meet certain security requirements before they can access your organization's data.

For example, you can require a strong passcode, require a device to be encrypted, block jailbroken or rooted devices, and more.

There are two parts to compliance policies in Intune:

- **Compliance policy settings**: These settings are tenant-wide settings and are similar to built-in compliance policies that every device automatically receives. Compliance policy settings set a baseline for how compliance policy works in your Intune environment. You also determine if devices that haven’t received any device compliance policies are compliant or noncompliant.

- **Device compliance policy**: The policies are platform-specific rules that admins can configure and deploy to groups of users or devices. These rules define requirements for devices, like minimum operating system version or using disk encryption. Devices must meet these rules to be considered compliant.

The following articles will help you understand how to create & monitor compliance policies in Intune, how to integrate with MTD & NAC solutions, and use conditional access:

- [Get started with device compliance policies in Microsoft Intune](../protect/device-compliance-get-started.md)
- [Create a compliance policy in Microsoft Intune](../protect/create-compliance-policy.md)
- [Intune reports for compliance, assignment failures, check-in status, and more](reports.md)
- [Enable Mobile Threat Defense connector in Microsoft Intune](../protect/mtd-connector-enable.md)
- [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md)
- [Network access control integration with Microsoft Intune](../protect/network-access-control-integrate.md)
- [Integrate with Conditional Access](../protect/device-compliance-get-started.md#integrate-with-conditional-access)
- [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md)
- [Conditional Access scenarios](../protect/conditional-access-intune-common-ways-use.md)
- [Monitor device compliance policies in Microsoft Intune](../protect/compliance-policy-monitor.md)

## Protect your apps

Intune app protection policies (APP) allow you to protect organizational data within an application. You can implement mobile application management (MAM) in Intune to help protect sensitive data that's accessed from managed applications. See the official list of [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md) available for public use.

Together with app configuration capabilities, 

To get an overview of app protection policies and how they work, go to the following articles:

- [App protection policies overview](../apps/app-protection-policy.md)
- [Data protection framework using app protection policies](../apps/app-protection-framework.md)
- [Understand app protection policy delivery timing](../apps/app-protection-policy-delivery.md)
- [How to create and assign app protection policies](../apps/app-protection-policies.md)
- [How to manage data transfer between iOS apps in Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md)
- [How to monitor app protection policies](../apps/app-protection-policies-monitor.md)
- [Review client app protection logs](../apps/app-protection-policy-settings-log.md)
- [Frequently asked questions about MAM and app protection](../apps/mam-faq.yml)

## Deliver apps to devices

Intune supports a wide range of apps, including store apps for Android, iOS/iPacOS, macOS, and Windows, and line-of-business (LOB) apps. You can manage app deployment from the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Also, you can use Intune to orchestrate store app deployment with managed Google Play, the Apple App Store, and the Microsoft Store.

Check out these resources to find out how to add and manage apps with Intune:

- [What is app management in Microsoft Intune](../apps/app-management.md)
- [Add apps to Microsoft Intune](../apps/apps-add.md)
- [Add and assign managed Google Play apps to Android Enterprise devices](../apps/apps-add-android-for-work.md)
- [Add iOS store apps to Microsoft Intune](../apps/store-apps-ios.md)
- [How to manage iOS and macOS apps purchased through Apple Business Manager](../apps/vpp-apps-ios.md)
- [Windows 10 app deployment by using Microsoft Intune](../apps/apps-windows-10-app-deploy.md)
- [How to protect your company app data with Microsoft Intune](/graph/api/resources/intune-app-conceptual?view=graph-rest-beta&preserve-view=true)
- [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md)

## Next steps

