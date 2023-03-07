---
# required metadata

title: Device enrollment guide for Microsoft Intune
description: Enroll Android, Android Enterprise, iOS, iPadOS, Linux, macOS, and Windows devices in Intune. Decide which enrollment method to use, and get an overview of the administrator and end user tasks to enroll devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/31/2023
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

Microsoft Intune, in conjunction with Azure Active Directory (Azure AD), facilitates a secure, streamlined process for registering and enrolling devices that want access to your internal resources. Once users and devices are registered within your Azure AD (also called a *tenant*), then you can utilize Intune for its endpoint management capabilities. The process that enables device management for a device is called *device enrollment*. 

During enrollment, Intune installs an MDM certificate on the enrolling device. The MDM certificate communicates with the Intune service, and enables Intune to start enforcing your organization's policies, such as:  
 
- Enrollment policies that limit the number or type of devices someone can enroll.  
- Compliance policies that help users and devices meet your rules.  
- Configuration profiles that configure work-appropriate features and settings on devices.  

Typically, policies are deployed during enrollment.  Some groups, depending on their roles in your organization, may require stricter policies than others. Many organizations start by creating a baseline of required policies for users and devices, and build them out as needed for different groups and use cases. 

You can enroll devices running on the following platforms. For a list of supported versions, see [Supported operating systems](supported-devices-browsers.md). 

- Android
- iOS/iPadOS
- Linux
- macOS
- Windows

Enrollment is enabled for all platforms by default, but you can restrict specific platforms from enrolling by using an Intune enrollment restriction policy.     

This article describes the supported device scenarios and enrollment prerequisites, has information about using other MDM providers, and includes links to platform-specific enrollment guidance.  

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]  

## Supported device scenarios    
Microsoft Intune enables mobile device management for:   
* Personal devices, including personally owned phones, tablets, and PCs. 
* Corporate-owned devices, including phones, tablets, and PCs owned by your organization and distributed to employees and students for use at work or school. 

### Personal devices  
Devices in bring-your-own-device (BYOD) scenarios can be enrolled in Intune. The supported enrollment methods enable employees and students to use their personal devices for work or school things. As the admin, you're required to add device users in the Microsoft Intune admin center, configure their enrollment experience, and set up Intune policies. Enrollment is initiated and completed by the device user in the Intune Company Portal app.  

> [!NOTE]
> Intune marks devices that are Azure AD-registered as personally-owned devices.  

### Corporate-owned devices  

Microsoft Intune offers more granular settings and policies for devices classified as *corporate-owned*. For example, there are more password policies to choose from in Intune for corporate-owned devices, so you can enforce stricter password requirements. Microsoft Intune automatically marks devices that meet certain criteria as corporate-owned. For more information, see [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md).   

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

- If you're bulk enrolling devices, consider creating the **Device enrollment manager** (DEM) account. The DEM account can enroll up to 1,000 mobile devices. Use this account to enroll and configure the devices before giving them to users. The DEM account is an Intune permission that's applied to an Azure AD user account. This type of account isn't compatible with all enrollment methods, such as Apple automated device enrollment. 

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

## Mobile device record cleanup  

The MDM certificate renews automatically as long as enrolled devices are communicating with the Microsoft Intune service. The MDM certificate doesn't renew for devices that have been wiped, or devices that fail to sync with Microsoft Intune for an extended period of time. Microsoft Intune deletes idle devices from record 180 days after the MDM certificate expires.  

## Reporting and troubleshooting

- [Incomplete user enrollments](../enrollment/enrollment-report-company-portal-abandon.md)
- [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)

## Next steps  

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. [Configure device features](deployment-plan-configuration-profile.md)
5. 🡺 **Enroll devices** (*You are here*)

For platform-specific enrollment guidance, see:

- [Application Management without enrollment](deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)  


