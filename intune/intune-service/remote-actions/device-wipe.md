---
title: "Intune Remote Device Action: Wipe"
description: Learn how to wipe devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Wipe devices with Intune

::: zone pivot="macos,ios,windows,android"
::: zone-end

<!--By using the **Retire** or **Wipe** actions, you can remove devices from Intune that are no longer needed, being repurposed, or missing. Users can also issue a remote command from the Intune Company Portal to devices that are enrolled in Intune.
MDM policies will be reapplied the next time the device connects to Intune.

A wipe is useful for resetting a device before you give the device to a new user, or when the device has been lost or stolen. Be careful about selecting **Wipe**. Data on the device can't be recovered. The method that "Wipe" uses to remove data is simple file deletion, and the drive is BitLocker decrypted as part of this process.
-->

The **Wipe** device action restores a device to its factory default settings.

::: zone pivot="macos,android"
## Before you start
::: zone-end

::: zone pivot="macos"

For devices running macOS 12.0.1 and later, review the requirements for erasing devices available on the [Apple Support site](https://support.apple.com/guide/deployment/dep0a819891e).

For devices running a version of macOS earlier than 12.0.1, macOS must be reinstalled. Steps covering how to reinstall macOS are available on the [Apple Support site](https://support.apple.com/HT204904).

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
> To execute these remote actions, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### How to wipe a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Wipe**.

::: zone pivot="macos"
4. Provide a 6-digit number for the **Recovery PIN**. The six-digit PIN is required to reinstall the operating system on the device, if the device isn't equipped with T2 security chip enabled (that is, the model year of the device is 2018 and earlier, or the device is running macOS 10.14 or earlier). Be sure to make a note of this PIN and give it to the device owner as it won't be visible after the wipe action completes.

    :::image type="content" source="images/obliteration-behavior.png" alt-text="Screen shot that shows where to provide a pin and select an option for obliteration behavior." lightbox="images/obliteration-behavior.png":::

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
::: zone-end
::: zone pivot="ios"
1. For iOS/iPadOS eSIM devices, the cellular data plan is preserved by default when you wipe a device. If you want to remove the data plan from the device when you wipe the device, select the **Also remove the devices data plan...** option.
::: zone-end

## Wipe all data from a macOS device

Intune gives you the ability to use the **Wipe** remote device action to wipe data from macOS devices, including the operating system.

> [!IMPORTANT]
> When you use **Wipe**, the device is also removed from Intune management and no warning is given to the end user once a wipe is initiated.

> [!NOTE]
> The behavior for **Wipe** on iOS devices is that it restores the device to factory defaults and removes the management profile, including any configuration profiles that were installed.

## Reference links

- Microsoft Graph API: [wipe action][GRAPH-1]



<!--
Initiates a wipe of the device. Also called a factory reset. The Factory reset action restores a device to its factory default settings. The user data is kept or wiped depending on whether or not you choose the Retain enrollment state and user account checkbox.


Are you sure you want to wipe CLIENT
Factory reset returns the device to its default settings. This removes all personal and company data and settings from this device. You can choose whether to keep the device enrolled and the user account associated with this device. You cannot revert this action.

Wipe device, but keep enrollment state and associated user account



{
  "keepEnrollmentData": true,
  "keepUserData": true,
  "macOsUnlockCode": "Mac Os Unlock Code value",
  "obliterationBehavior": "doNotObliterate",
  "persistEsimDataPlan": true,
}
-->

## Next steps

::: zone pivot="windows"
The Wipe action doesn't remove the Windows Autopilot registration from the device. To remove the Windows Autopilot registration from the device, see [Deregister from Windows Autopilot using Intune](/autopilot/registration-overview#deregister-from-autopilot-using-intune)
::: zone-end

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
