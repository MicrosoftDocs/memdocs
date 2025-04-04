---
# required metadata

title: Add custom settings for Windows 10/11 devices in Microsoft Intune
description: Add or create a custom profile to use the OMA-URI settings for devices running Windows 10/11 client in Microsoft Intune. Use a custom profile to add custom settings.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/25/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Use custom settings for Windows client devices in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes some of the different custom settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to configure settings that aren't built in to Intune.

For more information on custom profiles, go to [Create a profile with custom settings](custom-settings-configure.md).

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your Windows client devices.

This feature applies to:

- Windows 11
- Windows 10

Windows client custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features. These settings are typically used by mobile device manufacturers to control features on the device.

Windows client makes many Configuration Service Provider (CSP) settings available, such as [Policy Configuration Service Provider (Policy CSP)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

If you're looking for a specific setting, the [Windows device restriction profile](device-restrictions-windows-10.md) and the [Settings catalog](settings-catalog.md) include many built-in settings. So, you may not need to enter custom values.

## Before you begin

- [Create a Windows custom profile](custom-settings-configure.md#create-the-profile).

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

After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (`.csv`) file.

## Find the policies you can configure

For a complete list of all configuration service providers (CSPs) that Windows client supports, go to the [CSP reference](/windows/client-management/mdm/configuration-service-provider-reference).

Not all settings are compatible with all Windows client versions. The [CSP reference](/windows/client-management/mdm/configuration-service-provider-reference) lists the supported versions for each CSP.

Also, Intune doesn't support all the settings listed in [CSP reference](/windows/client-management/mdm/configuration-service-provider-reference). To find out if Intune supports the setting you want, open the article for that setting. Each setting page shows its supported operation. To work with Intune, the setting must support the **Add**, **Replace**, and **Get** operations. If the value returned by the **Get** operation doesn't match the value supplied by the **Add** or **Replace** operations, then Intune reports a compliance error.

> [!NOTE]
> For settings created using a string, base64, or XML data type, the stored value is obscured. If the user who is accessing the value has any of the following permissions or roles, they can see the value:
>
> - A Microsoft Intune role that has the **Device configurations** > **Create**, **Read**, and **Update** permissions, like the **Policy and Profile manager** Intune built-in role.
> - Intune Administrator Microsoft Entra role
>
> For more information, go to:
> - [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md)
> - [Microsoft Entra built-in roles - Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Learn more about custom profiles in Intune](custom-settings-configure.md).
