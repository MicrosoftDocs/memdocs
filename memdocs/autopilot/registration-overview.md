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

## Deregister a device

Whenever a device permanently leaves an organization, whether it's for a repair or the end of the device life cycle, the device should always be deregistered from Autopilot.

If the IT Admin registered the device, they likely did so via Intune. If so, they should deregister the device from Intune because devices registered in Intune won't show up in Microsoft Partner Center (MPC).

Below we describe the steps an IT Admin would go through to deregister a device from Intune and Autopilot.

### Deregister from Intune

To deregister an Autopilot device from Intune:

#### Make a note of any Assigned and Direct groups the device is a member of

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. Under **Device name**, find the device that needs to be deregistered and then select the device. If necessary, use the **Search** box.

1. In the properties screen for the device, under **Monitor**, select **Group membership**.

1. Make a note of all of the groups the device is a member of where **Membership type** is **Assigned** and **Direct or Transitive** is **Direct**. If the device is not a member of any groups that are both **Assigned** and **Direct**, then go to the [Delete the device from Intune](#delete-the-device-from-intune) section.

#### Remove the device from any Assigned and Direct groups it's a member of

1. In the **Home** screen, select **Groups** in the left hand pane.

1. In the **Groups | All groups** screen, make sure **All groups** is selected.

1. Under **Name**, locate and select the **Assigned** and **Direct** groups that the device is a member of as determined in the [Make a note of the device's group membership](#make-a-note-of-any-assigned-and-direct-groups-the-device-is-a-member-of) section. If necessary, use the **Search** box.

1. After selecting a group, in the group's property page, under **Manage**, select **Members**.

1. Under **Name**, locate the device in the group. If necessary, use the **Search by name** box.

1. Select the device by selecting the checkbox next to the device.

1. In the toolbar at the top of the page, select **Remove**.

1. A warning dialog box will appear confirming the removal of the device from the group. Select **Yes** to confirm the removal of the device from the group.

#### Delete the device from Intune

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. Under **Device name**, find the device that needs to be deregistered and then select the device. If necessary, use the **Search** box.

1. In the properties screen for the device, make a note of the serial number listed under **Serial number**.

1. After making a note of the serial number of the device, select **Delete** in the toolbar at the top of the page.

1. A warning dialog box will appear confirming the deletion of the device from Intune. Select **Yes** to confirm deleting the device.

## Deregister a device from Autopilot

1. Make sure the device has been deregistered from Intune as described in the [Deregister from Intune](#deregister-from-intune) section.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows enrollment** screen, select **Windows enrollment**

1. Under **Windows Autopilot Deployment Program**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens, under **Serial number**, find the device that needs to be deregistered by its serial number as determined in the [Delete the device from Intune](#delete-the-device-from-intune) section. If necessary, use the **Search by serial number** box.

1. Select the device by selecting the checkbox next to the device.

1. Select the extended menu icon (`…`) on the far right end of the line containing the device. An menu will appear with the option **Unassign user**.

   - If the **Unassign user** option is available and not greyed out, then select it. A warning dialog box will appear confirming to unassign the user from the device. Select **OK** to confirm unassigning the device from the user.
   - If the **Unassign user** option is not available and greyed out, then move on to the next step.

1. With the device still selected, select **Delete** in the toolbar at the top of the page.

1. A warning dialog box will appear confirming the deletion of the device from Autopilot. Select **Yes** to confirm deleting the device.

1. The deregistration process may take some time. The process can be accelerated by selecting the **Sync** button in the toolbar at the top of the page.

1. Every few minutes select **Refresh** in the toolbar at the top of the page until the device is no longer present.

> [!IMPORTANT]
>
> No additional steps are necessary to remove the device from Intune and Autopilot. Unneeded steps includes manually deleting the device from Azure AD. Manually deleting the device from Azure AD may cause unexpected problems, issues, and behavior. If needed, the device will be automatically removed from Azure AD after the steps above are followed.

The steps above deregister the device from Autopilot, unenroll the device from Intune, and disjoin the device from Azure AD. It may appear that only deregistering the device from Autopilot is needed. However, there are barriers in Intune that require all the above steps to avoid problems with lost or unrecoverable devices. To prevent the possibility of orphaned devices in the Autopilot database, Intune, or Azure AD, it's best to complete all the steps.

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
