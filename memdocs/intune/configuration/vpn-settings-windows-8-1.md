---
# required metadata

title: Configure VPN settings on Windows 8.1 devices in Microsoft Intune
description: Add or create a VPN configuration profile using virtual private network (VPN) configuration settings, including the connection details, and the proxy settings to include IP or FQDN address, and TCP port in Microsoft Intune on devices running Windows 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/20/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add VPN settings on Windows 8.1 devices in Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

This article shows you the Intune settings you can use to configure VPN connections on devices running Windows 8.1.

Depending on the settings you choose, not all values in the following list are configurable.

## Before you begin

- [Create a Windows 8.1 VPN device configuration profile](vpn-settings-configure.md).

- [!INCLUDE [partner-vpns](../includes/partner-vpns.md)]

## Base VPN settings

- **Connection name**: Enter a name for this connection. Users see this name when they browse their device for the list of available VPN connections. For example, enter `Contoso VPN`.
- **Servers**: Add one or more VPN servers that devices connect to. When you add a server, you enter the following information:
  - **Description**: Enter a descriptive name for the server, such as **Contoso VPN server**.
  - **IP address or FQDN**: Enter the IP address or fully qualified domain name (FQDN) of the VPN server that devices connect to. For example, enter `192.168.1.1` or `vpn.contoso.com`.
  - **Default server**: **True** sets this server as the default server that devices use to establish the connection. Set only one server as the default.
  - **Import**: Browse to a comma-separated file with the list of servers in the format: description, IP address or FQDN, Default server. Choose **OK** to import these servers into the **Servers** list.
  - **Export**: Exports the list of servers to a comma-separated-values (csv) file.

- **Connection type**: Select the VPN connection type. Your options:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Access**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Login group or domain** (SonicWall Mobile Connect only): Enter the name of the login group or domain you want to connect to.

- **Role** (Pulse Secure only): Enter the name of the user role that can access this connection. A user role defines personal settings and options, and it enables or disables certain access features.

- **Realm** (Pulse Secure only): Enter the name of the authentication realm you want to use. An authentication realm is a grouping of authentication resources that the Pulse Secure connection type uses.

- **Custom XML**: Enter any custom XML commands that configure the VPN connection.

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

## Proxy

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the proxy server URL that includes the configuration file. For example, enter `http://proxy.contoso.com/pac`.
- **Address**: Enter the IP address or fully qualified host name of the proxy server. For example, enter `10.0.0.3` or `vpn.contoso.com`.
- **Port number**: Enter the port number associated with the proxy server. For example, enter `8080`.
- **Automatically detect proxy settings**: If your VPN server requires a proxy server for the connection, choose if you want devices to automatically detect the connection settings. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enable**: Automatically detects the connection settings.
  - **Disable**: Doesn't automatically detect the connection settings.
- **Bypass proxy for local addresses**: Choose to use the proxy server for local addresses. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enable**: Don't use a proxy server for local addresses.
  - **Disable**: Use a proxy server for local addresses.

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md), and [Windows 10/11](vpn-settings-windows-10.md) devices.
