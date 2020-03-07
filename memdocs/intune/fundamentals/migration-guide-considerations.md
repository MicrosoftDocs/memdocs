---
# required metadata

title: Special migration considerations
titleSuffix: Microsoft Intune
description: This article provides special migration considerations before you start a migration campaign to Microsoft Intune.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: f29d2894-e98b-4f2c-b444-a8ccc1b7efdd

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Special migration considerations

There are special migration considerations that may apply depending on your existing MDM provider environment.

## Wipe for Apple’s Device Enrollment Program (DEP)

The Apple Device Enrollment Program (DEP) sets device configurations that cannot be removed by the end user. To retain the advanced management features of DEP, the device must be returned to the out-of-box (new) state by wiping it to enroll it into Intune.

To continue using DEP to manage the devices in Intune, [set up iOS/iPadOS device enrollment with Device Enrollment Program](../enrollment/device-enrollment-program-enroll-ios.md).


## Next steps

[Phase 2: Migration campaign](../migration-guide-campaign.md)
