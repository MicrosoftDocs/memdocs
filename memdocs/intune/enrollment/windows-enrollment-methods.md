---
# required metadata

title: Intune enrollment methods for Windows devices
titleSuffix: Microsoft Intune
description: Learn the different ways you can enroll Windows devices in Intune
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/25/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.custom: 
ms.collection: 
---

# Intune enrollment methods for Windows devices

To manage devices in Intune, devices must first be enrolled in the Intune service. Both personally owned and corporate-owned devices can be enrolled for Intune management. 

There are two ways to get devices enrolled in Intune:
- Users can self-enroll their Windows PCs 
- Admins can configure policies to force automatic enrollment without any user involvement

## User self-enrollment in Intune

Users can self-enroll their Windows device by using any of these methods:

- [Bring your own device (BYOD)](https://docs.microsoft.com/intune-user-help/enroll-windows-10-device): Users enroll their personally owned devices by choosing to connect a **Work and School** account from **Settings** of the device. This process:
  - Registers the device with Azure Active Directory to gain access to corporate resource like email.
  - Enrolls the device in Intune as a personal owned device (BYOD).
If an administrator has configured Auto enrollment (available with Azure AD premium subscriptions), the user only has to enter their credentials once. Otherwise, they’ll have to enroll separately through MDM only enrollment and reenter their credentials.  
- **MDM only enrollment** lets users enroll an existing Workgroup, Active Directory, or Azure Active directory joined PC into Intune. Users enroll from Settings on the existing Windows PC. This method isn’t recommended because it doesn’t register the device into Azure Active Directory. It also prevents the use of features such as Conditional Access.
- [Azure Active Directory (Azure AD) Join](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network) - Joins the device with Azure Active Directory and enables users to sign in to Windows with their Azure AD credentials. If Auto Enrollment is enabled, the device is automatically enrolled in Intune. The benefit of auto enrollment is a single-step process for the user. Otherwise, they’ll have to enroll separately through MDM only enrollment and reenter their credentials. Users enroll this way either during initial Windows OOBE or from Settings. The device is marked as a corporate owned device in Intune.
- [Autopilot](enrollment-autopilot.md) - Automates Azure AD Join and enrolls new corporate-owned devices into Intune. This method simplifies the out-of-box experience and removes the need to apply custom operating system images onto the devices. When admins use Intune to manage Autopilot devices, they can manage policies, profiles, apps, and more after they're enrolled.  There are four types of Autopilot deployment: [Self Deploying Mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying) (for kiosks, digital signage, or a shared device), [User Driven Mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) (for traditional users), [White Glove](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove) enables partners or IT staff to pre-provision a Windows 10 PC so that it is fully configured and business-ready and [Autopilot for existing devices](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) enables you to easily deploy the latest version of Windows 10 to your existing devices.

## Administrator-based enrollment in Intune

Administrators can set up the following methods of enrollment that require no user interaction:

- [Hybrid Azure AD Join](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) lets administrators configure Active Directory group policy to automatically enroll devices that are hybrid Azure AD joined. 
- [Configuration Manager Co-management](https://docs.microsoft.com/configmgr/comanage/overview) lets administrators enroll their existing Configuration Manager managed devices into Intune to get the dual benefits of Intune and Configuration Manager. 
- [Device enrollment manager](device-enrollment-manager-enroll.md) (DEM) is a special service account. DEM accounts have permissions that let authorized users enroll and manage multiple corporate-owned devices. These types of devices are good for point-of-sale or utility apps, for example, but not for users who need to access email or company resources. This method does not allow the use of features such as Conditional Access. 
- [Bulk enroll](../windows-bulk-enroll.md) lets an authorized user join large numbers of new corporate-owned devices to Azure Active Directory and Intune. You create a provisioning package with the Windows Configuration Designer (WCD) app. Then, using USB media during initial Windows OOBE experience or from existing Windows PC, you install the provisioning package to automatically enroll the devices into Intune. This method does not allow the use of Conditional Access. 
- [Enrolling Windows IoT Core devices](https://docs.microsoft.com/windows/iot-core/manage-your-device/intunedeviceenrollment) is accomplished by using the Windows IoT Core Dashboard to prepare the device, and then using Windows Configuration Designer to create a provisioning package. Then, using SD Card media during initial boot up, it installs the provisioning package to automatically enroll the devices into Intune.

## Next steps

[Learn the capabilities of the Windows enrollment methods](enrollment-method-capab.md)
