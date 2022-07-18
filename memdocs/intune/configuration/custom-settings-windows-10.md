---
# required metadata

title: Add custom settings for Windows 10/11 devices in Microsoft Intune
description: Add or create a custom profile to use the OMA-URI settings for devices running Windows 10/11 client in Microsoft Intune. Use a custom profile to add custom settings.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/18/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Use custom settings for Windows 10/11 client devices in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes some of the different custom settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to configure settings that aren't built-in to Intune.

For more information on custom profiles, see [Create a profile with custom settings](custom-settings-configure.md).

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your Windows client devices.

This feature applies to:

- Windows 11
- Windows 10

Windows client custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features. These settings are typically used by mobile device manufacturers to control features on the device.

Windows client makes many Configuration Service Provider (CSP) settings available, such as [Policy Configuration Service Provider (Policy CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

If you're looking for a specific setting, remember that the [Windows 10/11 device restriction profile](device-restrictions-windows-10.md) includes many built-in settings. So, you may not need to enter custom values.

## Before you begin

[Create a Windows 10/11 custom profile](custom-settings-configure.md#create-the-profile).

## OMA-URI settings

**Add**: Enter the following settings:

- **Name**: Enter a unique name for the OMA-URI setting to help you identify it in the list of settings.
- **Description**: Enter a description that gives an overview of the setting, and any other important details.
- **OMA-URI** (case sensitive): Enter the OMA-URI you want to use as a setting.
- **Data type**: Select the data type you'll use for this OMA-URI setting. Your options:

  - Base64 (file)
  - Boolean
  - String (XML file)
  - Date and time
  - String
  - Floating point
  - Integer

- **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

## Find the policies you can configure

There's a complete list of all configuration service providers (CSPs) that Windows client supports in the [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference).

Not all settings are compatible with all Windows client versions. [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) tells you which versions are supported for each CSP.

Additionally, Intune doesn't support all the settings listed in [Configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference). To find out if Intune supports the setting you want, open the article for that setting. Each setting page shows its supported operation. To work with Intune, the setting must support the **Add**, **Replace**, and **Get** operations. If the value returned by the **Get** operation doesn't match the value supplied by the **Add** or **Replace** operations, then Intune reports a compliance error.
 
> [!NOTE]
> For settings that were created by using a string, base64, or XML data type, the stored value is obscured. If the user who is accessing the value has any of the following permissions or roles, they can see the value:
>
> - Create, Read, and Update permissions in a Microsoft Endpoint Manager role-based access control (RBAC) role.
> - Intune Service Administrator.
> - Global Administrator Azure Active Directory role.
> 
> For more information, see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Learn more about custom profiles in Intune](custom-settings-configure.md).
