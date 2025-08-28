---
# required metadata

title: Retire devices using Microsoft Intune
description: Learn how to retire device using Microsoft Intune.
ms.date: 07/22/2025
ms.topic: how-to

ms.reviewer:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Retire

The **Retire** action removes managed app data (where applicable), settings, and email profiles that were assigned by using Intune. The device is removed from Intune management. Removal happens the next time the device checks in and receives the remote **Retire** action. The device still shows up in Intune until the device checks in. If you want to remove stale devices immediately, use the [Delete action](devices-wipe.md#delete-devices-from-the-intune-admin-center) instead.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> -


### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute these remote actions, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)

## How to retire a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **Retire**. To confirm, select **Yes**.

###Effect of the **Retire** action on data that remains on the device

When you use the **Retire** device action, the user's personal data is not removed from the device.

The following tables describe what data is removed, and the effect of the **Retire** action on data that remains on the device after company data is removed.

# [:::image type="icon" source="../media/icons/platforms/ios-ipados.svg"::: **iOS/iPadOS**](#tab/ios-ipados)

> [!IMPORTANT]
> Retired devices might not be automatically deleted resulting in the device record remaining in Intune for 180 days unless issued a **Delete** action.

|Data type|iOS|
|-------------|-------|
|Company apps and associated data installed by Intune|**Apps installed using Company Portal:** For apps that are pinned to the management profile, all app data and the apps are removed. These apps include apps originally installed from App Store and later managed as company apps unless the app is configured to not be uninstalled on device removal. <br /><br /> **Microsoft apps that use App Protection Policies and were installed from App Store:** Intune triggers a [selective wipe](../apps/apps-selective-wipe.md) for apps protected by an [App Protection Policy](../apps/app-protection-policy.md) when a Retire action is initiated against an enrolled device. This wipe includes apps installed from the App Store that have work or school account data. The next time the app is launched, the selective wipe removes the protected work or school account data. In order for the selective wipe to occur, an App Protection Policy check-in must occur between the MDM enrollment and retire events. Personal app data and the apps aren't removed after a selective wipe.|
|Settings|Configurations set by Intune policy are no longer enforced. Users can change the settings.|
|Wi-Fi and VPN profile settings|Removed.|
|Certificate profile settings|Certificates are removed and revoked.|
|Management agent|The management profile is removed.|
|Email|Email profiles that are provisioned through Intune are removed. Cached email on the device is deleted.|
|Microsoft Entra Device Record |The Microsoft Entra ID record isn't removed.|

> [!NOTE]
> Users that reinstall the Outlook Mobile app following a **Retire** device action may need to choose to **Delete All Saved Contacts** before re-exporting contacts to avoid duplicate contact entries.  Previously exported contacts from Outlook Mobile are considered personal data and are not removed by the **Retire** device action.

# [:::image type="icon" source="../media/icons/platforms/android.svg"::: **Android**](#tab/android)

#### Android device administrator

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

|Data type|Android|Android Samsung Knox Standard|
|-------------|-----------|------------------------|
|Web links|Removed.|Removed.|
|Unmanaged Google Play apps|Apps and data remain installed. <br /> <br />Company app data that's protected by Mobile Application Management (MAM) encryption within the app local storage is removed. Data that's protected by MAM encryption outside the app remains encrypted and unusable, but isn't removed. |Apps and data remain installed. <br /> <br />Company app data that's protected by Mobile Application Management (MAM) encryption within the app local storage is removed. Data that's protected by MAM encryption outside the app remains encrypted and unusable, but isn't removed.|
|Unmanaged line-of-business apps|Apps and data remain installed.|Apps are uninstalled and data that's local to the app is removed. No data that's outside the app (for example, on an SD card) is removed.|
|Managed Google Play apps|App data is removed. The app isn't removed. Data that's protected by Mobile Application Management (MAM) encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed.|App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted, but isn't removed.|
|Managed line-of-business apps|App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed.|App data is removed. The app isn't removed. Data that's protected by MAM encryption outside the app (for example, an SD card) remains encrypted and unusable, but isn't removed.|
|Settings|Configurations set by Intune policy are no longer enforced. Users can change the settings.|Configurations set by Intune policy are no longer enforced. Users can change the settings.|
|Wi-Fi and VPN profile settings|Removed.|Removed.|
|Certificate profile settings|Certificates are revoked but not removed.|Certificates are removed and revoked.|
|Management agent|Device Administrator privilege is revoked.|Device Administrator privilege is revoked.|
|Email|N/A (Android devices don't support Email profiles)|Email profiles that are provisioned through Intune are removed. Cached email on the device is deleted.|
|Microsoft Entra unjoin|The Microsoft Entra ID record is removed.|The Microsoft Entra ID record is removed.|

#### Android Enterprise personally owned devices with a work profile

Removing company data from an Android personally owned work profile device removes all data, apps, and settings in the work profile on that device. The device is retired from management with Intune.

# [:::image type="icon" source="../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)


- Settings: Configurations set by Intune policy are no longer enforced. Users can change the settings.
- Wi-Fi and VPN profile settings: Removed.
- Certificate profile settings: Certificates that were deployed through MDM are removed and revoked.
- Management agent: The management profile is removed.
- Outlook: If Conditional Access is enabled, the device doesn't receive new mail.
- Microsoft Entra Device Record: The Microsoft Entra ID record isn't removed.


# [:::image type="icon" source="../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

- Company apps and associated data installed by Intune: Apps are uninstalled. Sideloading keys are removed.<br>For Windows 10 version 1709 (Creators Update) and later, Microsoft 365 Apps aren't removed. Intune management extension installed Win32 apps aren't uninstalled on unenrolled devices. Admins can use assignment exclusion to not offer Win32 apps to BYOD Devices.
- Settings: Configurations set by Intune policy are no longer enforced. Users can change the settings.
- Wi-Fi and VPN profile settings: Removed.
- Certificate profile settings: Certificates are removed and revoked.
- Email: Removes email that's EFS-enabled including emails and attachments in the Mail app for Windows. Removes mail accounts provisioned by Intune.
- Microsoft Entra unjoin: The Microsoft Entra ID record is removed.

> [!IMPORTANT]
> Windows devices that are not registered in the Windows Autopilot Service, upon being deleted or retired from Intune are removed from Microsoft Entra ID. Before performing these commands consider backing up the BitLocker Recovery Key and/or a local administrator user account credentials. On the other hand, although Windows Autopilot registered devices leave Microsoft Entra ID, their computer object is retained alongside their properties (e.g. Windows LAPS, BitLocker Recovery Key, Entra ID groups memberships).

> [!NOTE]
> For Windows 10 devices that join Microsoft Entra ID during initial Setup (OOBE), the retire command will remove all Microsoft Entra accounts from the device. Follow the steps at [Start your PC in Safe mode](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode) to login as a local admin and regain access to the user's local data.

---


## Reference links

- Microsoft Graph API reference: [wipe action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
