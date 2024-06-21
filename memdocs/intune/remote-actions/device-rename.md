---
# required metadata

title: Rename a device with Microsoft Intune
description: Rename a device by using Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/29/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Elcox 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Rename a device in Intune

You can use the **Rename device** action to change the **Device name** in the Microsoft Intune admin center for a device enrolled in Intune. The Rename action doesn't change the **Management name** in the Intune admin center or the **Device name** in the Company Portal.

For more information, on modifying the Management name and renaming in the Company Portal go to:

- [View device details with Microsoft Intune](../remote-actions/device-inventory.md#hardware-device-details).
- [Rename device from the Intune Company Portal app for Windows](../user-help/rename-your-device-cpapp.md).

If a device isn't listed here, it's not supported. This feature doesn't support renaming hybrid Microsoft Entra Windows devices.

You can rename the following types of devices:

- Android Enterprise:
  - Corporate-owned work profiles
  - Dedicated devices
  - Fully managed
- iOS/iPadOS supervised devices with iOS 9.3 and later
- macOS 10 - Corporate-owned devices
- Windows - Corporate-owned devices
- Corporate-owned co-managed devices that are Microsoft Entra joined

> [!NOTE]
> Renaming of Android Enterprise devices will only change the **Device name** in the Intune admin center and not on the device itself. The Device name in Intune is a friendly name that users are free to change.

## Rename a device

Use the **Rename** action to give your device a new name. If you already renamed the device but don't see its new name, the device might need to check in to Intune. Check the status of your rename in device **Overview** before attempting to rename again.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices** > choose a device > **...** > **Rename device**.
3. In the **Rename device** pane, type the new name in the text box. You can use letters, numbers, and hyphens. The name must contain at least one letter or hyphen. Android Enterprise dedicated, fully managed, and corporate-owned work profile devices are an exception, and don't require a letter or hyphen.
4. If you want to restart the device after renaming it, choose **Yes** next to **Restart after rename**.
5. Choose **Rename**.

> [!NOTE]
> If you have an enrollment profile (iOS) that uses a Device Name Template, the device will be renamed but will revert to using the template upon the next sync with Intune.

> [!NOTE]
> It may take 10 minutes or more for a renamed Android Enterprise device to update in the Devices blade.

## Windows device rename rules

When you rename a Windows device, the new name must follow these rules:

- Less than or equal to 63 bytes, not including trailing NULL
- Not null or an empty string
- Allowed ASCII: Letters (a-z, A-Z), numbers (0-9), and hyphens
- Allowed Unicode: characters >= 0x80, must be valid UTF8, must be IDN-mappable (that is, RtlIdnToNameprepUnicode succeeds; see RFC 3492)
- Names must not contain only numbers
- No spaces in the name
- Disallowed characters: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)

## Bulk rename devices

You can choose to rename devices in bulk, based on the device platform. The bulk rename option uses the same rules as renaming a single device. However, you must also include one of the following variables as part of the device name:

- **{{serialnumber}}** - Add the device's serial number to the name.
- **{{rand:x}}** - Add a random string of numbers, where x equals the number of digits to add.

To use the bulk rename action:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices** > **Bulk Device Actions**.
3. On the Basics page, for *OS* select the platform of the devices you want to rename, and then for *Device action* select **Rename**.
4. Complete the configuration wizard.

## Next steps

To see the status of the **Rename** device action, check the **Overview** page for the device.
