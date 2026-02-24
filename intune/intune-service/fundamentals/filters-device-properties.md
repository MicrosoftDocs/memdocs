---
title: Assignment filter properties and operators reference
description: Reference guide for device and app properties, operators, and rule syntax when creating assignment filters in Microsoft Intune. Includes examples and supported values.
author: MandiOhlinger
ms.author: mandia
ms.date: 02/24/2026
ms.topic: reference
ms.reviewer: mattcall
ms.collection:
- M365-identity-device-management
---

# App and device properties, operators, and rule editing when creating assignment filters in Microsoft Intune

[Assignment filters in Intune](filters.md) let you refine app and policy targeting based on device and app properties. This reference article describes the properties, operators, and rule syntax you can use when creating filters for managed devices and managed apps.

When you create an app, compliance policy, or configuration profile, you assign that app or policy to groups (users or devices). Assignment filters allow you to narrow the scope of your assignments based on specific criteria.

You can use assignment filters on **managed devices** (devices enrolled in Intune) and **managed apps** (apps managed by Intune). When creating a filter, you specify properties like device manufacturer, OS version, or enrollment profile, and use operators to build rule expressions, like `startsWith` and `contains`.

This article provides a complete reference for managed device properties, managed app properties, and supported operators you can use in your assignment filters, and includes practical examples.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Available properties

You can use assignment filters on **managed devices** (devices enrolled in Intune) and **managed apps** (apps managed by Intune). This section lists the available properties.

# [Managed device properties](#tab/managed-device)

You can use the following device properties in your managed device filter rules:

- **`cpuArchitecture` (CPU Architecture)**: Create a filter rule based on the Intune device CPU architecture property.

  For Windows, your options are (with `-eq`, `-ne`, `-in`, `-notIn` operators):

  - amd64
  - x86
  - arm64
  - unknown

  For macOS, your options are (with `-eq`, `-ne`, `-in`, `-notIn` operators):

  - x64
  - arm64
  - unknown

  Examples:

  - `(device.cpuArchitecture -eq "arm64")`
  - `(device.cpuArchitecture -in ["x64", "arm64"])`
  - `(device.cpuArchitecture -eq "unknown")`

  This property applies to:

  - macOS
  - Windows

  > [!NOTE]
  > Currently, enrollment scenarios don't support the `cpuArchitecture` property. Support will be added in a future update (no ETA).

- **`deviceCategory` (Device Category)**: Create a filter rule based on the Intune device category property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceCategory -eq "Engineering devices")`
  - `(device.deviceCategory -contains "Engineering")`
  - `(device.model -startsWith "E")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **`deviceManagementType` (Device Management Type)**: Create a filter rule based on the Intune device management type. Select from the following values using the `-eq` and `-ne` operators:

  | Value | Supported platforms |
  |-----------|------------------------|
  | `Corporate-owned dedicated devices with Entra ID Shared mode` | Android |
  | `Corporate-owned dedicated devices without Entra ID Shared mode` | Android |
  | `Corporate-owned with work profile` | Android |
  | `Corporate-owned fully managed` | Android |
  | `Personally-owned work profile` | Android |
  | `AOSP user-associated devices` | Android |
  | `AOSP userless devices` | Android |

  Example:

  - `(app.deviceManagementType -eq "Corporate-owned dedicated devices without Entra ID Shared mode")`

  This property applies to:

  - Android Enterprise
  - Android (AOSP)

- **`deviceName` (Device Name)**: Create a filter rule based on the Intune device name property. Enter a string value for the device's full name (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.deviceName -eq "Scott's Device")`
  - `(device.deviceName -in ["Scott's device", "Sara's device"])`
  - `(device.deviceName -startsWith "S")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **`deviceOwnership` (Ownership)**: Create a filter rule based on the device's ownership property in Intune. Select `Personal`, `Corporate`, or unknown values using the `-eq` and `-ne` operators.

  Example:

  - `(device.deviceOwnership -eq "Personal")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **`deviceTrustType` (Microsoft Entra join type)**: Create a filter rule based on the device's Microsoft Entra join type. Choose between Azure AD joined, Azure AD registered, Hybrid Azure AD joined,  or Unknown values (with `-eq`, `-ne`, `-in`, `-notIn` operators).

  Examples:

  - `(device.deviceTrustType -eq "Azure AD joined")`
  - `(device.deviceTrustType -ne "Azure AD registered")`
  - `(device.deviceTrustType -in ["Hybrid Azure AD joined","Azure AD joined"])`

  This property applies to:

  - Windows

  > [!NOTE]
  > The `deviceTrustType` property exists in Microsoft Entra ID and Intune. The values in this Intune assignment filters article apply to Intune. They don't apply to Microsoft Entra ID.

