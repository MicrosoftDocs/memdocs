---
title: "Wipe devices with Microsoft Intune"
description: Learn how to wipe managed devices with Microsoft Intune, choose platform-specific reset options, and prepare devices for retirement, reuse, or recovery.
ms.date: 08/20/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
zone_pivot_groups: c5fbc3ee-cfe5-494a-b441-d95cbed3128c
#customer intent: As an Intune administrator, I want to wipe managed devices so that I can securely reset, retire, or repurpose them.
---

# Wipe devices with Microsoft Intune

Use the *Wipe* action in Intune to factory reset a device, restoring it to its default settings. This action removes all personal and organizational data, apps, and configurations. It's commonly used when a device needs to be retired, repurposed, reset for troubleshooting, or securely erased if lost or stolen.

Depending on the platform, you can customize the wipe behavior to meet your organization's needs.

> [!IMPORTANT]
> A tenant can submit up to 500 Wipe actions per day. This tenant-wide limit is cumulative across individual device actions, bulk device actions, and Microsoft Graph API requests. To request a limit change, [contact Microsoft support](../../fundamentals/it-pro-support/get-support-admin-center.md). For all device action limits, see [Daily tenant limits](index.md#daily-tenant-limits).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Open Source Project (AOSP)
> - ChromeOS
> - iOS/iPadOS
> - macOS
> - tvOS 10.2+
> - visionOS 1.1+
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator]
> - [School Administrator]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
::: zone pivot="macos,android"
## Before wiping a device
::: zone-end

::: zone pivot="macos"

Review the requirements for erasing macOS devices available on [Apple's deployment guide for erasing devices](https://support.apple.com/guide/deployment/dep0a819891e).

::: zone-end

::: zone pivot="android"

### Factory Reset Protection (FRP) considerations

Whether a device requires Google account credentials after reset depends on ownership (Android Enterprise corporate-owned work profile/fully managed/dedicated), the reset method (Settings, Recovery, or admin wipe), and whether FRP is configured. By default, Intune's admin wipe doesn't preserve FRP data.

For more information, see [Factory reset protection emails setting isn't enforced after you reset an Android Enterprise device](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced).

### Samsung devices

For Android Enterprise fully managed Samsung devices, make sure the **Factory Reset** setting under **Device Restrictions** isn't set to **Block**.

If **Factory Reset** is blocked and a **Wipe** action is initiated, the device loses contact with Intune and be unable to complete the factory reset.

### Zebra devices

On Zebra Android devices, the **Wipe** action is designed to remove only corporate data. It doesn't perform a factory reset.

To factory reset a Zebra Android device, use one of the following methods:

- [Use Zebra StageNow](https://techdocs.zebra.com/stagenow/5-17/profiles/wipedevice/)
- [Use OEM Config Data Wipe Configuration](https://techdocs.zebra.com/oemconfig/latest/mc2/)
::: zone-end

## How to wipe a device from the Intune admin center

::: zone pivot="android"
> [!IMPORTANT]
> To choose whether to remove eSIMs during a single-device wipe, use the new device view. In the [Microsoft Intune admin center], go to [**Devices**] > [**All devices**], set **Preview new device view** to **On**, and then select the device.
::: zone-end

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Wipe**.

::: zone pivot="android"
4. For Android Enterprise corporate-owned fully managed (COBO), corporate-owned dedicated (COSU), and corporate-owned work profile (COPE) devices, eSIMs are preserved by default. To remove the eSIMs during the wipe, select the option to remove eSIMs.
5. Select **Wipe**.

::: zone-end

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
      - Resets the device to factory settings, while preserving the user data, user accounts, and important settings.\
        To learn more about what data is preserved, see [How push-button reset features work](/windows-hardware/manufacture/desktop/how-push-button-reset-features-work#keep-my-files).
      - MDM policies and settings are removed, but the device remains enrolled in Intune.
      - Uses the [doWipePersistUserData](/windows/client-management/mdm/remotewipe-csp#dowipepersistuserdata) CSP node.
    - **Wipe device, and continue to wipe even if device loses power**
      - Resets the device to factory settings, deleting all user data, settings, and MDM policies.
      - Overwrites the free space to prevent data recovery.
      - Ensures the wipe continues even if the device loses power, preventing interruption—ideal for high-security scenarios such as lost or stolen devices.
      - Uses the [doWipeProtected](/windows/client-management/mdm/remotewipe-csp#dowipeprotected) CSP node.
        > [!IMPORTANT]
        > This option can prevent some devices from starting up again. The wipe process may interfere with boot recovery or firmware protections, leaving the device unrecoverable. Use only on corporate-owned devices where full data destruction is required and recovery procedures are in place.
    - **No options selected**
      - Resets the device to factory settings, deleting all user data, settings, and MDM policies.
      - If the wipe is interrupted, the device attempts to roll back to its previous state. If rollback fails, the device may become unusable and require a full Windows reinstallation.
      - Uses the [doWipe](/windows/client-management/mdm/remotewipe-csp#dowipe) CSP node.

5. To confirm the wipe, select **Wipe**.

::: zone-end
::: zone pivot="ios"
4. For iOS/iPadOS eSIM devices, the cellular data plan is preserved by default when you wipe a device. If you want to remove the data plan from the device when you wipe the device, select the **Also remove the devices data plan...** option.
::: zone-end

::: zone pivot="chromeos"

4. Select on of the following options:

    - **Remove user profiles only**: To remove all user account data. Device and enrollment policies remain on the device.
    - **Factory reset (powerwash)**: To restore a device to its factory state, removing all personal and work data. Before using this action, [deprovision](deprovision.md) the device. Otherwise, once it connects to Wi-Fi, it will automatically enroll again.

For more information about wiping ChromeOS devices, see [Wipe ChromeOS device data](https://support.google.com/chrome/a/answer/1360642).

::: zone-end

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

::: zone pivot="windows"

[!INCLUDE [remove-device-from-autopilot](includes/remove-device-from-autopilot.md)]

::: zone-end

::: zone pivot="android,ios,macos,windows"
[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]
::: zone-end

::: zone pivot="android"
## Wipe multiple Android Enterprise devices

You can preserve or remove eSIMs when you use a bulk wipe for Android Enterprise corporate-owned fully managed (COBO), corporate-owned dedicated (COSU), and corporate-owned work profile (COPE) devices. The bulk wipe uses the standard bulk device action workflow.

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**] > [**Bulk device actions**].
1. On the **Basics** page, select **Android** for the operating system and **Wipe** for the device action.
1. By default, the wipe preserves eSIMs. To remove the eSIMs during the wipe, select the option to remove eSIMs, and then select **Next**.
1. On the **Devices** page, select the devices to wipe, and then select **Next**.
1. On the **Review + create** page, select **Create**.

::: zone-end

## Reference links


- Microsoft Graph API: [wipe action][GRAPH-1]
::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the action: [RemoteWipe CSP][CSP-1]
::: zone-end

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**Bulk device actions**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/BulkActionWizardBlade
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#school-administrator
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe

<!--Other links-->

[CSP-1]: /windows/client-management/mdm/remotewipe-csp
