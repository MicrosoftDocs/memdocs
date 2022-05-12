---
# required metadata

title: Common tasks and features you can configure using settings catalog in Microsoft Intune
description: Use the settings catalog in Microsoft Intune and Endpoint Manager to configure common features. For example, you can create a Universal Print policy, configure Microsoft Edge and Google Chrome web browser, and use built in settings instead of plist files for macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/23/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz, mikedano, beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Tasks you can complete using the Settings Catalog in Intune

Using the [settings catalog](settings-catalog.md) in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can access many settings that manage apps and features on your devices.

This article lists and describes some of the features you can configure. For more information on the settings catalog, and what it is, go to [Use the settings catalog to configure settings on Windows and macOS devices](settings-catalog.md). To see all the settings you can configure, create a settings catalog policy.

This feature applies to:

- macOS
- Windows 11
- Windows 10

## Configure Microsoft Edge and Google Chrome

<!-- ms.reviewer: mikedano -->

These web browser settings are built in, and can be configured & deployed to your managed devices. on Windows devices, you can also configure Google Chrome:

:::image type="content" source="./media/settings-catalog-common-features/google-chrome-settings.png" alt-text="In Settings Catalog, Google Chrome settings are built in to Microsoft Intune and Endpoint Manager admin center. Use these settings to create and configure a Google Chrome policy on Windows devices.":::

This feature applies to:

- macOS
- Windows 11
- Windows 10

## Add universal printers

<!-- ms.reviewer: laarrizz -->

You can create a universal print policy, add printers, and then deploy this printer list to your managed users. When the policy is deployed, it automatically installs the printers you added. Users can see these printers, and select a printer from your list.

For more information, go to [Create a Universal Print policy in Microsoft Intune](settings-catalog-printer-provisioning.md).

This feature applies to:

- Windows 11
- Windows 10

## Built-in macOS features replacing plist files

<!-- ms.reviewer: beflamm -->

Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then it's recommended to continue using the [preference file](preference-file-settings-macos.md).

- **Configure Microsoft Edge version 77 and newer**. Previously, you had to [use a property list (plist) file](/deployedge/configure-microsoft-edge-on-mac) (opens another Microsoft website). For a list of the settings you can configure, see [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies) (opens another Microsoft website). 

- **Configure Microsoft Defender for Endpoint**. Previously, you had to [use a property list (plist) file](/microsoft-365/security/defender-endpoint/mac-install-with-intune) (opens another Microsoft website). For a list of the settings you can configure, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) (opens another Microsoft website).

This feature applies to:

- macOS

## Learn more

- [Use the settings catalog to configure settings on Windows and macOS devices](settings-catalog.md)
- [Create a Universal Print policy in Microsoft Intune](settings-catalog-printer-provisioning.md)
