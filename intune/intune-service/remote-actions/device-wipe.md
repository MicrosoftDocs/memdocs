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

zone_pivot_groups: c5fbc3ee-cfe5-494a-b441-d95cbed3128c
---

# Wipe devices using Intune

Use the **Wipe** remote action in Intune to factory reset a device, restoring it to its default settings. This action removes all personal and organizational data, apps, and configurations. It's commonly used when a device needs to be retired, repurposed, reset for troubleshooting, or securely erased if lost or stolen.

Depending on the platform, you can customize the wipe behavior to meet your organization's needs.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Open Source Project (AOSP)
> - ChromeOS
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

::: zone pivot="macos,android"
## Before wiping a device
::: zone-end

::: zone pivot="macos"

Review the requirements for erasing macOS devices available on the [Apple Support site](https://support.apple.com/guide/deployment/dep0a819891e).

::: zone-end

::: zone pivot="android"

### Factory Reset Protection (FRP) considerations

Whether a device requires Google account credentials after reset depends on ownership (Android Enterprise corporate-owned work profile/fully managed/dedicated), the reset method (Settings, Recovery, or admin wipe), and whether FRP is configured. By default, Intune's admin wipe doesn't preserve FRP data.

For more information, see [Factory reset protection emails setting isn't enforced after you reset an Android Enterprise device](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced).

### Samsung devices

For Android Enterprise fully managed Samsung devices, make sure the **Factory Reset** setting under **Device Restrictions** isn't set to **Block**.

If **Factory Reset** is blocked and a **Wipe** action is initiated, the device loses contact with Intune and be unable to complete the factory reset.

### Zebra devices

On Zebra Android devices, the **Wipe** remote action is designed to remove only corporate data. It doesn't perform a factory reset.

To factory reset a Zebra Android device, use one of the following methods:

- [Use Zebra StageNow](https://techdocs.zebra.com/stagenow/5-17/profiles/wipedevice/)
- [Use OEM Config Data Wipe Configuration](https://techdocs.zebra.com/oemconfig/latest/mc2/)
::: zone-end

## How to wipe a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Wipe**.

::: zone pivot="macos"
4. Enter a 6-digit **Recovery PIN**. This PIN is required to reinstall the operating system on devices that don't have the T2 security chip—typically models from 2018 or earlier, or devices running macOS 10.14 or earlier. Make sure to record the PIN and share it with the device owner. The PIN won't be visible after the wipe completes.
5. Select an option from **Obliteration Behavior**, which is used to define the fallback for devices when Erase All Contents and Settings (EACS) fails. The following options can be configured:

    - **Default**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Do not obliterate**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and doesn't attempt to erase itself. If EACS preflight succeeds but EACS fails, then the device doesn't attempt to erase itself.
    - **Obliterate with warning**: If Erase All Content and Settings (EACS) preflight fails, the device responds with a Success status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Always obliterate**: The system doesn't attempt Erase All Content and Settings (EACS). T2 and later devices always obliterate.
6. Select **Wipe** to erase the device.
::: zone-end

::: zone pivot="windows"
4. You can customize the wipe behavior with the following options:

    - **Wipe device, but keep enrollment state and associated user account**
      - When selected, the wipe removes all MDM policies but retains user accounts and data. User settings are reset to default, and the device remains enrolled in Intune.
      - When not selected, the wipe removes all user accounts, data, MDM policies, and settings. The device is reset to its factory default state.
    - **Wipe device, and continue to wipe even if device loses power**
      - Ensures the wipe continues even if the device loses power during the process. This prevents users from interrupting the wipe, which is useful in high-security scenarios such as lost or stolen devices.

        > [!IMPORTANT]
        > Selecting this option might prevent some devices from starting up again. The wipe process can interfere with boot recovery or     firmware protections, potentially leaving the device in an unrecoverable state. Use this option only on corporate-owned devices     where full data destruction is required and recovery procedures are in place.

      - When not selected, if the wipe is interrupted, the device attempts to roll back to its previous state. If rollback fails, the device may become unusable and require a full reinstallation of Windows.

5. To confirm the wipe, select **Yes**.

::: zone-end
::: zone pivot="ios"
4. For iOS/iPadOS eSIM devices, the cellular data plan is preserved by default when you wipe a device. If you want to remove the data plan from the device when you wipe the device, select the **Also remove the devices data plan...** option.
::: zone-end

::: zone pivot="chromeos"

4. Select on of the following options:

    - **Remove user profiles only**: To remove all user account data. Device and enrollment policies remain on the device.
    - **Factory reset (powerwash)**: To restore a device to its factory state, removing all personal and work data. Before using this action, [deprovision](device-deprovision.md) the device. Otherwise, once it connects to Wi-Fi, it will automatically enroll again.

For more information about wiping ChromeOS devices, see [Wipe ChromeOS device data](https://support.google.com/chrome/a/answer/1360642).

::: zone-end

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

::: zone pivot="windows"

[!INCLUDE [remove-device-from-autopilot](includes/remove-device-from-autopilot.md)]

::: zone-end

::: zone pivot="android,ios,macos,windows"
[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]
::: zone-end

## Reference links


- Microsoft Graph API: [wipe action][GRAPH-1]
::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the remote action: [RemoteWipe CSP][CSP-1]
::: zone-end

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
[CSP-1]: /windows/client-management/mdm/remotewipe-csp

---
<!--test-->
[!INCLUDE [rbac-requirements](includes/h3/rbac-requirements.md)]

laoreet ipsum lorem adipiscing adipiscing nonummy dolore nonummy adipiscing laoreet dolor adipiscing nonummy nibh erat elit nonummy adipiscing elit nonummy amet sit nonummy magna sed aliquam laoreet consectetuer amet aliquam euismod elit lorem euismod magna consectetuer diam euismod consectetuer euismod sit ut amet erat magna nibh aliquam sit dolore elit dolore amet sit magna sed ut adipiscing sed sed magna adipiscing. ut consectetuer nibh adipiscing adipiscing sit sed aliquam magna elit elit aliquam aliquam amet elit ipsum sed adipiscing laoreet ipsum sed aliquam erat amet adipiscing adipiscing diam ipsum sed euismod ut amet lorem diam nibh diam tincidunt erat adipiscing ipsum elit diam ut tincidunt sit lorem nonummy sed euismod laoreet lorem tincidunt sed aliquam magna amet laoreet nonummy sed diam laoreet.
sit ut consectetuer magna lorem dolore aliquam sed sed euismod lorem elit amet sit lorem nibh elit lorem sit aliquam magna aliquam euismod nibh sed ut erat ipsum lorem laoreet aliquam nonummy amet nibh elit diam laoreet diam lorem diam euismod laoreet elit adipiscing tincidunt aliquam ut ipsum aliquam diam dolore adipiscing ipsum amet sed adipiscing euismod euismod nonummy ut lorem. lorem dolore erat sit adipiscing nibh dolore nibh aliquam nonummy elit lorem euismod diam diam dolor consectetuer amet erat sit amet diam laoreet nonummy magna magna sed consectetuer amet dolor nonummy tincidunt dolore sed dolor amet lorem diam adipiscing aliquam consectetuer dolore magna lorem ut sit dolor ut tincidunt adipiscing lorem erat ut tincidunt dolore tincidunt magna tincidunt dolor ut nonummy.

[!INCLUDE [platform-requirements](includes/h3/platform-requirements.md)]

laoreet ipsum lorem adipiscing adipiscing nonummy dolore nonummy adipiscing laoreet dolor adipiscing nonummy nibh erat elit nonummy adipiscing elit nonummy amet sit nonummy magna sed aliquam laoreet consectetuer amet aliquam euismod elit lorem euismod magna consectetuer diam euismod consectetuer euismod sit ut amet erat magna nibh aliquam sit dolore elit dolore amet sit magna sed ut adipiscing sed sed magna adipiscing. ut consectetuer nibh adipiscing adipiscing sit sed aliquam magna elit elit aliquam aliquam amet elit ipsum sed adipiscing laoreet ipsum sed aliquam erat amet adipiscing adipiscing diam ipsum sed euismod ut amet lorem diam nibh diam tincidunt erat adipiscing ipsum elit diam ut tincidunt sit lorem nonummy sed euismod laoreet lorem tincidunt sed aliquam magna amet laoreet nonummy sed diam laoreet.
sit ut consectetuer magna lorem dolore aliquam sed sed euismod lorem elit amet sit lorem nibh elit lorem sit aliquam magna aliquam euismod nibh sed ut erat ipsum lorem laoreet aliquam nonummy amet nibh elit diam laoreet diam lorem diam euismod laoreet elit adipiscing tincidunt aliquam ut ipsum aliquam diam dolore adipiscing ipsum amet sed adipiscing euismod euismod nonummy ut lorem. lorem dolore erat sit adipiscing nibh dolore nibh aliquam nonummy elit lorem euismod diam diam dolor consectetuer amet erat sit amet diam laoreet nonummy magna magna sed consectetuer amet dolor nonummy tincidunt dolore sed dolor amet lorem diam adipiscing aliquam consectetuer dolore magna lorem ut sit dolor ut tincidunt adipiscing lorem erat ut tincidunt dolore tincidunt magna tincidunt dolor ut nonummy.
