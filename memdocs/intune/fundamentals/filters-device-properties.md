---
# required metadata

title: Supported filter device properties and operators in Microsoft Intune
description: When using filters, get more information on the device properties, supported operators, and supported Windows OS SKUs, including examples. Use these features to create rule expressions in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/24/2023
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Device properties, operators, and rule editing when creating filters in Microsoft Intune

When you create an app, compliance policy, or configuration profile, you assign that app or policy to groups (users or devices). When you assign the app or policy, you can also use filters. For more information on this feature, see [Use filters when assigning your apps, policies, and profiles](filters.md).

When you create a filter, you enter the device properties to use in your filter. For example, in your filter, enter the device manufacturer so the policy only applies to Microsoft devices.

Advanced rule editing is also available. You can use common operators, such as `and`, `contains`, and `startsWith` to create expressions. These expressions are saved and used in your filter.

This article describes the different [device properties](#device-properties) and [operators](#supported-operators) you can use in your filters, and gives examples.

## Device properties

You can use the following device properties in your filter rules:

- **`deviceName` (Device Name)**: Create a filter rule based on the Intune device name property. Enter a string value for the device's full name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceName -eq "Scott's Device")`
  - `(device.deviceName -in ["Scott's device", "Sara's device"])`
  - `(device.deviceName -startsWith "S")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`manufacturer` (Manufacturer)**: Create a filter rule based on the Intune device manufacturer property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.manufacturer -eq "Microsoft")`
  - `(device.manufacturer -startsWith "Micro")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`model` (Model)**: Create a filter rule based on the Intune device model property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.model -eq "Surface Book 3")`
  - `(device.model -in ["Surface Book 3", "Surface Book 2"])`
  - `(device.model -startsWith "Surface Book")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`deviceCategory` (Device Category)**: Create a filter rule based on the Intune device category property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceCategory -eq "Engineering devices")`
  - `(device.deviceCategory -contains "Engineering")`
  - `(device.model -startsWith "E")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`osVersion` (OS Version)**: Create a filter rule based on the Intune device operating system (OS) version. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.osVersion -eq "14.2.1")`
  - `(device.osVersion -in ["10.15.3 (19D2064)","10.14.2 (18C54)"])`
  - `(device.osVersion -startsWith "10.0.18362")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`IsRooted` (Rooted or jailbroken)**: Create a filter rule based on the device's rooted (Android) or jailbroken (iOS/iPadOS) device property. Select `True`, `False`, or unknown values using the `-eq` and `-ne` operators.

  Example:

  - `(device.isRooted -eq "True")`

  This property applies to:

  - Android device administrator
  - Android Enterprise (Work profile only)
  - iOS/iPadOS

- **`deviceOwnership` (Ownership)**: Create a filter rule based on the device's ownership property in Intune. Select `Personal`, `Corporate`, or unknown values using the `-eq` and `-ne` operators. 

  Example:

  - `(device.deviceOwnership -eq "Personal")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 11
  - Windows 10

- **`enrollmentProfileName` (Enrollment profile name)**: Create a filter rule based on the enrollment profile name. This property is applied to a device when the device enrolls. It's a string value created by you, and matches the Windows Autopilot, Apple Automated Device Enrollment (ADE), or Google enrollment profile applied to the device. To see your enrollment profile names, sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Devices** > **Enroll devices**.

  Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.enrollmentProfileName -eq "DEP iPhones")`
  - `(device.enrollmentProfileName -startsWith "Autopilot Profile")`
  - `(device.enrollmentProfileName -ne $null)`

  This property applies to:

  - Android Enterprise
  - iOS/iPadOS
  - Windows 11
  - Windows 10

- **`deviceTrustType` (Azure AD Join type)**: Create a filter rule based on the device's Azure AD Join type. Choose between Azure AD Join, Hybrid Azure AD, Azure AD registered or unknown values (with `-eq`, `-ne`, `-in`, `-notIn` operators).

  Examples:

  - `(device.deviceTrustType -eq "Azure AD joined")`
  - `(device.deviceTrustType -ne "Azure AD registered")`
  - `(device.deviceTrustType -in ["Hybrid Azure AD joined","Azure AD joined"])`

  This property applies to:

  - Windows 11
  - Windows 10

- **`operatingSystemSKU` (Operating System SKU)**: Create a filter rule based on the device's Windows client OS SKU. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.operatingSystemSKU -eq "Enterprise")`
  - `(device.operatingSystemSKU -in ["Enterprise", "EnterpriseS", "EnterpriseN", "EnterpriseEval"])`
  - `(device.operatingSystemSKU -startsWith "Enterprise")`

  You can use the following supported values for the **Operating System SKU** property. The [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) doesn't show the SKU names. So, be sure to use the supported values in the following table:

  | Supported value | OS SKU definition |
  | ---- | --- |
  | **BusinessN** | Windows 10/11 Professional N (49) |
  | **CloudEdition** | CloudEdition (Windows 11 SE (203) |
  | **CloudEditionN** | CloudEditionN (Windows 11 SE N (202) |
  | **Core** | Windows 10/11 Home (10/111) |
  | **CoreCountrySpecific** | Windows 10/11 Home China (99) |
  | **CoreN** | Windows 10/11 Home N (98) |
  | **CoreSingleLanguage** | Windows 10/11 Home single language (100) |  
  | **Education** | Windows 10/11 Education (121) |
  | **EducationN**  | Windows 10/11 Education (122) |
  | **Enterprise** | Windows 10/11 Enterprise (4) |
  | **EnterpriseEval** | Windows 10/11 Enterprise Evaluation (72) |
  | **EnterpriseG** | Windows 10/11 Enterprise G (171) |
  | **EnterpriseGN** | Windows 10/11 Enterprise G N (172) |
  | **EnterpriseN** | Windows 10/11 Enterprise N (27) |
  | **EnterpriseNEval** | Windows 10/11 Enterprise N Evaluation (84) |
  | **EnterpriseS** | Windows 10 Enterprise LTSC (125) |
  | **EnterpriseSEval** | Windows 10 Enterprise LTSC Evaluation (129) |
  | **EnterpriseSN** | Windows 10 Enterprise LTSC N (126) |
  | **Holographic** | Windows 10 Holographic (136) |
  | **IoTUAP** | Windows 10 IoT Core (123) |
  | **IoTUAPCommercial** | Windows 10 IoT Core Commercial (131) |
  | **IoTEnterprise** | Windows 10/11 IoT Enterprise (188) |
  | **PPIPro** | Windows 10 TeamOS (119) |
  | **Professional** | Windows 10/11 Professional (48) |
  | **ProfessionalEducation** | Windows 10/11 Professional Education (164) |
  | **ProfessionalEducationN** | Windows 10/11 Professional Education N (165) |
  | **ProfessionalWorkstation** | Windows 10/11 Professional for workstation (161) |
  | **ProfessionalN** | Windows 10/11 Professional for workstation N (162) |
  | **ProfessionalSingleLanguage** | Windows 10/11 Professional Single Language (138) |
  | **ServerRdsh** | Windows 10/11 Enterprise multi-session (175) |

  This property applies to:

  - Windows 11
  - Windows 10

> [!TIP]
> Use the powershell command `Get-WmiObject -Class Win32_OperatingSystem |select operatingsystemSKU` from a Windows device to return the SKU number.

## Advanced rule editing

When you create a filter, you can manually create simple or complex rules in the rule syntax editor. You can also use common operators, such as `or`, `contains`, and more. The format is similar Azure AD dynamic groups: `([entity].[property name] [operation] [value])`.

### What you need to know

- The properties, operations, and values are case insensitive.
- Parentheses and nested parentheses are supported.
- You can use `Null` or `$Null` as a value with the `-Equals` and `-NotEquals` operators.
- Some advanced syntax options, such as nested parentheses, are only available in the rule syntax editor. If you use advanced expressions in the rule syntax editor, then the rule builder is disabled.

  For more information on the rule syntax editor and the rule builder, see [Use filters when assigning your apps, policies, and profiles](filters.md)

### Supported operators

You can use the following operators in the rule syntax editor:

- **Or**: Use for all value types, especially when grouping simple rules.

  - **Allowed values**: `-or` | `or`
  - **Example**: `(device.manufacturer -eq "Samsung") or (device.model -contains "Galaxy Note")`

- **And**: Use for all value types, especially when grouping simple rules.

  - **Allowed values**: `-and` | `and`
  - **Example**: `(device.manufacturer -eq "Samsung") and (device.model -contains "Galaxy Note")`

- **Equals**: Use for all value types, including simple rules, strings, arrays, and more.

  - **Allowed values**: `-eq` | `eq`
  - **Example**: `(device.manufacturer -eq "Samsung") and (device.model -eq "Galaxy Note")`

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

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported workloads when creating filters](filters-supported-workloads.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
