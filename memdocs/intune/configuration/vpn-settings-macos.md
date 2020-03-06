---
# required metadata

title: Configure VPN settings to macOS devices in Microsoft Intune - Azure | Microsoft Docs
description: Add or create a virtual private network (VPN) configuration profile, including the connection details, split tunneling, custom VPN settings with the identifier, key and value pairs, proxy settings with a configuration script, IP or FQDN address, and TCP port in Microsoft Intune on devices running macOS.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add VPN settings on macOS devices in Microsoft Intune



This article shows you the Intune settings you can use to configure VPN connections on devices running macOS.

Depending on the settings you choose, not all values in the following list are configurable.

## Before you begin

[Create a device configuration profile](vpn-settings-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Base VPN settings

**Connection name**: Enter a name for this connection. End users see this name when they browse their device for the list of available VPN connections.
- **IP address or FQDN**: Provide the IP address or fully qualified domain name of the VPN server that devices connect to. Examples: **192.168.1.1**, **vpn.contoso.com**.
- **Authentication method**: Choose how devices authenticate to the VPN server from:
  - **Certificates**: Under **Authentication certificate**, Choose a SCEP or PKCS certificate profile you previously created to authenticate the connection. For more information about certificate profiles, see [How to configure certificates](../protect/certificates-configure.md).
  - **Username and password**: End users must supply a username and password to log into the VPN server.
- **Connection type**: Select the VPN connection type from the following list of vendors:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**
  - **Custom VPN**
- **Split tunneling**: **Enable** or **Disable** this option that lets devices decide which connection to use depending on the traffic. For example, a user in a hotel uses the VPN connection to access work files, but use the hotel's standard network for regular web browsing.

<!--- **Per-app VPN** - Select this option if you want to associate this VPN connection with an iOS/iPadOS or macOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md). --->

## Custom VPN settings

If you selected **Custom VPN**, configure these further settings:

- **VPN identifier**: Enter an identifier for the VPN app you're using. This identifier is supplied by your VPN provider.
- **Enter key and value pairs for the custom VPN attributes**: Add or import **Keys** and **Values** that customize your VPN connection. These values are typically supplied by your VPN provider.

## Proxy settings

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`.
- **Address**: Enter the proxy server address (as an IP address).
- **Port number**: Enter the port number associated with the proxy server.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md), and [Windows 10](vpn-settings-windows-10.md) devices.