- **`enrollmentProfileName` (Enrollment profile name)**: Create a filter rule based on the enrollment profile name. This property is applied to a device when the device enrolls. It's a string value created by you, and matches the Windows Autopilot, Apple Automated Device Enrollment (ADE), or Google enrollment profile applied to the device. To see your enrollment profile names, sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Devices** > **Enroll devices**.

  Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.enrollmentProfileName -eq "DEP iPhones")`
  - `(device.enrollmentProfileName -startsWith "Autopilot Profile")`
  - `(device.enrollmentProfileName -ne $null)`

  This property applies to:

  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - Windows

- **`IsRooted` (Rooted or jailbroken)**: Create a filter rule based on the device's rooted (Android) or jailbroken (iOS/iPadOS) device property. Select `True`, `False`, or unknown values using the `-eq` and `-ne` operators.

  Example:

  - `(device.isRooted -eq "True")`

  This property applies to:

  - Android device administrator
  - Android Enterprise (Work profile only)
  - Android (AOSP)
  - iOS/iPadOS

- **`manufacturer` (Manufacturer)**: Create a filter rule based on the Intune device manufacturer property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.manufacturer -eq "Microsoft")`
  - `(device.manufacturer -startsWith "Micro")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **`model` (Model)**: Create a filter rule based on the Intune device model property. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  For iOS/iPadOS and macOS devices, use the model, not the product name. Only the model is recognized for Apple devices. For example, for iPhone 8 devices, enter the model as `iPhone 8`.

  Examples:

  - `(device.model -eq "Surface Book 3")`
  - `(device.model -in ["Surface Book 3", "Surface Book 2"])`
  - `(device.model -startsWith "Surface Book")`
  - `(device.model -startsWith "MacBookPro")`
  - `(device.model -startsWith "iPhone 8")`

  > [!NOTE]
  > Older iPad Pro models use the double prime symbol (`"`) instead of inch. If you use full string value operators, this symbol can cause assignment filters to not evaluate correctly. For these models, use partial value operators to ensure that assignment filters evaluate the model as intended. For example, for `iPad Pro (12.9")(2nd generation)` model devices, you can use `(device.model -contains "iPad Pro 12.9")` and `(device.model -contains "(2nd generation)")`.

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **`operatingSystemVersion` (Operating System Version)**: Create a filter rule based on the Intune device operating system (OS) version. Enter a version value (using `-eq`, `-ne`, `-gt`, `-ge`, `-lt`, `-le` operators).

  Examples:

  - `(device.operatingSystemVersion -eq 14.2.1)`
  - `(device.operatingSystemVersion -gt 10.0.22000.1000)`
  - `(device.operatingSystemVersion -le 10.0.22631.3235)`

  For a list of supported operators, go to [Supported operators for operatingSystemVersion](#supported-operators-for-operatingsystemversion) (in this article).

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

  > [!NOTE]
  > The `operatingSystemVersion` property is in public preview. For more information on what that means, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

- **`osVersion` (OS Version)**: Create a filter rule based on the Intune device operating system (OS) version. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  > [!TIP]
  > The `osVersion` property is being deprecated. Instead, use the `operatingSystemVersion` property. When `operatingSystemVersion` is generally available (GA), the `osVersion` property will retire, and you won't be able to create new assignment filters using this property. Existing assignment filters that use `osVersion` continue to work.

  Examples:

  - `(device.osVersion -eq "14.2.1")`
  - `(device.osVersion -in ["10.15.3 (19D2064)","10.14.2 (18C54)"])`
  - `(device.osVersion -startsWith "10.0.18362")`

  This property applies to:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

  > [!NOTE]
  > For Apple devices, the `OSversion` property doesn't include Apple's Security Patch Version (SPV) information. The SPV is the letter after the version number, like `14.1.2a`. When creating assignment filters for Apple devices, don't include the SPV in the `OSversion` rule syntax.

- **`operatingSystemSKU` (Operating System SKU)**: Create a filter rule based on the device's Windows client OS SKU. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(device.operatingSystemSKU -eq "Enterprise")`
  - `(device.operatingSystemSKU -in ["Enterprise", "EnterpriseS", "EnterpriseN", "EnterpriseEval"])`
  - `(device.operatingSystemSKU -startsWith "Enterprise")`

  You can use the following supported values for the **Operating System SKU** property. The [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) doesn't show the SKU names. So, be sure to use the supported values in the following table:

  | Supported value | OS SKU definition |
  | ---- | --- |
  | **BusinessN** | Windows 10/11 Professional N (49) |
  | **CloudEdition** | CloudEdition (Windows 11 SE (203)) |
  | **CloudEditionN** | CloudEditionN (Windows 11 SE N (202)) |
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

  - Windows

