---
title: "Remote Device Action: Retire"
description: Learn how to retire device using Microsoft Intune.
ms.date: 07/22/2025
ms.topic: how-to
zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Remote device action: retire

The *retire* remote action in Intune removes company data from a device without performing a full wipe or factory reset. This action is ideal for personally owned devices or when transitioning a device out of organizational control. It unenrolls the device from Intune and removes managed apps, settings, and profiles deployed through mobile device management (MDM), while preserving personal data.

Unlike the **Wipe** action, which resets the device to factory settings, **Retire** keeps user content intact. The action is triggered the next time the device checks in with Intune. Until then, the device might still appear in the admin center. If you need to remove a device immediately, consider using the [Delete action](device-delete.md) instead.

::: zone pivot="windows"

## Before retiring or deleting a Microsoft Entra joined device

If you delete or retire the Intune object for a Microsoft Entra joined device that is protected by BitLocker, Intune triggers a sync that removes key protectors. This action suspends BitLocker on the OS volume as a safeguard to prevent unrecoverable encryption scenarios when the Entra object is deleted.

Before retiring a Microsoft Entra joined device, make sure to back up any critical data that may be lost during the process, such as:

- BitLocker recovery key
- Local administrator account credentials

::: zone-end

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Android device administrator
> - Android Enterprise personally-owned work profile (BYOD)
> - iOS/iPadOS
> - macOS
> - Windows

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Retire**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to retire a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Retire**. To confirm, select **Yes**.

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

## User experience

When you use the **Retire** device action, the user's personal data isn't removed from the device.

::: zone pivot="ios"

The following table shows what data is removed and what remains on the device after the action is applied.

| Data type | iOS |
|-------------|-------|
|Company apps and associated data installed by Intune|**Apps installed using Company Portal:** For apps that are pinned to the management profile, all app data and the apps are removed. These apps include apps originally installed from App Store and later managed as company apps unless the app is configured to not be uninstalled on device removal. <br /><br /> **Microsoft apps that use App Protection Policies and were installed from App Store:** Intune triggers a [selective wipe](../apps/apps-selective-wipe.md) for apps protected by an [App Protection Policy](../apps/app-protection-policy.md) when a Retire action is initiated against an enrolled device. This wipe includes apps installed from the App Store that have work or school account data. The next time the app is launched, the selective wipe removes the protected work or school account data. In order for the selective wipe to occur, an App Protection Policy check-in must occur between the MDM enrollment and retire events. Personal app data and the apps aren't removed after a selective wipe.|
|Settings|Configurations set by Intune policy are no longer enforced. Users can change the settings.|
|Wi-Fi and VPN profile settings|Removed.|
|Certificate profile settings|Certificates are removed and revoked.|
|Management agent|The management profile is removed.|
|Email|Email profiles that are provisioned through Intune are removed. Cached email on the device is deleted.|
|Microsoft Entra device record |The Microsoft Entra ID record isn't removed.|

> [!NOTE]
> Users that reinstall the Outlook Mobile app following a **Retire** device action might need to choose to **Delete All Saved Contacts** before re-exporting contacts to avoid duplicate contact entries. Previously exported contacts from Outlook Mobile are considered personal data and are not removed by the **Retire** device action.

::: zone-end

::: zone pivot="android"

### Android Enterprise personally owned devices with a work profile

Removing company data from an Android personally owned work profile device removes all data, apps, and settings in the work profile on that device.

### Android device administrator

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

The following table shows what data is removed and what remains on the device after the action is applied.

