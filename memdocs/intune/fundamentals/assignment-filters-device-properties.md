---
# required metadata

title: Assignment filter reports and troubleshooting in Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2021
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

# Supported device properties when creating assignment filters in Microsoft Endpoint Manager

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

## Finding the right property values to create a filter
Most filter properties are viewable in the Devices section of the MEM admin center, either in all devices list or by viewing the detailed device page – this makes it easy to craft the right filter expressions for including or excluding those devices.  There are some properties, however that are not currently shown including:

- **Enrollment profile name**: This property is applied to a device during the enrollment process and is an admin-defined string matching the Windows autopilot, Apple ADE or Google enrollment profile applied to the device. You can view the enrollment profile names under the Devices > Enroll devices section of the MEM admin center.
- **Operating System SKU** (Windows 10 only): The Endpoint Manager admin center currently lists a “SKU Family” for Windows 10 devices in the device details section. It doesn't show the specific SKU. The following table shows the values that can be used in a filter (column 1).

  | Value | SKU name |
  | ---- | --- |
  | **Education** | Windows 10 Education (SKU 121) |
  | **EducationN**  | Windows 10 Education (SKU 122) |
  | **Enterprise** | Windows 10 Enterprise  (SKU 4) |
  | **EnterpriseEval** | Windows 10 Enterprise Evaluation (SKU 72) |
  | **EnterpriseG** | Windows 10 Enterprise G  (SKU 171) |
  | **EnterpriseGN** | Windows 10 Enterprise G N (SKU 172) |
  | **EnterpriseS** | Windows 10 Enterprise LTSB (SKU 125) |
  | **EnterpriseSEval** | Windows 10 Enterprise LTSB Evaluation (SKU 129) |
  | **EnterpriseSN** | Windows 10 Enterprise LTSB N  (SKU 162) |
  | **ServerRdsh** | Windows 10 Enterprise Multi-session (SKU 175) |
  | **EnterpriseN** | Windows 10 Enterprise N (SKU 27) |
  | **EnterpriseNEval** | Windows 10 Enterprise N Evaluation (SKU 84) |
  | **Holographic** | Windows 10 Holographic (SKU 136) |
  | **Core** | Windows 10 Home (SKU 101) |
  | **CoreCountrySpecific** | Windows 10 Home China (SKU 99) |
  | **CoreN** | Windows 10 Home N (SKU 98) |
  | **CoreSingleLanguage** | Windows 10 Home single language (SKU 100) |
  | **IoTUAP** | Windows 10 IoT Core  (SKU 123) |
  | **IoTUAPCommercial** | Windows 10 IoT Core Commercial (SKU 131) |
  | **IoTEnterprise** | Windows 10 IoT Enterprise (SKU 188) |
  | **Professional** | Windows 10 Professional  (SKU 48) |
  | **ProfessionalEducation** | Windows 10 Professional Education (SKU 164) |
  | **ProfessionalEducationN** | Windows 10 Professional Education N (SKU 165) |
  | **ProfessionalWorkstation** | Windows 10 Professional for workstation  (SKU 161) |
  | **ProfessionalN** | Windows 10 Professional for workstation N (SKU 162) |
  | **BusinessN** | Windows 10 Professional N  (SKU 49) |
  | **ProfessionalSingleLanguage** | Windows 10 Professional Single Language (SKU 138) |
  | **PPIPro** | Windows 10 TeamOS (SKU 119) |

## Advanced rule editing

The assignment filter rule creation experience uses a similar syntax to Azure AD dynamic groups where a format of `([entity].[property name] [operation] [value])` is used.

- Properties, operations and values in rules are case insensitive.
- Parentheses and nested parentheses are supported.

### Supported operators

Some advanced syntax options, such as nested parentheses, are only available in the advanced editing experience. If you use advanced syntax in the advanced editor, then the basic editing experience is disabled.

- **Or**: Use for all value types, especially when grouping simple rules.

  - **Allowed values**: `-or` | `or`
  - **Example**: `(device.manufacturer -eq "Samsung") or (device.model -contains "Galaxy Note")`

- **And**: Use for all value types, especially when grouping simple rules.

  - **Allowed values**: `-and` | `and`
  - **Example**: `(device.manufacturer -eq "Samsung") and (device.model -contains "Galaxy Note")`

- **Equals**: Use for all value types, including simple rules, strings, arrays, and more.

  - **Allowed values**: `-eq` | `eq`
  - **Example**: `(device.manufacturer -eq "Samsung") and (device.model -contains "Galaxy Note")`

- **NotEquals**: Use for all value types, including simple rules, strings, arrays, and more.

  - **Allowed values**: `-ne` | `ne`
  - **Example**: `(device.manufacturer -ne "Samsung") or (device.model -ne "Galaxy Note")`

- **StartsWith**: Use for string value types.

  - **Allowed values**: `-startsWith` | `startsWith`
  - **Example**: `(device.manufacturer -startsWith "Sams")`

- **In**: Use for array value types, such as `["1", "2"]`.

  - **Allowed values**: `-in` | `in`
  - **Example**: `(device.manufacturer -in ["Samsung","Lenovo","Microsoft"])`

- **NotIn**: Use for array value types, such as `["1", "2"]`.

  - **Allowed values**: `-notIn` | `notIn`
  - **Example**: `(device.manufacturer -notIn ["Samsung","Lenovo","Microsoft"])`

- **Contains**: Use for string value types.

  - **Allowed values**: `-contains` | `contains`
  - **Example**: `(device.manufacturer -contains "Samsung")`

- **NotContains**: Use for string value types.

  - **Allowed values**: `-notContains` | `notContains`
  - **Example**: `(device.manufacturer -notContains "Samsung")`

## Next steps
