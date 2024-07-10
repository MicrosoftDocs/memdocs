---
# required metadata

title: Device enrollment guide for Microsoft Intune
description: Enroll Android, Android Enterprise, iOS, iPadOS, Linux, macOS, and Windows devices in Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/24/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Enrollment guide: Microsoft Intune enrollment

Microsoft Intune, together with Microsoft Entra ID, facilitates a secure, streamlined process for registering and enrolling devices that want access to your internal resources. Once users and devices are registered within your Microsoft Entra ID (also called a *tenant*), then you can utilize Intune for its endpoint management capabilities. The process that enables device management for a device is called **device enrollment**.

During enrollment, Intune installs a Mobile Device Management (MDM) certificate on the enrolling device. The MDM certificate communicates with the Intune service, and enables Intune to start enforcing your organization's policies, like:  

- Enrollment policies that limit the number or type of devices someone can enroll.  
- Compliance policies that help users and devices meet your rules.  
- Configuration profiles that configure work-appropriate features and settings on devices.  

:::image type="content" source="./media/deployment-guide-enrollment/mdm-certificate.png" alt-text="Diagram that shows the device enrolls, the object is created in Microsoft Entra ID, and the MDM certificate is pushed to these devices in Microsoft Intune.":::

Typically, policies are deployed during enrollment. Some groups, depending on their roles in your organization, can require stricter policies than others. Many organizations start by creating a baseline of required policies for users and devices. Then, add to this baseline as needed for different groups and use cases.

You can enroll devices running on the following platforms. For a list of supported versions, go to [Supported operating systems](supported-devices-browsers.md).

- Android
- iOS/iPadOS
- Linux
- macOS
- Windows

Enrollment is enabled for all platforms by default, but you can restrict specific platforms from enrolling by using an Intune [enrollment restriction policy](../enrollment/enrollment-restrictions-set.md).

This article describes the supported device scenarios and enrollment prerequisites, has information about using other MDM providers, and includes links to platform-specific enrollment guidance.  

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]  

## Supported device scenarios

Microsoft Intune enables mobile device management for:

- Personal devices, including personally owned phones, tablets, and PCs.
- Corporate-owned devices, including phones, tablets, and PCs owned by your organization and distributed to employees and students for use at work or school.

### Personal devices

Devices in bring-your-own-device (BYOD) scenarios can be MDM enrolled in Intune. The supported enrollment methods enable employees and students to use their personal devices for work or school tasks.

As the admin, you add device users in the Microsoft Intune admin center, configure their enrollment experience, and set up Intune policies. In the Intune Company Portal app, the device user starts and completes the enrollment.

To determine if enrolling personal devices in Intune is right for your organization, go to [Intune planning guide: Personal devices vs Organization-owned devices](intune-planning-guide.md#personal-devices-vs-organization-owned-devices).

> [!NOTE]
> Intune marks devices that are [Microsoft Entra registered](/entra/identity/devices/concept-device-registration) as personally-owned devices.  

### Corporate-owned devices  

Microsoft Intune offers more granular settings and policies for devices classified as **corporate-owned** or **organization-owned**. There are more password settings available for corporate-owned devices. So, you can enforce stricter password requirements.

Microsoft Intune automatically marks devices that meet certain criteria as corporate-owned. For more information, go to [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md).

## Prerequisites  

- Intune is set up, and ready to enroll users and devices. Be sure:

  - The [MDM Authority](mdm-authority-set.md) is set to Intune, even when using [co-management](../../configmgr/comanage/overview.md) with Intune + Configuration Manager.
  - [Intune licenses are assigned](licenses-assign.md).

  For more information, go to the [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](supported-devices-browsers.md). This requirement includes devices that are co-managed, or Microsoft Entra hybrid joined devices.

- Sign in as a member of the **Policy and Profile Manager** built-in Intune role. For information on the permissions in this role, go to [Built-in role permissions for Microsoft Intune - Policy and Profile manager](role-based-access-control-reference.md#policy-and-profile-manager).

  If you created an Intune Trial subscription, then the account that created the subscription is the Global Administrator.

  The Global Administrator has more permissions than needed to create enrollment policies. We recommend you use the least privileged role to complete this task, which is the **Policy and Profile Manager** built-in Intune role.

  It's possible some enrollment platforms might require a more privileged Microsoft Entra role, like the **Intune Administrator** built-in role. For information on this role, go to [Microsoft Entra built-in roles - Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).

- Different platforms can have other requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md). Any other platform requirements are listed.

  | Platform | Other requirements |
  | --- | --- |
  | Android | none |
  | Android Enterprise | none |
  | iOS/iPadOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)<br/>Apple ID |
  | Linux | none |
  | macOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) |
  | Windows | none |