| Data type | Android | Android Samsung Knox Standard |
|--|--|--|
| Web links | Removed. | Removed. |
| Unmanaged Google Play apps | Apps and data remain installed. <br /> <br />Company app data that's protected by Mobile Application Management (MAM) encryption within the app local storage is removed. Data that's protected by MAM encryption outside the app remains encrypted and unusable, but isn't removed. | Apps and data remain installed. <br /> <br />Company app data that's protected by Mobile Application Management (MAM) encryption within the app local storage is removed. Data that's protected by MAM encryption outside the app remains encrypted and unusable, but isn't removed. |
| Unmanaged line-of-business apps | Apps and data remain installed. | Apps are uninstalled and data that's local to the app is removed. No data that's outside the app (for example, on an SD card) is removed. |
| Managed Google Play apps | App data is removed. The app isn't removed. Data that's protected by Mobile Application Management (MAM) encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed. | App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted, but isn't removed. |
| Managed line-of-business apps | App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed. | App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed. |
| Settings | Configurations set by Intune policy are no longer enforced. Users can change the settings. | Configurations set by Intune policy are no longer enforced. Users can change the settings. |
| Wi-Fi and VPN profile settings | Removed. | Removed. |
| Certificate profile settings | Certificates are revoked but not removed. | Certificates are removed and revoked. |
| Management agent | Device Administrator privilege is revoked. | Device Administrator privilege is revoked. |
| Email | N/A (Android devices don't support Email profiles) | Email profiles that are provisioned through Intune are removed. Cached email on the device is deleted. |
| Microsoft Entra device record | The Microsoft Entra ID record is removed. | The Microsoft Entra ID record is removed. |

::: zone-end

::: zone pivot="macos"

The following table shows what data is removed and what remains on the device after the action is applied.

| Data type | macOS |
|--|--|
| Settings | Configurations set by Intune policy are no longer enforced. Users can change the settings. |
| Wi-Fi and VPN profile settings | Removed. |
| Certificate profile settings | Certificates are removed and revoked. |
| Management agent | The management profile is removed. |
| Outlook | If Conditional Access is enabled, the device doesn't receive new mail. |
| Microsoft Entra device record | The Microsoft Entra ID record isn't removed. |

::: zone-end

::: zone pivot="windows"

The following table shows what data is removed and what remains on the device after the action is applied.

| Data type | Windows |
|--|--|
| Company apps and associated data installed by Intune | - Apps are uninstalled<br>-Sideloading keys are removed<br> Microsoft 365 Apps aren't removed<br>- Intune management extension installed Win32 apps aren't uninstalled on unenrolled devices. Admins can use assignment exclusion to not offer Win32 apps to BYOD Devices. |
| Settings | Configurations set by Intune policy are no longer enforced. Users can change the settings. |
| Wi-Fi and VPN profile settings | Removed. |
| Certificate profile settings | Certificates are removed and revoked. |
| Email | Removes email that's EFS-enabled including emails and attachments in the Mail app for Windows. Removes mail accounts provisioned by Intune |
| Microsoft Entra join status | - If the device is Microsoft Entra joined, the device is unjoined from Microsoft Entra.<br>- If the device is Microsoft Entra registered, the work or school account is disconnected and the device is unregistered from Microsoft Entra ID.|
| Microsoft Entra device record | - If the device is registered in Autopilot, the Microsoft Entra ID record is not removed.<br>- If the device is Microsoft Entra joined, the record is removed.<br>- If the device is Microsoft Entra registered, the record is removed.|

For Microsoft Entra ID joined devices, after the **Retire** command is executed, you can't sign in wih a Microsoft Entra account. Follow the steps at [Start your PC in Safe mode](https://support.microsoft.com/topic/1af6ec8c-4d4a-4b23-adb7-e76eef0b847f) to sign in with a local admin account and regain access to the user's local data.

::: zone-end

[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]

::: zone pivot="ios,macos"

[!INCLUDE [remove-device-from-apple-ade](includes/remove-device-from-apple-ade.md)]

::: zone-end

## Reference links

- Microsoft Graph API: [retire action][GRAPH-1]
- Configuration service provider (CSP) used to initiate the remote action: [Defender CSP][CSP-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-retire
[CSP-1]: /windows/client-management/mdm/defender-csp
