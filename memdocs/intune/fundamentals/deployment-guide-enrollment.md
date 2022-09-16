---
# required metadata

title: Device enrollment guide for Microsoft Intune
description: Enroll Android, Android Enterprise, iOS, iPadOS, macOS, and Windows devices In Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2022
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
  - M365-identity-device-management
  - highpri
  - highseo
---

# Deployment guidance: Enroll devices in Microsoft Intune

Azure AD is the backbone of Intune and Endpoint Manager. Once users and devices are registered within your Azure AD (also called a tenant), then it's available to Intune and Endpoint Manager. This feature is called "enrollment".

Enrolling devices allows them to receive the policies you create. The policies can include:

- Compliance policies that help users and devices meet your rules.
- Configuration profiles that configure features and settings on devices.

Many organizations create a baseline of what all users and devices must have. Typically, these policies get deployed during enrollment. For example, you might create a VPN connection, install an authentication certificate, and require Windows Hello PIN. For more information on enrollment, see [What is device enrollment?](../enrollment/device-enrollment.md).

When a device is enrolled, it's issued an MDM certificate. This certificate communicates with the Intune service.

You can enroll devices on the following platforms. For the specific versions, see [Supported operating systems](supported-devices-browsers.md):

- Android
- iOS/iPadOS
- macOS
- Windows

This article lists the enrollment prerequisites, has information on using other MDM providers, and includes links to platform-specific enrollment guidance.

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Prerequisites

- Intune is set up, and ready to enroll users and devices. Be sure:

  - The [MDM Authority](mdm-authority-set.md) is set to Intune, even when using [co-management](../../configmgr/comanage/overview.md) with Intune + Configuration Manager.
  - [Intune licenses are assigned](licenses-assign.md).

  For more information, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).

- Your devices [are supported](supported-devices-browsers.md). This requirement includes devices that are co-managed, or hybrid Azure Active Directory (Azure AD) joined devices.

- Sign in as a member of the **Global Administrator** or **Intune Service Administrator** Azure AD roles. [Role-based access control (RBAC) with Intune](role-based-access-control.md) has more information. If you created an Intune trial subscription, then the account that created the subscription is the **Global administrator**.

- Different platforms may have other requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md). Any other platform requirements are listed.

  | Platform | Other requirements |
  | --- | --- |
  | Android | none |
  | Android Enterprise | none |
  | iOS/iPadOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md)<br/>Apple ID |
  | macOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) |
  | Windows | none |

- Have your user groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then see [Planning Guide: Task 4: Review existing policies and infrastructure](intune-planning-guide.md#task-4-review-existing-policies-and-infrastructure).

- If you're bulk enrolling devices, consider creating the **Device enrollment manager** (DEM) account. This account is an Intune permission that's applied to an Azure AD user account. The DEM account can enroll up to 1,000 mobile devices. Use this account to enroll and configure the devices before giving them to users.

  For more information, see [Enroll devices using a DEM account](../enrollment/device-enrollment-manager-enroll.md).

## Unenroll from existing MDM and factory reset

If devices are currently enrolled in another MDM provider, then unenroll the devices from the existing MDM provider. Typically, unenrolling doesn't remove existing features and settings you configured. Most MDM providers have remote actions that remove organization-specific data from devices. Before enrolling in Intune, you can remove organization-specific data from these devices. But, it's not required.

Depending on the platform, a factory reset may be required before enrolling in Intune.

-----
| Platform | Factory reset required? |
| --- | --- |
| Android Enterprise personally owned devices with a work profile (BYOD) | No |
| Android Enterprise corporate-owned work profile (COPE) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android device administrator (DA) | No |
| iOS/iPadOS | Yes |
| macOS | Yes |
| Windows | No |

-----

On the platforms that don't require a factory reset, when these devices enroll in Intune, they'll start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible previously configured settings remain configured on devices.

## Choose your platform enrollment guide

There's an enrollment guide for every platform. Choose your scenario, and get started:

- [Application management without enrollment (MAM-WE)](deployment-guide-enrollment-mamwe.md)
- [Android](deployment-guide-enrollment-android.md)
- [iOS/iPadOS](deployment-guide-enrollment-ios-ipados.md)
- [macOS](deployment-guide-enrollment-macos.md)
- [Windows](deployment-guide-enrollment-windows.md)

## Download the visual enrollment guide

There's also a visual guide of the different enrollment options for each platform:

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)

## Pilot groups

When assigning your profiles, start small, and use a staged approach. Assign the enrollment profile to a pilot or test group. After initial testing, add more users to the pilot group. Then, assign the enrollment profile to more pilot groups.

For more information and suggestions, see the [Planning guide: Task 5: Create a rollout plan](intune-planning-guide.md#task-5-create-a-rollout-plan).

## Reporting and troubleshooting

- [Incomplete user enrollments](../enrollment/enrollment-report-company-portal-abandon.md)
- [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)

## Next steps

Choose your platform, and get started:

- [Application Management without enrollment](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)