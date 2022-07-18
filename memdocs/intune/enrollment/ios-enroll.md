---
# required metadata

title: Enroll iOS/iPadOS devices in Intune in Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Enrollment summary and overview of iOS/iPadOS devices in Microsoft Intune. Get information on the different enrollment methods.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Enroll iOS/iPadOS devices in Intune

Intune enables mobile device management (MDM) of iPads and iPhones to give users secure access to company email, data, and apps.

As an Intune admin, you can set up enrollment for iOS/iPadOS and iPadOS devices to access company resources. You can let users enroll personally-owned devices, known as "bring your own device" (BYOD) enrollment. You can also set up enrollment of company-owned devices.

## Prerequisites for iOS/iPadOS enrollment

Before you can enable iOS/iPadOS devices, complete the following steps:

- [Make sure your devices are supported](../fundamentals/supported-devices-browsers.md).
- [Set up Intune](../fundamentals/setup-steps.md) - These steps set up your Intune infrastructure. In particular, device enrollment requires that you [set your MDM authority](../fundamentals/mdm-authority-set.md).
- [Get an Apple MDM Push certificate](apple-mdm-push-certificate-get.md) - Apple requires a certificate to enable management of iOS/iPadOS and macOS devices.

## User-owned iOS/iPadOS and iPadOS devices (BYOD)

You can let users enroll their personal devices for Intune management, know as "bring your own device" or BYOD. There are three options for enrolling users:
- App Protection Policies give you the lightest BYOD experience, providing management at an app level only. However, if you want to also secure the device with a 6-digit complex PIN, you can use these policies along with User Enrollment.
- Device Enrollment is what you may think of as typical BYOD enrollment. It provides admins with a wide range of management options.
- User Enrollment is a more streamlined enrollment process that provides admins with a subset of device management options. This feature is currently in preview. 

After you've completed the prerequisites and assigned user licenses, users can download the Intune Company Portal app from the App Store, and follow enrollment instructions in the app. You can customize the Company Portal privacy statement on iOS/iPadOS devices as explained in [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md#configuration).

## Company-owned iOS/iPadOS devices

For organizations that buy devices for their users, Intune supports the following iOS/iPadOS company-owned device enrollment methods:

- Apple's Automated Device Enrollment (ADE)
- Apple School Manager
- Apple Configurator Setup Assistant enrollment
- Apple Configurator direct enrollment

You can also enroll company-owned iOS/iPadOS devices with a [device enrollment manager](device-enrollment-manager-enroll.md) account.

## Automated Device Enrollment

Organizations can purchase iOS/iPadOS devices through Apple's Automated Device Enrollment (ADE). ADE lets you deploy an enrollment profile "over the air" to bring devices into management. For more information, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](device-enrollment-program-enroll-ios.md).

## User enrollment
User Enrollment gives admins a subset of management options compared to other enrollment methods. For more information, see [User Enrollment supported actions, passwords, and other options](ios-user-enrollment-supported-actions.md) and [Set up iOS/iPadOS and iPadOS User Enrollment](ios-user-enrollment.md).

## Apple School Manager

Apple School Manager is a device purchase and enrollment program for schools. Like ADE, you can deploy a profile to enroll devices in management. Learn more about [Apple School Manager](apple-school-manager-set-up-ios.md).

## Apple Configurator

You can enroll iOS/iPadOS devices with Apple Configurator running on a Mac computer. To prepare devices, you USB-connect them and install an enrollment profile. You can enroll devices with Apple Configurator in two ways:

- Setup Assistant enrollment - Wipes the device, prepares it to run Setup Assistant, and installs the company's policies for the device's new user.
- Direct enrollment - Doesn't wipe the device and enrolls the device with a predefined policy. This method is for devices with no user affinity.

Learn more about [Apple Configurator enrollment](apple-configurator-enroll-ios.md).

## Use the Company Portal on ADE-enrolled or Apple Configurator-enrolled devices

Devices configured with user affinity can install and run the Company Portal app to download apps and manage devices. After users receive their devices, they must complete a number of additional steps to complete the Setup Assistant and install the Company Portal app.

User affinity is required to support the following:

- App Protection Policy (APP) apps
- Conditional Access to email and company data
- Company Portal app

### How users enroll corporate-owned iOS/iPadOS devices with user affinity

1. When users turn on their device, they are prompted to complete the Setup Assistant.
2. After completing setup, users are prompted for an Apple ID. They must provide an Apple ID to allow the device to install Company Portal.
3. The iOS/iPadOS device automatically installs the Company Portal app from the App Store.
4. Users should launch the Company Portal app and sign in using the credentials (like the unique personal name or UPN) that are associated with their subscription in Intune.
5. After logging in, enrollment is complete. Users can now use this device with the full set of capabilities.

### About corporate-owned managed devices with no user affinity

The Company Portal app is designed for users who have corporate credentials, and require access to personalized corporate resources (like email). On devices configured with no user affinity, the Company Portal app isn't needed. Devices that are enrolled with no user affinity aren't intended to have a dedicated user sign in. Kiosk, point of sale (POS), or shared-utility devices are typical use cases for devices that are enrolled with no user affinity.

In some situations, you might want to associate a primary user on devices enrolled without user affinity. To do this, add the Company Portal app using an app configuration policy. For more information, see [Configure the Company Portal app to support iOS and iPadOS devices enrolled with Automated Device Enrollment](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment).

If user affinity is required, be sure that the device's enrollment profile has **User Affinity** selected before enrolling the device. To change the affinity status on a device, you must retire the device and reenroll it.

## See also

[Troubleshooting iOS/iPadOS device enrollment problems in Microsoft Intune](https://support.microsoft.com/help/4039809)
