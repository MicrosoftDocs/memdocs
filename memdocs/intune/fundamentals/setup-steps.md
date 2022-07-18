---
# required metadata

title: Set up Microsoft Intune
description: Requirements and prerequisites for starting to use your Intune subscription
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/14/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: 
  - M365-identity-device-management
  - highpri
---


# Set up Intune

These set-up steps help you enable mobile device management (MDM) by using Intune. Devices must be managed before you can give users access to company resources or manage settings on those devices.

Some steps, such as setting up an Intune subscription and setting the MDM authority, are required for most scenarios. Other steps, such as configuring a custom domain or adding apps, are optional depending upon your company's needs.

If you're currently using Microsoft Endpoint Configuration Manager to manage computers and servers, you can [cloud-attach Configuration Manager with co-management](/configmgr/comanage/overview).

>[!TIP]
>If you purchase at least 150 licenses for Intune in an eligible plan, you can use the *FastTrack Center Benefit*. With this service, Microsoft specialists work with you to get your environment ready for Intune. See [FastTrack Center Benefit for Enterprise Mobility + Security (EMS)](/enterprise-mobility-security/Solutions/enterprise-mobility-fasttrack-program).

| Steps | Status  |
|---|---|
|   1   | [Supported configurations](supported-devices-browsers.md) - Need-to-know info before you start. This includes supported configurations and networking requirements.|
|   2   |  [Sign in to Intune](account-sign-up.md) - Sign in to your trial subscription or create a new Intune subscription. |
|   3   | [Configure domain name](custom-domain-name-configure.md) - Set DNS registration to connect your company's domain name with Intune. This gives users a familiar domain when connecting to Intune and using resources. |
|   4   | [Add users](users-add.md) and [groups](groups-add.md) - Add users and groups, or connect Active Directory to sync with Intune. Required unless your devices are "userless" kiosk devices, for example. Groups are used to assign apps, settings, and other resources.|
|   5   | [Assign licenses](licenses-assign.md) - Give users permission to use Intune. Each user or userless device requires an Intune license to access the service. |
|   6   | [Set the MDM authority](mdm-authority-set.md) - Use user and device groups to simplify management tasks. Groups are used to assign apps, settings, and other resources. |
|   7   | [Add apps](../apps/apps-add.md) - Apps can be assigned to groups and automatically or optionally installed. |
|   8   | [Configure devices](../configuration/device-profiles.md) - Set up profiles that manage device settings. Device profiles can preconfigure settings for email, VPN, Wi-Fi, and device features. They can also restrict devices to help protect both devices and data. |
|   9   |  [Customize Company Portal](../apps/company-portal-app.md) - Customize the Intune Company Portal that users use to enroll devices and install apps. These settings appear in both the Company Portal app and the Intune Company Portal website.       |
|  10   | [Enable device enrollment](../enrollment/device-enrollment.md) - Enable Intune management of iOS/iPadOS, Windows, Android, and Mac devices by setting the MDM authority and enabling specific platforms. |
|  11   |  [Configure app policies](../apps/app-protection-policy.md) - Supply specific settings based on app protection policies in Microsoft Intune. |
