---
# required metadata

title: Assignment filter reports and troubleshooting in Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Supported device properties when creating assignment filters in in Microsoft Endpoint Manager

## Device properties

- **Device Name**: Create a filter rule based on the Intune device name property. Enter a string value that's a device's full name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceName -eq "Scott's Device")`
  - `(device.deviceName -in ["Scott's device", "Sara's device"])`
  - `(device.deviceName -startsWith "S")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **Manufacturer**: Create a filter rule based on the Intune device manufacturer property. Enter a string value that's a manufacturer's full name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.manufacturer -eq "Microsoft")`
  - `(device.manufacturer -startsWith "Micro")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **Model**: Create a filter rule based on the Intune device model property. Enter a string value that's a device model's full name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.model -eq "Surface Book 3")`
  - `(device.model -in ["Surface Book 3", "Surface Book 2"])`
  - `(device.model -startsWith "Surface Book")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **Device Category**: Create a filter rule based on the Intune device category property. Enter a string value that's a category name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceCategory -eq "Engineering devices")`
  - `(device.deviceCategory -contains ["Engineering devices", "EMEA devices"])`
  - `(device.model -startsWith "E")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **OS Version**: Create a filter rule based on the Intune device Operating System version. Specify a string value for the OSversion (using -eq, -ne, -in, -notIn operators) or partial value (using -startswith, -contains, -notcontains operators).

  Examples:

  - `(device.osVersion -eq "14.2.1")`
  - `(device.osVersion -in ["10.15.3 (19D2064)","10.14.2 (18C54)"])`
  - `(device.osVersion -startsWith "10.0.18362")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **IsRooted**: Create a filter rule based on the device's Rooted (Android) or Jailbroken (iOS/iPadOS) device property. Choose between `True`, `False`, or unknown values using the `-eq` and `-ne` operators.

  Example:

  - `(device.isRooted -eq "True")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS

- **Device Ownership**: Create a filter rule based on the device's ownership property in Intune. Choose between `Personal`, `Corporate`, or unknown values using the `-eq` and `-ne` operators.

  Example:

  - `(device.deviceOwnership -eq "Personal")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10 and newer

- **Enrollment Profile Name**: Create a filter rule based on the name of the Enrollment Profile applied to a device during enrollment. Specify the full string value (using -eq, -ne, -in, -notIn operators) or partial value (using -startswith, -contains, -notcontains operators).

  Examples:

  - `(device.enrollmentProfileName -eq "DEP iPhones")`
  - `(device.enrollmentProfileName -startsWith "AutoPilot Profile")`

  This property applies to:

  - iOS/iPadOS
  - Windows 10 and newer

- **Operating System SKU**: Create a filter rule based on the device's Windows 10 Operating System SKU. Enter the full OS SKU name string value (using -eq, -ne, -in, -notIn operators) or partial value (using -startswith, -contains, -notcontains operators).

  Examples:

  - `(device.operatingSystemSKU -eq "Enterprise")`
  - `(device.operatingSystemSKU -in ["Enterprise", "EnterpriseS", "EnterpriseN", "EnterpriseEval"])`
  - `(device.operatingSystemSKU -startsWith "Enterprise")`

  This property applies to:

  - Windows 10 and newer

## Next steps
