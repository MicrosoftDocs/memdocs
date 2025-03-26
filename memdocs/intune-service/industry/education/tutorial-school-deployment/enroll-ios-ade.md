---
title: Education device enrollment with Automated Device Enrollment and Intune
description: Learn how to automatically enroll devices through Apple School Manager with Automated Device Enrollment during Setup Assistant on iOS/iPadOS devices.
ms.date: 5/2/2024
ms.topic: tutorial
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
ms.service: microsoft-intune
ms.subservice: education
---

# Enroll devices with Automated Device Enrollment

Automated Device Enrollment through Apple School Manager is designed to simplify all parts of iOS devices lifecycle, from initial deployment through end of life. Using cloud-based services, Automated Device Enrollment can reduce the overall costs for deploying, managing, and retiring devices.

From the user's perspective, it only takes a few simple operations to make their device ready to use. The only interaction required from the end user is to set their language and regional settings, connect to a network, and depending on the profile type - verify their credentials. Everything beyond that is automated.

There are two types of enrollment:

- **User affinity**. This enrollment type is designed for devices that have only one user. In this scenario, the user is prompted for credentials during enrollment.
- **No user affinity**. This enrollment type is designed for shared devices and is common in lower grades. In this scenario, no credentials are required to enroll the device. For iPad devices, a configuration called Shared iPad can be applied that allows users to log in with their Managed Apple ID or use a temporary session.

For more information on configuring Automated Device Enrollment, see:

## [Intune](#tab/intune)

[Set up automated device enrollment in Intune](/mem/intune-service/enrollment/device-enrollment-program-enroll-ios).

## [Intune For Education](#tab/intune-for-education)

[Set up iOS device management](/intune-education/setup-ios-device-management)

---

## Next steps

With the devices managed by Intune, you can use Intune to maintain them and report on their status.

> [!div class="nextstepaction"]
> [Next: Manage devices >](manage-overview.md)
