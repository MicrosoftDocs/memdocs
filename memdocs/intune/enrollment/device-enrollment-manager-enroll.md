---
# required metadata

title: Enroll devices using a device enrollment manager account
titleSuffix: Microsoft Intune
description: Use the device enrollment manager account to enroll devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/02/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver, shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Enroll devices in Intune by using a device enrollment manager account

You can enroll up to 1,000 devices in total with a single Azure Active Directory account by using a device enrollment manager (DEM) account. DEM is an Intune permission that can be applied to an Azure AD user account and lets the user enroll up to 1,000 devices. A DEM account is useful for scenarios where devices are enrolled and prepared before handing them out to the users of the devices. By design, there's a limit of 150 active DEM accounts in Microsoft Intune.

## Limitations of devices that are enrolled with a DEM account

DEM user accounts and devices that are enrolled with a DEM user account have the following limitations:

- A DEM account user must be assigned an Intune license.
- Wipe can't be done from the Company Portal. Wiping a device enrolled by a DEM user account can be done from the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
- Only the local device appears in the Company Portal app or website.
- DEM user accounts cannot use Apple Volume Purchase Program (VPP) apps with Apple VPP user licenses because of per-user Apple ID requirements for app management.
- Microsoft Intune does not support the use of DEM accounts when enrolling devices via Apple Automated Device Enrollment (ADE).  
- DEM accounts cannot support conditional access because conditional access is intended for per-user scenarios. 
- Devices can install VPP apps if they have Apple VPP device licenses.
- Every device enrolled with DEM accounts needs to be properly licensed to be managed by Intune. The license could be an Intune user license or an Intune device license.
- If you're [enrolling Android Enterprise personally-owned devices with work profile](android-work-profile-enroll.md) using a DEM account, there is a limit of 10 devices that can be enrolled per account.
- [Enrolling Android Enterprise fully managed devices](android-fully-managed-enroll.md) with DEM accounts isn't supported.
- [Enrolling Android Enterprise corporate owned work profile devices](android-corporate-owned-work-profile-enroll.md) with DEM accounts isn't supported.
- Applying an Azure AD device restriction to a DEM account will prevent you from reaching the 1,000 device limit that the DEM account can enroll.

>[!NOTE]
>For additional details regarding enrollment capabilities for Windows and the use of DEM accounts, please refer [Intune enrollment method capabilities for Windows devices](./enrollment-method-capab.md).

## Enrollment methods supported by DEM accounts

You can use the following methods to enroll devices using DEM accounts:

- [Windows Autopilot](../../autopilot/enrollment-autopilot.md)
- [Windows devices bulk enrollment](windows-bulk-enroll.md)
- DEM initiated via Company Portal
- DEM initiated via Azure AD join

## Add a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.

2. Select **Add**.

3. On the **Add User** blade, enter a user principal name for the DEM user, and select **Add**. The DEM user is added to the list of DEM users.

## Permissions required to create DEM accounts

Global Administrator or Intune Service Administrator Azure AD roles are required to

- Assign DEM permission to an Azure AD user account
- See all DEM users

If a user doesn't have the Global Administrator or Intune Service Administrator role assigned to them, but has read permissions enabled for the Device Enrollment Managers role assigned to them, they can see only the DEM users they've created.

## Remove device enrollment manager permissions

Removing a device enrollment manager doesn't affect enrolled devices.

### To remove a device enrollment manager

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enroll devices** > **Device enrollment managers**.
2. On the **Device enrollment managers** blade, select the DEM user, and select **Delete**.
