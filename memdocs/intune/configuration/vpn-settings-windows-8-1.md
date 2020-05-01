---
# required metadata

title: Configure VPN settings on Windows 8.1 devices in Microsoft Intune - Azure | Microsoft Docs
description: Add or create a VPN configuration profile using virtual private network (VPN) configuration settings, including the connection details, and the proxy settings to include IP or FQDN address, and TCP port in Microsoft Intune on devices running Windows 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add VPN settings on Windows 8.1 devices in Microsoft Intune

This article shows you the Intune settings you can use to configure VPN connections on devices running Windows 8.1.

Depending on the settings you choose, not all values in the following list are configurable.

## Before you begin

[Create a device configuration profile](vpn-settings-configure.md).

## Base VPN settings

- **Apply all settings to Windows 8.1 only**: Configure this setting in the Intune classic portal. In the Microsoft Endpoint Manager admin center, this setting can't be changed. When set to **Configured**, any settings are only applied to Windows 8.1 devices. When set to **Not Configured**, these settings also apply to Windows 10 devices.
- **Connection name**: Enter a name for this connection. Users see this name when they browse their device for the list of available VPN connections.
- **Servers**: Add one or more VPN servers that devices connect to.
  - **Add**: Opens the **Add Row** page where you can specify the following information:
    - **Description**: Specify a descriptive name for the server like **Contoso VPN server**.
    - **IP address or FQDN**: Provide the IP address or fully qualified domain name of the VPN server that devices connect to. Examples: **192.168.1.1**, **vpn.contoso.com**.
    - **Default server**: Enables this server as the default server that devices use to establish the connection. Make sure to set only one server as the default.
  - **Import**: Browse to a comma-separated file with the list of servers in the format description, IP address or FQDN, Default server. Choose **OK** to import these servers into the **Servers** list.
  - **Export**: Exports the list of servers to a comma-seperated-values (csv) file.

- **Connection type**: Select the VPN connection type from the following list of vendors:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Login group or domain** (SonicWall Mobile Connect only): Specify the name of the login group or domain that you want to connect to.

- **Role** (Pulse Secure only): Specify the name of the user role that has access to this connection. A user role defines personal settings and options, and it enables or disables certain access features.

- **Realm** (Pulse Secure only): Specify the name of the authentication realm that you want to use. An authentication realm is a grouping of authentication resources that the Pulse Secure connection type uses.

- **Custom XML**: Specify any custom XML commands that configure the VPN connection.

  **Pulse Secure example**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **CheckPoint Mobile VPN example**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWall Mobile Connect example**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client example**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  For more information on writing custom XML commands, see the manufacturer's VPN documentation.

- **Split tunneling**: **Enable** lets devices decide which connection to use depending on the traffic. For example, a user in a hotel uses the VPN connection to access work files, but use the hotel's standard network for regular web browsing. If you want all traffic to use the VPN tunnel when the VPN connection is active, then set to **Disable**.

## Proxy settings

- **Automatically detect proxy settings**: If your VPN server requires a proxy server for the connection, specify whether you want devices to automatically detect the connection settings.
- **Automatic configuration script**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`.
- **Use proxy server**: Enable this option if you want to manually enter the proxy server settings.
  - **Address**: Enter the proxy server address (as an IP address).
  - **Port number**: Enter the port number associated with the proxy server.
- **Bypass proxy for local addresses**: If your VPN server requires a proxy server for the connection, and you don't want to use the proxy server for local addresses you enter, then select this option.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md), and [Windows 10](vpn-settings-windows-10.md) devices.
