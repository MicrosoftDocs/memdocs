---
# required metadata
title: Onboard NXT devices into your organization's environment
titleSuffix:
description: Learn about options for onboarding NXT devices into your organization's environment.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Onboard NXT devices to your organization's environment

After [setting up your organization's environment to support NXT devices](deployment-overview.md), you can decide how you want to onboard the devices to your organization's environment.

NXT devices are designed to be shared. The first time a NXT boots it loads the Out of Box Experience (OOBE) to guide a user through a simplified process that joins the device to Entra ID and enrolls into Intune management. After this process completes, the device shows only the sign-in screen for any user to authenticate and connect to their own Cloud PC.

With the right permissions, a standard user can onboard NXT devices using the OOBE process. Alternatively, you can choose to have admins onboard NXT devices and complete the onboarding before delivering the devices to users.  You can have admins onboard some devices and users onboard others. To help you decide, consider the following recommendations:

| Considerations | Admin driven onboarding | User driven onboarding |
| --- | --- | --- |
| The device will be used by different users. | Yes |  |
| The device will be used by one user. |  | Yes |
| Users aren't allowed to join or register devices.  | Yes |  |
| Devices are shipped directly to users. |  | Yes |

## Admin driven onboarding

When onboarding devices shared by multiple users, you can use an account that is designated as a [Device Enrollment Manager](/mem/intune/enrollment/device-enrollment-manager-enroll) (DEM). This account doesn't need admin privileges in the tenant but is allowed to enroll up to 1000 devices in Intune.

A Device Enrollment Manager is still subject to the limit on the number of devices that can be joined to Entra ID. For more information, see [Join NXT to Microosft Entra](join-microsoft-entra.md). Consider increasing the **Maximum number of devices per user** to a value you expect a DEM to enroll.

Using this DEM account on onboard NXT devices:

- Enrolls the NXT devices in a shared device mode.
- Bypasses Intune enrollment restrictions for platforms and device limits that may be in place.
- Doesn't require any changes to allow personal Windows devices.
- Doesn't designate a primary user of the device. With no primary user, the NXT doesn't appear in a user's list of devices in Intune, Entra, Company Portal, or other places.

To set up a DEM account to onboard NXT devices, follow these steps:

1. Create an account to use for NXT device onboarding.
2. Assign the required licensing (Microsoft Entra Premium, Intune, Windows, and so on ).
3. Make sure the user has permissions to join devices to Microsoft Entra ID.
4. Add the user to the list of Device Enrollment Managers.
5. To validate connectivity, provision a Cloud PC for this DEM account.

To onboard NXT devices using the DEM account, follow these steps:

1. Power on the NXT.
2. Sign in with the DEM account. Follow all the authentication steps to join the device to Microsoft Entra and enroll in Intune.
3. After you're connected to the Cloud PC, disconnect and then restart the NXT to install any available updates.
4. Shut down the NXT.
5. The NXT is now ready for any users in the organization to use with their own Cloud PC.

## User driven onboarding

Rather than having an administrative person onboard each NXT, users can complete the OOBE to join them to Microsoft Entra and enroll them in Intune. Using this method:

- The user is designated as the primary user of the device.
- The NXT appears in their list of devices (for example, in the Company Portal).
- Any user from the same organization can use the device to connect to their own Cloud PC.

To use this onboarding method, make sure each user:

- Has the required licensing (Microsoft Entra Premium, Intune, Windows, and so on).
- Has permissions to join devices to Microsoft Entra IP.
- Doesn't exceed the maximum number of devices that can be joined.
- Isn't blocked from Intune enrollment by any restrictions or device limits.
- Has a Cloud PC provisioned and consented to single sign-on.

To onboard NXT devices using this method, follow these steps:

1. Deliver the NXT to the user.
2. Power on the NXT.
3. Sign in with the user's account. Follow all authentication steps to join the device to Microsoft Entra and enrolls it in Intune.
4. After the user connects to their Cloud PC, disconnect and then restart the NXT to install any available updates.
5. Shut down the NXT.
6. The NXT is now ready for any users in the organization to use with their own Cloud PC.

## Next steps

For more information about managing devices in Microsoft Intune, see the [Microsoft Intune documentation](/mem/intune/fundamentals/what-is-intune).
