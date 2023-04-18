---
# required metadata

title: Configure device and app compliance during an Intune migration
titleSuffix: Microsoft Intune
description: This article provides the necessary steps to configure device compliance and app management policies during a Microsoft Intune migration.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 0062d08e-e5b3-4f73-8b64-5ad95adbe945

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Configure device compliance and app management policies when migrating to Microsoft Intune

The main goal when migrating to Intune is to have all devices enrolled in Intune and compliant with its policies. Device policies not only help you to manage corporate-owned single-user devices, but also personal (BYOD), and shared devices such as kiosks, point-of-sales machines, tablets shared by multiple students in a classroom, or user-less devices (iOS only).

Each device platform may offer different settings, but Intune device policies work with each device platform by providing the following mobile device management capabilities:

- Regulate numbers of devices each user enrolls.

- Manage devices settings (for example, device-level encryption, password length, camera usage).

- Deliver apps, email profiles, VPN profiles, and so on.

- Evaluate device-level criteria for security compliance policies.

> [!IMPORTANT]
> Device management policies are not assigned directly to individual devices or users, but instead are assigned to user groups. The policies may be directly applied to a user group, and thereby to the user's device, or the policies may be applied to a device group, and thereby to group members.

## Task list for device compliance policies

### Task 1: Add device groups (optional)

You can create device groups when you need to perform administrative tasks based on device identity instead of user identity.

Device groups are useful for managing devices that do not have dedicated users, such as kiosk devices, devices shared by shift workers, or devices assigned to a specific location.

By configuring device groups ahead of device enrollment, you can use device categories to automatically join devices to groups upon enrollment. Then they will receive their group's device policies automatically. [Get started with groups](groups-get-started.md).

### Task 2: Use resource access profiles (Wi-Fi, VPN, and email certificates)

Resource access profiles supply certificates and access configurations to enrolled devices. If you are using certificate-based authentication, [configure certificates](../protect/certificates-configure.md).

### Task 3: Create and deploy device configuration profiles

You need to create a device configuration profile to enforce device-level settings, for example: disable camera, app-store, configure single-app mode, home screen, and so on. Learn about [device profiles](../configuration/device-profiles.md).

#### Directly import iOS/iPadOS configuration profiles (optional)

- **Apple Configurator iOS profiles (iOS 7.1 and later):** If your existing MDM solution uses Apple Configurator profiles (.mobileconfig files), Intune can directly import them as custom configuration policies.

- **iOS Mobile Application Configuration policies:** If your existing MDM solution uses iOS/iPadOS Mobile Application Configuration policies, Intune can directly import them as long as they meet the XML format specified by Apple for property lists.

- Learn how to add a custom policy for [iOS](../configuration/custom-settings-ios.md).

### Task 4: Create and deploy device compliance policies (optional)

Device compliance policies evaluate security-oriented settings, and provide reporting that shows whether the devices are compliant with corporate standards or not. Such settings include:

- PIN length

- Jail-broken status

- OS version

See additional resources for device compliance settings:

- Learn about [device compliance policies](../protect/device-compliance-get-started.md).

### Task 5: Publish and deploy apps

When using Intune MDM, you can supply apps by either requiring their automatic installation, or making them available in the Company Portal.

- [How to add apps](../apps/apps-add.md).

- [How to deploy apps](../apps/apps-deploy.md).

### Task 6: Enable device enrollment

Device enrollment is necessary to manage the device. Learn [how to get ready to enroll corporate-owned and user personal's devices](/mem/intune/fundamentals/deployment-guide-enrollment).

## Next steps

[Configure app protection policies (optional)](../apps/app-protection-policies.md).