> [!NOTE]
>
> - In Windows PowerShell, use the `Get-WmiObject -Class Win32_OperatingSystem |select operatingsystemSKU` command on a Windows device to return the SKU number.
> - [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

# [Managed app properties](#tab/managed-app)

You can use the following app properties in your managed app filter rules:

- **`appVersion` (App Version)**: Create a filter rule based on the client reported application version. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(app.appVersion -eq "14.2.1")`
  - `(app.appVersion -in ["10.15.3","10.14.2"])`
  - `(app.appVersion -startsWith "10.0")`

  This property applies to:

  - Android
  - iOS/iPadOS
  - Windows

- **`deviceManagementType` (Device Management Type)**: Create a filter rule based on the Intune device management type. Select from the following values using the `-eq` and `-ne` operators:

  | Value | Supported platforms |
  |-----------|------------------------|
  | `Unmanaged` | Android <br/>iOS/iPadOS |
  | `Android device administrator` | Android |
  | `AOSP userless devices` | Android |
  | `AOSP user-associated devices` | Android |
  | `Corporate-owned dedicated devices with Entra ID Shared mode` | Android |
  | `Corporate-owned dedicated devices without Entra ID Shared mode` | Android |
  | `Corporate-owned with work profile` | Android |
  | `Corporate-owned fully managed` | Android |
  | `Personally-owned work profile` | Android |
  | `Android Enterprise` (deprecated) | Android |
  | `Automated Device Enrollment user-associated devices` | iOS/iPadOS |
  | `Automated Device Enrollment userless devices` | iOS/iPadOS |
  | `Account Driven User Enrollment` | iOS/iPadOS |
  | `Device Enrollment with Company Portal and Web Enrollment` | iOS/iPadOS |
  | `Managed` (deprecated) | iOS/iPadOS |

  Example:

  - `(app.deviceManagementType -eq "Unmanaged")`
  - `(app.deviceManagementType -eq "Corporate-owned dedicated devices without Entra ID Shared mode")`
  - `(app.deviceManagementType -ne "Android device administrator")`

  This property applies to:

  - Android
  - iOS/iPadOS

  > [!IMPORTANT]
  > - The `Managed` for iOS/iPadOS and the `Android Enterprise` values are deprecated and will be removed in a future update (no ETA). If you have existing assignment filters that use these values, they're automatically mapped to the other existing values for that platform. For example, `Managed` might be mapped to `Automated Device Enrollment userless devices` for your iOS/iPadOS kiosk devices.
  > - For the automatic mapping to work correctly, devices must be registered with Microsoft Entra and have a Microsoft Entra Device ID. If the devices don't meet these requirements, the app assignment filters won't match to the more granular management types. You can use an Intune [app configuration policy](../apps/app-configuration-policies-managed-app.md#add-an-app-configuration-policy-for-managed-apps-on-iosipados-and-android-devices) to force Microsoft Entra device registration with the `com.microsoft.intune.mam.IntuneMAMOnly.RequireAADRegistration=Enabled` key.
  > - If the device is MDM-managed by a third-party or partner service, the managed app assignment filters won't match to the more granular management types.

- **`deviceManufacturer` (Manufacturer)**: Create a filter rule based on the client reported device manufacturer. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(app.deviceManufacturer -eq "Microsoft")`
  - `(app.deviceManufacturer -startsWith "Micro")`

  This property applies to:

  - Android
  - iOS/iPadOS
  - Windows

- **`deviceModel` (Model)**: Create a filter rule based on the client reported device model. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  Examples:

  - `(app.deviceModel -eq "Surface Duo")`
  - `(app.deviceModel -in ["Surface Duo", "Surface Duo 2"])`
  - `(app.deviceModel -startsWith "Surface Duo")`
  - `(app.deviceModel -startsWith "RealityDevice")`

  This property applies to:

  - Android
  - iOS/iPadOS/visionOS
  - Windows

  > [!NOTE]
  > The `app.deviceModel -startsWith "RealityDevice"` property is in preview and is only supported on the Microsoft Teams app. If your app protection policy is targeted to the iOS/iPadOS platform, it also applies to visionOS. However, when targeting specific conditional launch settings to visionOS, like **Min/Max OS version** or **Min app version**, you can use the app property `app.deviceModel -startsWith "RealityDevice"` in your managed app filter rules.

- **`operatingSystemVersion` (Operating System Version)**: Create a filter rule based on the Intune device operating system (OS) version. Enter a version value (using `-eq`, `-ne`, `-gt`, `-ge`, `-lt`, `-le` operators).

  Examples:

  - `(app.operatingSystemVersion -eq 14.2.1)`
  - `(app.operatingSystemVersion -gt 10.0.22000.1000)`
  - `(app.operatingSystemVersion -le 10.0.22631.3235)`

  For a list of supported operators, go to [Supported operators for operatingSystemVersion](#supported-operators-for-operatingsystemversion) (in this article).

  This property applies to:

  - Android
  - iOS/iPadOS
  - Windows

  > [!NOTE]
  > The `operatingSystemVersion` property is in public preview. For more information on what that means, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

- **`osVersion` (OS Version)**: Create a filter rule based on the client reported operating system (OS) version. Enter the full string value (using `-eq`, `-ne`, `-in`, `-notIn` operators), or partial value (using `-startswith`, `-contains`, `-notcontains` operators).

  > [!TIP]
  > The `osVersion` property is being deprecated. Instead, use the `operatingSystemVersion` property. When `operatingSystemVersion` is generally available (GA), the `osVersion` property will retire, and you won't be able to create new assignment filters using this property. Existing assignment filters that use `osVersion` continue to work.

  Examples:

  - `(app.osVersion -eq "14.2.1")`
  - `(app.osVersion -in ["10.15.3","10.14.2"])`
  - `(app.osVersion -startsWith "10.0")`

  This property applies to:

  - Android
  - iOS/iPadOS
  - Windows

---

## Advanced rule editing

When you create a filter, you can manually create simple or complex rules in the rule syntax editor. You can also use common operators, such as `or`, `contains`, and more. The format is similar to Microsoft Entra dynamic groups: `([entity].[property name] [operation] [value])`.

### What you need to know

- The properties, operations, and values are case insensitive.
- Parentheses and nested parentheses are supported.
- You can use `Null` or `$Null` as a value with the `-Equals` and `-NotEquals` operators.
- Some advanced syntax options, such as nested parentheses, are only available in the rule syntax editor. If you use advanced expressions in the rule syntax editor, then the rule builder is disabled.

  For more information on the rule syntax editor and the rule builder, go to [Use filters when assigning your apps, policies, and profiles](filters.md)

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

#### Supported operators for operatingSystemVersion

When you use the `operatingSystemVersion (Operating System Version)` property, you can use the following operators in the rule syntax editor:

- **Equals**: Use for all value types, including simple rules, strings, arrays, and more.

  - **Allowed values**: `-eq` | `eq`
  - **Example**: `(device.operatingSystemVersion -eq "10.0.22000.1000")`

- **NotEquals**: Use for all value types, including simple rules, strings, arrays, and more.

  - **Allowed values**: `-ne` | `ne`
  - **Example**: `(device.operatingSystemVersion -ne "10.0.22000.1000")`

- **GreaterThan**: Use for version value types.

  - **Allowed values**: `-gt` | `gt`
  - **Example**: `(device.operatingSystemVersion -gt 10.0.22000.1000)`

- **LessThan**: Use for version value types.

  - **Allowed values**: `-lt` | `lt`
  - **Example**: `(device.operatingSystemVersion -lt 10.0.22000.1000)`

- **GreaterThanOrEquals**: Use for version value types.

  - **Allowed values**: `-ge` | `ge`
  - **Example**: `(device.operatingSystemVersion -ge 10.0.22000.1000)`

- **LessThanOrEquals**: Use for version value types.

  - **Allowed values**: `-le` | `le`
  - **Example**: `(device.operatingSystemVersion -le 10.0.22000.1000)`

## Related articles

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported workloads when creating assignment filters](filters-supported-workloads.md)
- [Filter performance recommendations](filters-performance-recommendations.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
