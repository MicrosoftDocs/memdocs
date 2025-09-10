---
title: "Intune Remote Device Action: Wipe"
description: Learn how to wipe, or factory reset, devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Wipe devices using Intune

Use the **Wipe** remote action in Intune to factory reset a device, restoring it to its default settings. This action removes all personal and organizational data, apps, and configurations. It's commonly used when a device needs to be retired, repurposed, reset for troubleshooting, or securely erased if lost or stolen.

Depending on the platform, you can customize the wipe behavior to meet your organization's needs.

::: zone pivot="macos,android"
## Before wiping a device
::: zone-end

::: zone pivot="macos"

Review the requirements for erasing macOS devices available on the [Apple Support site](https://support.apple.com/guide/deployment/dep0a819891e).

::: zone-end

::: zone pivot="android"

### Factory Reset Protection (FRP) considerations

Whether a device prompts for Google account credentials after reset depends on ownership (Android Enterprise corporate-owned work profile/fully managed/dedicated), the reset method (Settings, Recovery, or admin wipe), and whether FRP is configured. By default, Intune's admin wipe doesn't preserve FRP data.

For more information, see [Factory reset protection emails setting isn't enforced after you reset an Android Enterprise device](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced).

### Samsung devices

For Android Enterprise fully managed Samsung devices, make sure the **Factory Reset** setting under **Device Restrictions** is not set to **Block**.

If **Factory Reset** is blocked and a **Wipe** action is initiated, the device will lose contact with Intune and be unable to complete the factory reset.

### Zebra devices

On Zebra Android devices, the **Wipe** remote action is designed to remove only corporate data. It doesn't perform a factory reset.

To factory reset a Zebra Android device, use one of the following methods:

- [Use Zebra StageNow](https://techdocs.zebra.com/stagenow/5-17/profiles/wipedevice/)
- [Use OEM Config Data Wipe Configuration](https://techdocs.zebra.com/oemconfig/latest/mc2/)
::: zone-end

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Open Source Project (AOSP)
> - iOS/iPadOS (corporate-owned)
> - macOS
> - Windows

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### How to wipe a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Wipe**.

::: zone pivot="macos"
4. Provide a 6-digit number for the **Recovery PIN**. The six-digit PIN is required to reinstall the operating system on the device, if the device isn't equipped with T2 security chip enabled (that is, the model year of the device is 2018 and earlier, or the device is running macOS 10.14 or earlier). Be sure to make a note of this PIN and give it to the device owner as it won't be visible after the wipe action completes.

5. Select an option from **Obliteration Behavior**, which is used to define the fallback for devices when Erase All Contents and Settings (EACS) fails. The following options can be configured:

    - **Default**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Do not obliterate**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and doesn't attempt to erase itself. If EACS preflight succeeds but EACS fails, then the device doesn't attempt to erase itself.
    - **Obliterate with warning**: If Erase All Content and Settings (EACS) preflight fails, the device responds with a Success status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Always obliterate**: The system doesn't attempt Erase All Content and Settings (EACS). T2 and later devices always obliterate.
6. Select **Wipe** to erase the device.
::: zone-end

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

::: zone pivot="windows"

4. **Wipe device, but keep enrollment state and associated user account** option. If this option is selected, the following user account details are retained:

    |Retained during a wipe |Not retained|
    | -------------|------------|
    |User accounts associated with the device|User files|
    |Machine state \(domain join, Microsoft Entra joined)| User-installed apps \(store and Win32 apps)|
    |Mobile device management (MDM) enrollment|Non-default device settings|
    |OEM-installed apps \(store and Win32 apps)||
    |User profile||
    |User data outside of the user profile||
    |User autologon||

    |Wipe action|**Wipe device, but keep enrollment state and associated user account**|Removed from Intune management|Description|
    |:-------------:|:------------:|:------------:|------------|
    |**Wipe**| Not checked | Yes | Wipes all user accounts, data, MDM policies, and settings. Resets the operating system to its default state and settings.|
    |**Wipe**| Checked | No | Wipes all MDM Policies. Keeps user accounts and data. Resets user settings back to default. Resets the operating system to its default state and settings.|

5. The **Wipe device, and continue to wipe even if device loses power** option makes sure that the wipe action can't be circumvented by turning off the device. This option keeps trying to reset the device until successful. In some configurations, this action can leave the device [unable to reboot](/troubleshoot/mem/intune/troubleshoot-device-actions#wipe-action).

  - **Wipe device, and continue to wipe even if device loses power**: When selected, it ensures the wipe continues even if the device loses power during the process. This helps prevent users from interrupting the wipe by turning off the device, making it useful in high-security scenarios where guaranteed data removal is required.

      > [!IMPORTANT]
      > If you select this option, be aware that it might prevent some devices from starting up again. The persistent wipe process can interfere with boot recovery or firmware-level protections, potentially leaving the device in an unrecoverable state. Use this option only on corporate-owned devices where full data destruction is necessary and recovery procedures are in place.

6. To confirm the wipe, select **Yes**.


dowipe:
A remote reset is equivalent to running Reset this PC > Remove everything from the Settings app, with Clean Data set to No and Delete Files set to Yes. If a doWipe reset is started and then interrupted, the PC will attempt to roll-back to the pre-reset state. If the PC can't be rolled-back, the recovery environment will take no additional actions and the PC could be in an unusable state and Windows will have to be reinstalled.

doWipeCloudPersistProvisionedData: Exec on this node will back up provisioning data to a persistent location and perform a cloud-based remote wipe on the device. The information that was backed up will be restored and applied to the device when it resumes. The return status code shows whether the device accepted the Exec command.


doWipeCloudPersistUserData: Exec on this node will perform a cloud-based remote reset on the device and persist user accounts and data. The return status code shows whether the device accepted the Exec command.

doWipePersistProvisionedData: Exec on this node will back up provisioning data to a persistent location and perform a remote wipe on the device. The information that was backed up will be restored and applied to the device when it resumes. The return status code shows whether the device accepted the Exec command. When used with OMA Client Provisioning, a dummy value of "1" should be included for this element. The information that was backed up will be restored and applied to the device when it resumes. The return status code shows whether the device accepted the Exec command. Provisioning packages are persisted in %SystemDrive%\ProgramData\Microsoft\Provisioning directory.

doWipeProtected: Exec on this node will perform a remote wipe on the device and fully clean the internal drive. In some device configurations, this command may leave the device unable to boot. The return status code shows whether the device accepted the Exec command. The doWipeProtected is functionally similar to doWipe. But unlike doWipe, which can be easily circumvented by simply power cycling the device, doWipeProtected will keep trying to reset the device until it's done.
Note: Because doWipeProtected will clean the partitions in case of failure or interruption, use doWipeProtected in lost/stolen device scenarios.

::: zone-end
::: zone pivot="ios"
1. For iOS/iPadOS eSIM devices, the cellular data plan is preserved by default when you wipe a device. If you want to remove the data plan from the device when you wipe the device, select the **Also remove the devices data plan...** option.
::: zone-end

## User experience

::: zone pivot="macos"
When you use **Wipe**, the device is also removed from Intune management and no warning is given to the end user once a wipe is initiated.
::: zone-end

::: zone pivot="ios"
The behavior for **Wipe** on iOS devices is that it restores the device to factory defaults and removes the management profile, including any configuration profiles that were installed.
::: zone-end


[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

::: zone pivot="windows"

[!INCLUDE [remove-device-from-autopilot](includes/remove-device-from-autopilot.md)]

::: zone-end

[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]

## Reference links

- Configuration service provider (CSP) used to initiate the remote action: [RemoteWipe CSP][CSP-1]
- Microsoft Graph API: [wipe action][GRAPH-1]

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
[CSP-1]: /windows/client-management/mdm/remotewipe-csp