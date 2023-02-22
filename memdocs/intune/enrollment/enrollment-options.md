---
# required metadata

title: Enrollment options for devices managed by Microsoft Intune
titleSuffix: 
description: A list of enrollment options that admins can set for devices managed by Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2017
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: cf4ad6d4-423f-4826-ab8d-6eb7a7cfb559

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Enrollment options for devices managed by Intune

As an Intune admin, you can configure device enrollment to help users and enable Intune capabilities.  Intune includes the following enrollment options:

## Terms and conditions

You can require that users accept your company's terms and conditions before they can use the Company Portal to enroll their devices and access resources like company apps and email. Configuration of terms and conditions is optional. Learn more about [terms and conditions](terms-and-conditions-create.md).

## Enrollment restrictions

You can choose to restrict device enrollment by:
- Device platform
- Number of devices per user
- Block personal devices

Learn more about [enrollment restrictions](enrollment-restrictions-set.md).

## Enable Apple device enrollment

An MDM push certificate is required for iOS/iPadOS and macOS device enrollment. Learn more about [MDM push certificates](apple-mdm-push-certificate-get.md).

## Corporate identifiers

You can list international mobile equipment identifier (IMEI) numbers and serial numbers to identify corporate-owned devices. Learn more about [corporate identifiers](corporate-identifiers-add.md).
## Multi-factor authentication

You can require users to use an additional verification method, such as a phone, PIN or biometric data, when they enroll a device. Learn more about [multi-factor authentication](multi-factor-authentication.md).

## Device enrollment manager
You can make users device enrollment managers.  DEM users can enroll large numbers of mobile devices with a single user account. The device enrollment manager (DEM) account can enroll up to 1,000 devices. Learn more about [device enrollment managers](device-enrollment-manager-enroll.md).

## Device categories

You can use device categories to automatically add devices to groups based on categories that you define. Organizing devices into groups makes it easier for you to manage those devices. Learn more about [device categories](device-group-mapping.md).
