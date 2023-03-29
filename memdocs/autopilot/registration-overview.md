---
title: Windows Autopilot registration overview
description: Overview of Windows Autopilot device registration.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.topic: how-to
ms.collection: 
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
---

# Windows Autopilot registration overview

**Applies to:**

- Windows 11
- Windows 10
- Windows Holographic, version 2004

Before deploying a device using Windows Autopilot, the device must be registered with the Windows Autopilot deployment service. 

Successful registration requires that two processes are complete:

1. The device's unique [hardware identity](#device-identification) (known as a hardware hash) is captured and uploaded to the Autopilot service.
2. The device is associated to an Azure tenant ID.

Ideally, both of these processes are performed by the OEM, reseller, or distributor from which the devices were purchased. An OEM or other device provider uses the [registration authorization](registration-auth.md) process to perform device registration on your behalf. 

Registration can also be performed within your organization by collecting the hardware identity from new or existing devices and [uploading it manually](manual-registration.md). If devices meet certain requirements, they can also be configured for [automatic registration](automatic-registration.md) with Windows Autopilot. For more information about the ways in which devices can be registered with Windows Autopilot, see the following overview topics:

- [OEM registration](oem-registration.md)
- [Reseller, distributor, or partner registration](partner-registration.md)
- [Automatic registration](automatic-registration.md)
- [Manual registration](manual-registration.md)

When you register an Autopilot device, it automatically creates an Azure AD object. The Autopilot deployment process needs this object to identify the device before the user signs in. If you delete this object, the device can fail to enroll through Autopilot. 

> [!NOTE]
> Don't register to Autopilot the following types of devices:
>
> - [Azure AD registered](/azure/active-directory/devices/concept-azure-ad-register), also known as "workplace joined"
> - [Intune MDM-only enrollment](/mem/intune/enrollment/windows-enrollment-methods#user-self-enrollment-in-intune)
>
> These options are intended for users to join personally-owned devices to their organization's network.

Once a device is registered in Autopilot if a profile is not assigned, it will receive the default Autopilot profile. If you do not want a device to go through Autopilot, you must remove the Autopilot registration. 

## Terms

The following terms are used to refer to various steps in the registration process:

| Term | Definition |
| --- | --- |
| device registration | Device registration happens when a device's hardware hash is associated with the Windows Autopilot service. This process can be automated for new enterprise devices manufactured by OEMs that are Windows Autopilot partners. |
| add devices | Adding a device is the process of registering a device with the Windows Autopilot service, (if it is not already registered) **and associating it to a tenant ID**. |
| import devices | Importing devices is the process of uploading a comma-separated-values (CSV) file that contains device information such as the model and serial number in order to manually add devices. |
| enroll devices | Enrolling a device is the process of adding devices to Intune. |

## Device identification

To identify a device with Windows Autopilot, the device's unique hardware hash must be captured and uploaded to the service. As previously mentioned, this step is ideally done by the hardware vendor (OEM, reseller, or distributor) automatically associating the device with an organization. It's also possible to do identify a device with a [harvesting process](add-devices.md) that collects the device's hardware hash from within a running Windows installation.

The hardware hash contains details about the device, such as:

- manufacturer
- model
- device serial number
- hard drive serial number
- details about when the ID was generated
- many other attributes that can be used to uniquely identify the device

The hardware hash changes each time it's generated because it includes details about when it was generated. When the Windows Autopilot deployment service attempts to match a device, it considers changes like that. It also considers large changes such as a new hard drive, and is still able to match successfully. But large changes to the hardware, such as a motherboard replacement, wouldn't match, so a new hash would need to be generated and uploaded.

For more information about device IDs, see the following topics:

- [Windows Autopilot device guidelines](autopilot-device-guidelines.md)
- [Add devices to a customer account](/partner-center/autopilot)

## Windows Autopilot devices

Devices that have been registered with the Windows Autopilot service are displayed in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Enroll devices** > **Windows enrollment** > **Windows Autopilot Deployment Program** > **Devices**:

![Autopilot devices](images/ap-devices.png)

> [!NOTE]
> Devices that are listed in Intune under **Devices** > **Windows** > **Windows devices** are not the same as Windows Autopilot devices (**Devices** > **Enroll devices** > **Windows enrollment** > **Windows Autopilot Deployment Program** > **Devices**). Windows Autopilot devices are added to the list of **Windows devices** when both of the following are complete:

> - The Autopilot registration process is successful.
> - A [licensed](licensing-requirements.md) user has signed in on the device.

## Deregister a device from Autopilot

Whenever a device permanently leaves your organization, whether it's for a repair or the end of the device life cycle, the device should always be deregistered from Autopilot.

If the IT Admin registered the device, they likely did so via Intune or possibly the Microsoft Store for Business. If so, they should deregister the device from Intune or the Microsoft Store for Business because devices registered in Intune won't show up in Microsoft Partner Center (MPC).
Below we describe the steps an IT Admin would go through to deregister a device from Intune.

## Deregister from Intune

To deregister an Autopilot device from Intune, an IT Admin would:

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Navigate to **Groups** > **All groups**

3. Remove the device from its group

4. Navigate to **Devices** > **All devices**

5. Select the checkbox next to the device you want to delete, then select the **Delete** button on the top menu

6. Navigate to **Devices** > **Azure AD devices**

7. Select the checkbox next to the device you want to delete, then select the **Delete** button along the top menu

8. Navigate to **Device enrollment** > **Windows enrollment** > **Devices**

9. Select the checkbox next to the device you want to deregister

10. Select the extended menu icon (`…`) on the far right end of the line containing the device you want to deregister to expose an additional menu with the option to **unassign user**

11. Select **Unassign user** if the device was previously assigned to a user. If not, this option will be grayed-out and can be ignored.

12. With the unassigned device still selected, select the **Delete** button along the top menu to remove this device

These steps deregister the device from Autopilot, unenroll the device from Intune, and disjoin the device from Azure AD. It may appear that only deregistering the device from Autopilot is needed. However, there are barriers in Intune that require all the above steps to avoid problems with lost or unrecoverable devices. To prevent the possibility of orphaned devices in the Autopilot database, Intune, or Azure AD, it's best to complete all the steps.

The deregistration process will take about 15 minutes. You can accelerate the process by selecting the **Sync** button, then **Refresh** the display until the device is no longer present.

## Deregister from Microsoft Admin Center

To deregister an Autopilot device from the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431):

1. Sign into to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Devices** > **Autopilot**
3. Select the device to be deregistered and then select the **Delete device** button

Deregistering a device from Autopilot in Microsoft Partner Center (MPC) only deregisters the device from Autopilot. It doesn't perform any of the following actions:

- Unenroll the device from the MDM (Intune)
- Disjoin the device from Azure AD

## Related topics

[Register devices manually](add-devices.md)
