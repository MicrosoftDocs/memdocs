---
# required metadata

title: Enroll devices using a device enrollment manager account
titleSuffix: Microsoft Intune
description: Use the device enrollment manager account to enroll devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Enroll devices in Intune by using a device enrollment manager account

You can enroll up to 1,000 mobile devices with a single Azure Active Directory account by using a device enrollment manager (DEM) account. DEM is an Intune permission that can be applied to an AAD user account and lets the user enroll up to 1,000 devices. A DEM account is useful for scenarios where devices are enrolled and prepared before handing them out to the users of the devices. By design, there's a limit of 150 Device Enrollment Manager (DEM) accounts in Microsoft Intune.

## Limitations of devices that are enrolled with a DEM account

DEM user accounts and devices that are enrolled with a DEM user account have the following limitations:

- A DEM account user must be assigned an Intune license.
- Wipe can't be done from the Company Portal. Wiping a device enrolled by a DEM user account can be done from the Intune in Azure portal.
- Only the local device appears in the Company Portal app or website.
- DEM user accounts cannot use Apple Volume Purchase Program (VPP) apps with Apple VPP user licenses because of per-user Apple ID requirements for app management.
- DEM accounts cannot be used when enrolling devices via Apple's Automated Device Enrollment (ADE).
- Devices can install VPP apps if they have Apple VPP device licenses.
- Devices are blocked for Conditional Access with the exception of Windows 10 1803+
- Every device enrolled with DEM accounts needs to be properly licensed to be managed by Intune. The license could be an Intune user license or an Intune device license.
- If you're [enrolling Android Enterprise work profile devices](android-work-profile-enroll.md) by using a DEM account, there is a limit of 10 devices that can be enrolled per account.
- [Enrolling Android Enterprise fully managed devices](android-fully-managed-enroll.md) with DEM accounts isn't supported.

## Add a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.

2. Select **Add**.

3. On the **Add User** blade, enter a user principal name for the DEM user, and select **Add**. The DEM user is added to the list of DEM users.

## Permissions for DEM

Global Administrator or Intune Service Administrator Azure AD roles are required to
- assign DEM permission to an Azure AD user account
- see all DEM users

If a user doesn't have the Global Administrator or Intune Service Administrator role assigned to them, but has read permissions enabled for the Device Enrollment Managers role assigned to them, they can see only the DEM users they've created.


## Remove device enrollment manager permissions

Removing a device enrollment manager doesn't affect enrolled devices.

**To remove a device enrollment manager**

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.
2. On the **Device enrollment managers** blade, select the DEM user, and select **Delete**.