- Have your user groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then go to [Planning Guide: Step 4 - Review existing policies and infrastructure](intune-planning-guide.md#step-4---review-existing-policies-and-infrastructure).

- If you're bulk enrolling devices, consider creating the **Device enrollment manager** (DEM) account. The DEM account can enroll up to 1,000 mobile devices. Use this account to enroll and configure the devices before giving them to users. The DEM account is an Intune permission that applies to a Microsoft Entra user account. This type of account isn't compatible with all enrollment methods, like Apple automated device enrollment.

  For more information, go to [Enroll devices using a DEM account](../enrollment/device-enrollment-manager-enroll.md).  

## Unenroll from existing MDM and factory reset

If devices are currently enrolled in another MDM provider, then unenroll the devices from the existing MDM provider. Typically, unenrolling doesn't remove existing features and settings you configured. Most MDM providers have remote actions that remove organization-specific data from devices. Before enrolling in Intune, you can remove organization-specific data from these devices. But, it isn't required.

Depending on the platform, a factory reset might be required before enrolling in Intune.

-----
| Platform | Factory reset required? |
| --- | --- |
| Android Enterprise personally owned devices with a work profile (BYOD) | No |
| Android Enterprise corporate-owned work profile (COPE) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android device administrator (DA) | No |
| iOS/iPadOS | Yes |
| Linux | No |
| macOS | Yes |
| Windows | No |

-----

On the platforms that don't require a factory reset, when these devices enroll in Intune, they start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible previously configured settings remain configured on devices.

## Choose your platform enrollment guide

There's an enrollment guide for every platform. Choose your scenario, and get started:

- [Application management without enrollment (MAM-WE)](deployment-guide-enrollment-mamwe.md)
- [Android](deployment-guide-enrollment-android.md)
- [iOS/iPadOS](deployment-guide-enrollment-ios-ipados.md)
- [Linux](deployment-guide-enrollment-linux.md)
- [macOS](deployment-guide-enrollment-macos.md)
- [Windows](deployment-guide-enrollment-windows.md)

## Download the visual enrollment guide

There's also a visual guide of the different enrollment options for each platform:

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the enrollment profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the enrollment profile to more pilot groups.

For more information and suggestions, go to the [Planning guide: Step 5 - Create a rollout plan](intune-planning-guide.md#step-5---create-a-rollout-plan).  

## Mobile device record cleanup  

The MDM certificate renews automatically as long as enrolled devices are communicating with the Microsoft Intune service. The MDM certificate doesn't renew for devices that are wiped, or devices that fail to sync with Microsoft Intune for an extended period of time. Microsoft Intune deletes idle devices from record 180 days after the MDM certificate expires.  

## Reporting and troubleshooting

- [Incomplete user enrollments](../enrollment/enrollment-report-company-portal-abandon.md)
- [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)

## Next steps  

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. [Configure device features](deployment-plan-configuration-profile.md)
5. 🡺 **Enroll devices** (*You are here*)

For platform-specific enrollment guidance, go to:

- [Application Management without enrollment](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)  
