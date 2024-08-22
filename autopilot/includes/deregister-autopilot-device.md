---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

registration-overview.md
autopilot-motherboard-replacement.md

Headings are driven by article context. -->

Whenever a device permanently leaves an organization, the device should always be deregistered from Autopilot. For example, the device leaves the organization for repair or because the device is at the end of its life cycle.

Below we describe the steps an admin would go through to deregister a device from Intune and Autopilot.

### Delete from Intune

Before a device is deregistered from Autopilot, it first has to be deleted from Intune. To delete an Autopilot device from Intune:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. Under **Device name**, find the device that needs to be deleted and then select the device. If necessary, use the **Search** box.

1. In the properties screen for the device, make a note of the serial number listed under **Serial number**.

1. After making a note of the serial number of the device, select **Delete** in the toolbar at the top of the page.

1. A warning dialog box appears to confirm the deletion of the device from Intune. Select **Yes** to confirm deleting the device.

### Deregister from Autopilot using Intune

Once the device is deleted from Intune, it can then be deregistered from Autopilot. To deregister a device from Autopilot:

1. Make sure the device is deleted from Intune as described in the [Delete from Intune](#delete-from-intune) section.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens, under **Serial number**, find the device that needs to be deregistered by its serial number as determined in the [Delete from Intune](#delete-from-intune) section. If necessary, use the **Search by serial number** box.

1. Select the device by selecting the checkbox next to the device.

1. Select the extended menu icon (`…`) on the far right end of the line containing the device. A menu appears with the option **Unassign user**.

   - If the **Unassign user** option is available and not greyed out, then select it. A warning dialog box appears confirming to unassign the user from the device. Select **OK** to confirm unassigning the device from the user.
   - If the **Unassign user** option isn't available and greyed out, then move on to the next step.

1. With the device still selected, select **Delete** in the toolbar at the top of the page.

1. A warning dialog box appears to confirm the deletion of the device from Autopilot. Select **Yes** to confirm deleting the device.

1. The deregistration process might take some time. The process can be accelerated by selecting the **Sync** button in the toolbar at the top of the page.

1. Every few minutes select **Refresh** in the toolbar at the top of the page until the device is no longer present.

> [!IMPORTANT]
>
> - For Microsoft Entra join devices, no additional steps are necessary to remove the device from Intune and Autopilot. Unneeded steps include manually deleting the device from Microsoft Entra ID. Manually deleting the device from Microsoft Entra ID might cause unexpected problems, issues, and behavior. If needed, the device will be automatically removed from Microsoft Entra ID after these steps are followed.
>
> - For Microsoft Entra hybrid join devices, delete the computer object from the on-premises Active Directory Domain Services (AD DS) environment. Deleting the computer object from the on-premises AD DS ensures that the computer object isn't resynced back to Microsoft Entra ID. After the computer object is deleted from the on-premises AD DS environment, no additional steps are necessary to remove the device from Intune and Autopilot. Unneeded steps include manually deleting the device from Microsoft Entra ID. Manually deleting the device from Microsoft Entra ID might cause unexpected problems, issues, and behavior. If needed, the device will be automatically removed from Microsoft Entra ID after these steps are followed.

The above steps deregister the device from Autopilot, unenroll the device from Intune, and disjoin the device from Microsoft Entra ID. It might appear that only deregistering the device from Autopilot is needed. However, there are barriers in Intune that require all the above steps to avoid problems with lost or unrecoverable devices. To prevent the possibility of orphaned devices in the Autopilot database, Intune, or Microsoft Entra ID, it's best to complete all the steps. If a device gets into an unrecoverable state, contact the appropriate [Microsoft support alias](../autopilot-support.md) for assistance.

### Deregister from Autopilot using Microsoft 365 admin center

The device can be deregistered from Autopilot in [Microsoft 365 admin center](https://admin.microsoft.com/) if using the Microsoft 365 admin center instead of Intune. To deregister an Autopilot device from the Microsoft 365 admin center:

1. Sign into to the [Microsoft 365 admin center](https://admin.microsoft.com/).
1. Navigate to **Devices** > **Autopilot**.
1. Select the device to be deregistered and then select **Delete device**.

### Deregister from Autopilot in Microsoft Partner Center (MPC)

To deregister an Autopilot device from the Microsoft Partner Center (MPC), a Cloud Solution Partner (CSP) would:

1. Sign into the Microsoft Partner Center (MPC).
1. Navigate to **Customer** > **Devices**.
1. Select the device to be deregistered and then select **Delete device**.

   ![Screenshot of delete device](../images/devices.png)

Partners deregistering a device from Autopilot in Microsoft Partner Center (MPC) only deregisters the device from Autopilot. It doesn't perform any of the following actions:

- Unenroll the device from the mobile device management (MDM) solution, such as Intune.
- Disjoin the device from Microsoft Entra ID.

For these reasons, the OEM or CSP should work with the customer IT administrators to have the device fully removed by following the steps in the [Deregister a device](#deregister-a-device) section.

An OEM or CSP with integrated OEM Direct APIs can also deregister a device with the **AutopilotDeviceRegistration** API. Make sure the **TenantID** and **TenantDomain** fields are left blank.

> [!NOTE]
>
> If an admin registered a device via another portal other than the Microsoft Partner Center (MPC) such as Intune or the [Microsoft 365 admin center](https://admin.microsoft.com/), the device doesn't show up in Microsoft Partner Center (MPC). For a partner to register a device in the Microsoft Partner Center (MPC), the devices first needs to be deregistered using the steps outlined in the [Deregister a device](#deregister-a-device) section.
