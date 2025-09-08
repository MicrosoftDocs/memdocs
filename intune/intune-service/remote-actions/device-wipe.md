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
---

# Wipe devices with Intune

By using the **Retire** or **Wipe** actions, you can remove devices from Intune that are no longer needed, being repurposed, or missing. Users can also issue a remote command from the Intune Company Portal to devices that are enrolled in Intune.

If [multi-admin approval access policies](../fundamentals/multi-admin-approval.md) are enabled for device actions, then some device actions might require a second administrator to approve. To learn more, see [Use Access policies to require multiple administrative approvals](../fundamentals/multi-admin-approval.md).

## Wipe

The **Wipe** device action restores a device to its factory default settings. The user data is kept if you choose the **Wipe device, but keep enrollment state and associated user account** checkbox. Otherwise, all data, apps, and settings are removed.

|Wipe action|**Wipe device, but keep enrollment state and associated user account**|Removed from Intune management|Description|
|:-------------:|:------------:|:------------:|------------|
|**Wipe**| Not checked | Yes | Wipes all user accounts, data, MDM policies, and settings. Resets the operating system to its default state and settings.|
|**Wipe**| Checked | No | Wipes all MDM Policies. Keeps user accounts and data. Resets user settings back to default. Resets the operating system to its default state and settings.|

> [!NOTE]
> The Wipe action is not available for iOS/iPadOS devices enrolled using Account Driven Apple User Enrollment. To create an Account Driven Apple User Enrollment profile, see [Set up iOS/iPadOS and iPadOS Account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md).

