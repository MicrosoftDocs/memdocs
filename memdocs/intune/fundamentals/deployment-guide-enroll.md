---
# required metadata

title: Device enrollment guide for Microsoft Intune
description: Enroll Android, Android Enterprise, iOS, iPadOS, Linux, macOS, and Windows devices in Intune. Decide which enrollment method to use, and learn about the administrator and end user tasks required to enroll devices.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/24/2022
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

# Step 5 – Enroll devices in Microsoft Intune

In the final step of deployment, devices are registered in your organization's Azure AD tenant, enrolled in Microsoft Intune, and checked for compliance.    

Azure AD registration is an important part of the enrollment process, because it enables employees to sign in and access work things on their devices with their work account. 

Device enrollment installs the mobile device management (MDM) certificate on the device, which enables the device to receive Intune policies and profiles such as:   

* Device enrollment restrictions
* Configuration profiles
* Compliance policies 
* Terms and conditions 
* Multifactor authentication 

The final component of enrollment is compliance. Upon enrollment, users on enrolled devices are immediately notified of your compliance policies; things like lock screen, OS, and encryption requirements. Devices must meet all requirements to gain access to your network.  

This article describes your enrollment options and 

## Supported devices     

The following types of devices can be enrolled in Intune:    

* Windows 10/11 (Home, Pro, Education, S mode, and Enterprise versions)
* Windows 10/11 Cloud PCs on Windows 365
* Windows 10 IoT and Windows 10 Holographic
* Windows 10 2019 LTSC
* Windows RT 8.1, and Windows 8.1 (sustaining mode)
* Apple iOS/iPadOS 13.0 and later
* Mac OS X 10.15 and later
* Android 6.0 and later, including Samsung Knox 2.4 and later and Android for Work

For more information, see [Supported operating systems](supported-devices-browsers.md).  

## Custom domain  

## Enrollment restrictions  

## Terms and conditions  

## Enable Apple device enrollment  

## Corporate identifiers   

## Multi-factor authentication  

## Device enrollment manager  

## Conditional access 

## CNAME registration  

## Automatic enrollment 
Employees and students can enroll their Windows devices in Intune with the help  automated enrollment. During this process, devices register and join Azure Active Directory. 

## Bulk enrollment  






## Intune client apps  
The Microsoft Intune app and Intune Company Portal app

### Intune Company Portal
The Company Portal is available as a web application and as an application for desktops and mobile devices on all platforms. Users use this portal to self-manage device enrollment and also to access applications that company administrator publishes. They access it via https://portal.manage.microsoft.com/ or by installing the Company Portal app on Windows, iOS, or Android devices.

### Microsoft Intune app 

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
  | Linux | none |
  | macOS | [MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) |
  | Windows | none |

- Have your user groups and device groups ready to receive your enrollment policies. If you haven't reviewed or created your group structure, and want some guidance, then see [Planning Guide: Step 4 - Review existing policies and infrastructure](intune-planning-guide.md#step-4---review-existing-policies-and-infrastructure).

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
| Linux | No |
| macOS | Yes |
| Windows | No |

-----

On the platforms that don't require a factory reset, when these devices enroll in Intune, they'll start receiving your Intune policies. If you don't configure a setting in Intune, then Intune doesn't change or update that setting. So, it's possible previously configured settings remain configured on devices.  

## Configure Intune for Apple Device Support

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

For more information and suggestions, see the [Planning guide: Step 5 - Create a rollout plan](intune-planning-guide.md#step-5---create-a-rollout-plan).

## Reporting and troubleshooting

- [Incomplete user enrollments](../enrollment/enrollment-report-company-portal-abandon.md)
- [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)

## Next steps

Choose your platform, and get started:

- [Application Management without enrollment](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)