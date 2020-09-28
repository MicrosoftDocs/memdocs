---
# required metadata

title: Backup and restore iOS/iPadOS
titleSuffix: Microsoft Intune
description: Learn about backup and restore scenarios for iOS/iPadOS devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Backup and restore scenarios for iOS/iPadOS

You might have to backup and restore an Intune Automated Device Enrollment (ADE) managed iOS/iPadOS device during the setup assistant process. For example, when: 
- A device is factory reset and is then restored from a previous backup. 
- A user receives a new device and wants to migrate the data from the old device. 

To backup and restore an iOS/iPadOS device, you must follow the Apple instructions:
•	To backup your device, see [How to back up your iPhone, iPad and iPod touch](https://support.apple.com/HT203977).
•	To restore you device, see [Restore your iPhone, iPad, or iPod touch from a backup](https://support.apple.com/HT204184).
•	To transfer data to a new device, see [Use iCloud to transfer data from your previous iOS device to your new iPhone, iPad or iPod touch](https://support.apple.com/HT210217) or [Use Quick Start to transfer data to a new iPhone, iPad or iPod touch](https://support.apple.com/HT210216).

For more information about restoring Apple devices from backup, see [Get started using Apple Business Manager or Apple School Manager with Mobile Device Management](https://support.apple.com/HT207516).

## Restore a new device

When a user receives a new device they often want to restore data from the old device. All of the following scenarios have been tested with the new device completing the assigned Intune ADE enrollment profile:

| Old device enrolled with | New device enrolled with | Restore test completed |
| --- | --- | --- |
| Intune BYOD | ADE | Yes |
| Non-Intune BYOD | ADE | Yes |
| 3rd party MDM or other Intune tenant (BYOD or ADE) | ADE | Yes |

## Restore to the same device

If a device is factory reset for some reason, the user probably wants to restore their data. The important success factor here is how long it’s been since the last backup. If a device is restored from a backup taken weeks or months ago, it’s more likley that the restore can fail. If the management state of the device at the time of backup is still valid, it should return to the same state.  However, if the device was retired or the management certificate expired, the device will fail to check in.

## Expired management certificate

If the management certificate has expired since the last backup, upon restore the device won’t go through ADE enrollment. Instead, the device will simply be restored to whatever management state existed at the time of backup. 

| Device enrolled with | Restore to same device includes |
| --- | --- |
| Intune BYOD, non-supervised | Prior management profile. |
| Non-MDM | ADE |
| 3rd party MDM or other Intune tenant (BYOD or ADE) | ADE |

But what If you want to reset devices, let users restore them, and want them ADE enrolled? In this case, you should give them new devices. That way, they’ll be restoring to a different serial number from the backup. Therefore, they’ll be restoring to a new device and will see the behavior stated in that section above.

## Next steps

[Learn more about Automated Device Enrollment](device-enrollment-program-enroll-ios.md).


