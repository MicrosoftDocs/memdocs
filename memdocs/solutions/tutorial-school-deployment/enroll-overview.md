---
title: Device enrollment overview
description: Learn about the different options to enroll Windows devices in Microsoft Intune
ms.date: 11/09/2023
ms.topic: overview
zone_pivot_groups: platforms-windows-ios
author: scottbreenmsft
ms.author: scbree
---

# Device enrollment overview

::: zone pivot="windows"

There are three main methods for joining Windows devices to Microsoft Entra ID and getting them enrolled and managed by Intune:

- **Automatic Intune enrollment via Microsoft Entra join** happens when a user first turns on a device that is in out-of-box experience (OOBE), and selects the option to join Microsoft Entra ID. In this scenario, the user can customize certain Windows functionalities before reaching the desktop, and becomes a local administrator of the device. This option isn't an ideal enrollment method for education devices
- **Bulk enrollment with provisioning packages.** Provisioning packages are files that can be used to set up Windows devices, and can include information to connect to Wi-Fi networks and to join a Microsoft Entra tenant. Provisioning packages can be created using either **Set Up School PCs** or **Windows Configuration Designer** applications. These files can be applied during or after the out-of-box experience
- **Enrollment via Windows Autopilot.** Windows Autopilot is a collection of cloud services to configure the out-of-box experience, enabling light-touch or zero-touch deployment scenarios. Windows Autopilot simplifies the Windows device lifecycle, from initial deployment to end of life, for OEMs, resellers, IT administrators and end users

::: zone-end

::: zone pivot="ios"

There are four main methods for joining iOS devices to Microsoft Entra ID and getting them enrolled and managed by Intune:

- **Manual enrollment using Company Portal** is performed by the user by downloading and installing the Company Portal app from the App store and following the instructions to enroll the device. The device is enrolled with personal ownership. This option isn't an ideal enrollment method for education devices
- **Automated Device Enrollment** applies your organization's settings from Apple School Manager and enrolls devices without IT needing to physically interact with the device. iPhones and iPads can be shipped directly to employees and students. When they turn on their devices, Apple Setup Assistant guides them through setup and enrollment. Devices can be configured with user affinity for use with one user or no user affinity for shared device scenarios.
- **Apple Configurator** can be used on a Mac to apply configuration including enrollment information to one or more iPhones or iPads. This scenario is best suited for when IT has physical access to the devices and doesn't want to use Apple School Manager and Automated Device Enrollment.s

::: zone-end

## Choose the enrollment method

::: zone pivot="windows"

**Windows Autopilot** and the **Set up School PCs** app are usually the most efficient options for school environments.

This [table][INT-1] describes the ideal scenarios for using either option. It's recommended to review the table when planning your enrollment and deployment strategies.

::: zone-end

::: zone pivot="ios"

**Automated Device Enrollment** is usually the most efficient option for school environmments.

::: zone-end

:::image type="content" source="./images/enroll.png" alt-text="The device lifecycle for Intune-managed devices - enrollment" border="false":::

Select one of the following options to learn the next steps about the enrollment method you chose:

::: zone pivot="windows"
- [Automatic Intune enrollment via Microsoft Entra join](enroll-entra-join.md)
- [Bulk enrollment with provisioning packages](enroll-package.md)
- [Enroll devices with Windows Autopilot](enroll-autopilot.md)
::: zone-end

::: zone pivot="ios"
- [Company Portal](enroll-ios-company-portal.md)
- [Automated Device Enrollment](enroll-ios-ade.md)
- [Apple Configurator](enroll-ios-apple-configurator.md)
::: zone-end

<!-- Reference links in article -->

[INT-1]: /intune-education/add-devices-windows#when-to-use-set-up-school-pcs-vs-windows-autopilot
