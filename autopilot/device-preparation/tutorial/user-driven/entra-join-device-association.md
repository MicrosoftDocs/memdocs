---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 7 - Associate devices
description: Associate devices to your tenant as an alternative to corporate identifiers, including exporting device information, pre-associating in Intune, completing association, and reviewing associated devices.
ms.date: 08/07/2026
ms.topic: tutorial
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Associate devices

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create an assigned device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7, option 1: [Add Windows corporate identifier to device](entra-join-corporate-identifier.md)

> [!div class="checklist"]
>
> - **Step 7, option 2: Associate devices**

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

Device association is an **optional** feature of Windows Autopilot device preparation and an alternative to [adding corporate identifiers](entra-join-corporate-identifier.md). It binds a device to your tenant before enrollment, and it unlocks additional device preparation policy settings—such as OOBE customization and device naming—that are only available to associated devices.

> [!IMPORTANT]
>
> If you use Intune enrollment restrictions to block personal device enrollments, you must configure **either** corporate identifiers **or** device association for each device before deployment. You don't need both. If a device is associated, you don't need to upload a corporate identifier for it—associated devices are automatically marked as corporate-owned.

To associate devices, complete the following tasks in this step.

## Export device information from OOBE

> [!NOTE]
>
> We recommend using a USB drive formatted with the NTFS file system.

1. Turn on the device and boot into OOBE. Stop at the region selection page—don't complete OOBE setup.
1. Press the **Windows** key five times quickly. The Autopilot menu opens.

   > [!NOTE]
   >
   > The OOBE Autopilot menu includes two options: **Scan QR code** and **Export device information**. Currently, Intune supports uploading only the CSV file created by option 2, **Export device information**. Option 1, **Scan QR code**, can be used with a custom app that calls Microsoft Graph to pre-associate the device.

1. From the Autopilot menu, select **Export device information**.
1. Insert a USB drive into the device.
1. In the Autopilot menu, select **Export device information**. The device information file is saved to the USB drive.
1. Remove the USB drive and copy the exported CSV file to a computer that has access to the Microsoft Intune admin center.

## Export device information from an existing device

For existing devices that are already past the out-of-box experience (OOBE), you can't open the Autopilot menu. Instead, collect the device's Autopilot diagnostic logs by using one of the following methods, and then retrieve the DeviceLink CSV from the collected diagnostics:

- **On the device, from Settings:** Go to **Settings** > **Accounts** > **Access work or school**, and under **Related settings**, select **Export your management logs** > **Export**. Follow the displayed path to retrieve the exported diagnostics.
- **On the device, from a command prompt:** From an elevated command prompt, run `MdmDiagnosticsTool.exe -area Autopilot -cab C:\Diagnostics\Autopilot.cab`.
- **Remotely from Intune:** In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **All devices**, select the device, and then select **Collect diagnostics**. When the upload finishes, download the diagnostics from the device's **Device diagnostics** view.

After you collect the diagnostics, locate the DeviceLink CSV file and copy it to a computer that has access to the Microsoft Intune admin center.

## Pre-associate the device in Intune

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment** > **Device association** > **Devices**.
1. Select **Add**.
1. On the **Import CSV** page, select **Browse** and upload the CSV file exported in the previous task.
1. Select **Next**.
1. On the **Assign device preparation policy** page, optionally select the device preparation policy you created in [Step 6: Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md) to assign to this device. Assigning a policy here ensures the device gets the correct policy without relying on a user-group assignment.

   > [!NOTE]
   >
   > If you don't assign a policy here, the device uses the device preparation policy assigned to the user who signs in during enrollment. If that user has no assigned policy, no device preparation policy is applied to the device.

1. Select **Next**, review the import summary, and then select **Add**.

The device appears in the **Device association** list with an **Association state** of **Pre-associated**.

> [!NOTE]
>
> At this time, only one device per CSV file is allowed. Upload a separate CSV file for each device.

## Complete device association

Device association happens automatically for pre-associated devices when the device connects to a network in OOBE. Alternatively, association can be completed on the device in OOBE.

To trigger association manually on the device in OOBE:

1. On the device, return to the Autopilot menu and select **Next** after pre-associating the device.
1. The device contacts the Windows Autopilot service and finds the pre-association record. If the device matches, the OOBE screen shows **Association complete**.

## Review associated devices

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment** > **Device association** > **Devices**.

The list shows all pre-associated and associated devices in your tenant. Use the **Search** box to find devices by serial number or device name, and use the column filters to narrow results by association state, policy, manufacturer, or model. Each device shows the following association states:

| State | Description |
|---|---|
| **Pre-associated** | The device was added via CSV and is waiting to complete association in OOBE. |
| **Associated** | The device completed the OOBE association step. It's ready for enrollment. |
| **Pending removal** | A remove-association request was submitted and is being processed. |

## Next steps

Because associated devices are automatically treated as corporate-owned, you don't need to add [Windows corporate identifiers](entra-join-corporate-identifier.md) for them. Once devices are associated, proceed with deploying the device.

## Related content

- [Overview of Windows Autopilot device association](../../device-association/overview.md)
- [Device association lifecycle management](../../device-association/lifecycle-management.md)