> [!NOTE]
> By design, Zebra has defined the Wipe action on any Android Zebra device to only remove corporate data from devices, and not perform a factory reset.
> To perform factory reset on a Zebra Android device, you can use either of these methods:
> - [Use Zebra StageNow](https://techdocs.zebra.com/stagenow/5-11/profiles/wipedevice/)
> - [Use OEM Config Data Wipe Configuration](https://techdocs.zebra.com/oemconfig/latest/mc/)

> [!NOTE]
> For fully managed Samsung devices (Android Enterprise), make sure that you do NOT have **Factory Reset** set to **Block** under **Device Restrictions**. If the **Factory Reset** toggle is set to **Block** and a **Wipe** action is initiated, the device will lose contact with Intune and will also be prevented from being factory reset.

> [!NOTE]
> **Factory Reset Protection (FRP) considerations (Android Enterprise):** Whether a device prompts for Google account credentials after reset depends on ownership (**Corporate owned with work profile/Fully managed/Dedicated**), the reset method (**Settings**, **Recovery**, or **admin wipe**), and whether FRP is configured. By default, Intune's admin wipe **does not** preserve FRP data. For more information, see [Factory reset protection emails setting isn't enforced after you reset an Android Enterprise device](/troubleshoot/mem/intune/device-configuration/factory-reset-protection-emails-not-enforced).

> [!IMPORTANT]
>
> The Wipe action doesn't remove the Windows Autopilot registration from the device. To remove the Windows Autopilot registration from the device, see [Deregister from Windows Autopilot using Intune](/autopilot/registration-overview#deregister-from-autopilot-using-intune)

The **Retain enrollment state and user account** option is only available for Windows 10 version 1709 or later.

MDM policies will be reapplied the next time the device connects to Intune.

A wipe is useful for resetting a device before you give the device to a new user, or when the device has been lost or stolen. Be careful about selecting **Wipe**. Data on the device can't be recovered. The method that "Wipe" uses to remove data is simple file deletion, and the drive is BitLocker decrypted as part of this process.

### How to wipe a device

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. Select the name of the device that you want to wipe.
4. In the pane that shows the device name, select **Wipe**.
5. For Windows 10 version 1709 or later, you also have the **Wipe device, but keep enrollment state and associated user account** option. If this option is selected, the following user account details are retained:

    |Retained during a wipe |Not retained|
    | -------------|------------|
    |User accounts associated with the device|User files|
    |Machine state \(domain join, Microsoft Entra joined)| User-installed apps \(store and Win32 apps)|
    |Mobile device management (MDM) enrollment|Non-default device settings|
    |OEM-installed apps \(store and Win32 apps)||
    |User profile||
    |User data outside of the user profile||
    |User autologon||

6. The **Wipe device, and continue to wipe even if device loses power** option makes sure that the wipe action can't be circumvented by turning off the device. This option keeps trying to reset the device until successful. In some configurations, this action can leave the device [unable to reboot](/troubleshoot/mem/intune/troubleshoot-device-actions#wipe-action).
7. For iOS/iPadOS eSIM devices, the cellular data plan is preserved by default when you wipe a device. If you want to remove the data plan from the device when you wipe the device, select the **Also remove the devices data plan...** option.
8. To confirm the wipe, select **Yes**.

If the device is on and connected, the **Wipe** action propagates across all device types in less than 15 minutes.

## Supported platforms for Wipe device action

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>

- Android Enterprise Dedicated, Fully Managed, and Corporate-Owned Work Profile devices
- Android Open Source Project (AOSP) devices
- iOS/iPadOS
- macOS
- Windows 10/11

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>

## Manually unenroll devices

Device owners can manually unenroll their devices as explained in the following end user help articles:

- [Remove device from Company Portal for Android](../user-help/unenroll-your-device-from-intune-android.md)
- [Remove device from Company Portal for iOS app](../user-help/unenroll-your-device-from-intune-ios.md)
- [Remove device from Company Portal for macOS app](../user-help/unenroll-your-device-from-intune-macos.md)
- [Remove your Windows device from management](../user-help/unenroll-your-device-from-intune-windows.md)

> [!TIP]
> When a Windows device user uses the Settings app to un-enroll their device, Intune and the cleanup rules don't automatically delete the Intune device or Microsoft Entra ID records. To remove the Intune device record:
> - Manually delete the device in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
> - Manually delete the device record in Microsoft Entra ID.


## Wipe all data from a macOS device

Intune gives you the ability to use the **Wipe** remote device action to wipe data from macOS devices, including the operating system.

> [!IMPORTANT]
> When you use **Wipe**, the device is also removed from Intune management and no warning is given to the end user once a wipe is initiated.

> [!NOTE]
> The behavior for **Wipe** on iOS devices is that it restores the device to factory defaults and removes the management profile, including any configuration profiles that were installed.

## Before you start

- For devices running macOS 12.0.1 and later, review the requirements for erasing devices available on the [Apple Support site](https://support.apple.com/en-ph/guide/deployment/dep0a819891e/web).

- For devices running a version of macOS earlier to 12.0.1, macOS must be reinstalled. Steps covering how to reinstall macOS are available on the [Apple Support site](https://support.apple.com/en-us/HT204904).

## How to wipe a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **Wipe**.
1. Provide a 6-digit number for the **Recovery PIN**. The six-digit PIN is required to reinstall the operating system on the device, if the device isn't equipped with T2 security chip enabled (that is, the model year of the device is 2018 and earlier, or the device is running macOS 10.14 or earlier). Be sure to make a note of this PIN and give it to the device owner as it won't be visible after the wipe action completes.

    :::image type="content" source="images/obliteration-behavior.png" alt-text="Screen shot that shows where to provide a pin and select an option for obliteration behavior." lightbox="images/obliteration-behavior.png":::

1. Select an option from **Obliteration Behavior**, which is used to define the fallback for devices when Erase All Contents and Settings (EACS) fails. The following options can be configured:

    - **Default**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Do not obliterate**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and doesn't attempt to erase itself. If EACS preflight succeeds but EACS fails, then the device doesn't attempt to erase itself.
    - **Obliterate with warning**: If Erase All Content and Settings (EACS) preflight fails, the device responds with a Success status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.
    - **Always obliterate**: The system doesn't attempt Erase All Content and Settings (EACS). T2 and later devices always obliterate.
1. Select **Wipe** to erase the device.

## Reference links

- Microsoft Graph API: [wipe action][GRAPH-1]

<!--
Initiates a wipe of the device. Also called a factory reset. The Factory reset action restores a device to its factory default settings. The user data is kept or wiped depending on whether or not you choose the Retain enrollment state and user account checkbox.


Are you sure you want to wipe CLIENT
Factory reset returns the device to its default settings. This removes all personal and company data and settings from this device. You can choose whether to keep the device enrolled and the user account associated with this device. You cannot revert this action. Are you sure you want to reset this device?
Wipe device, but keep enrollment state and associated user account
Wipe device, and continue to wipe even if device loses power. If you select this option, please be aware that it might prevent some devices running Windows 10 and later from starting up again.


{
  "keepEnrollmentData": true,
  "keepUserData": true,
  "macOsUnlockCode": "Mac Os Unlock Code value",
  "obliterationBehavior": "doNotObliterate",
  "persistEsimDataPlan": true,
  "useProtectedWipe": true
}
-->
