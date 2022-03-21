---
# required metadata

title: Add custom settings to Windows Phone 8.1 devices in Microsoft Intune
titleSuffix:
description: Add or create a custom profile to use the OMA-URI settings for devices running Windows Phone 8.1 in Microsoft Intune.
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

ROBOTS: NOINDEX
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use custom settings for Windows Phone 8.1 devices in Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Using Microsoft Intune, you can add or create custom settings for your Windows Phone 8.1 devices using "custom profiles". Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

Windows Phone 8.1 custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features. These settings are typically used by mobile device manufacturers to control features on the device. [Windows Phone 8.1 MDM protocol documentation](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) lists the settings.

This article shows you how to create a custom profile for Windows Phone 8.1 devices. 

## Before you begin

[Create a Windows Phone 8.1 custom profile](custom-settings-configure.md).

## Custom OMA-URI settings

- **OMA-URI Settings**: **Add** the following settings:

  - **Name**: Enter a unique name for the OMA-URI setting to help you identify it in the list of settings.
  - **Description**: Enter a description that gives an overview of the setting, and any other relevant information to help you locate the profile.
  - **OMA-URI** (case sensitive): Enter the OMA-URI you want to use as a setting.
  - **Data type**: Select the data type you'll use for this OMA-URI setting. Your options:

    - String
    - String (XML file)
    - Date and time
    - Integer
    - Floating point
    - Boolean
    - Base64 (file)

  - **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

  After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

## Example

In the following example, Windows 8.1 phone devices are prevented from changing cellular networks when traveling outside the carrier coverage area.

- **Name**: Allow Cellular Data Roaming
- **Description**: Allow or disallow cellular data roaming
- **OMA-URI** (case sensitive): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Data type**: Integer
- **Value**: 0

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

Create a [custom profile on Windows 10/11 devices](custom-settings-windows-10.md).
