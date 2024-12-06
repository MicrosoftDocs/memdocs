---
# required metadata

title: Configure VPN settings to macOS devices in Microsoft Intune
description: Add or create a virtual private network (VPN) configuration profile in Microsoft Intune. Add the connection details, split tunneling, custom VPN settings with the identifier, key and value pairs, proxy settings with a configuration script, IP or FQDN address, and TCP port in Microsoft Intune on devices running macOS.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/19/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abalwan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Add VPN settings on macOS devices in Microsoft Intune

This article lists and describes the Intune settings you can use to configure VPN connections on devices running macOS.

Depending on the settings you choose, not all values in the following list are configurable.

This feature applies to:

- macOS  


## Before you begin

- Create a [macOS VPN device configuration profile](vpn-settings-configure.md).

- [!INCLUDE [partner-vpns](../includes/partner-vpns.md)]

- These settings are available for all enrollment types. For more information on the enrollment types, go to [macOS enrollment](../enrollment/macos-enroll.md).

## Base VPN

- **Deployment channel**: Select how you want to deploy the profile. This setting also determines the keychain where the authentication certificates are stored, so it's important to select the proper channel. It's not possible to edit the deployment channel after you deploy the profile. To change it, you must create a new profile. 

  >[!NOTE]
  > We recommend rechecking the deployment channel setting in existing profiles when the linked authentication certificates are up for renewal to ensure the intended channel is selected. If it isn't, create a new profile with the correct deployment channel.   

   You have two options:  
   - **User channel**: Always select the user deployment channel in profiles with user certificates. This option stores certificates in the user keychain.     
   - **Device channel**: Always select the device deployment channel in profiles with device certificates. This option stores certificates in the system keychain.   
   
- **Connection name**: Enter a name for this connection. End users see this name when they browse their device for the list of available VPN connections.

- **VPN server address**: Enter the IP address or fully qualified domain name of the VPN server that devices connect to. For example, enter `192.168.1.1` or `vpn.contoso.com`.
- **Authentication method**: Choose how devices authenticate to the VPN server. Your options:
  - **Certificates**: Under **Authentication certificate**, select a SCEP or PKCS certificate profile you previously created to authenticate the connection. For more information about certificate profiles, go to [How to configure certificates](../protect/certificates-configure.md). Choose the certificates that align with your deployment channel selection. If you selected the user channel, your certificate options are limited to user certificate profiles. If you selected the device channel, you have both user and device certificate profiles to choose from. However, we recommend always selecting the certificate type that aligns with the selected channel. Storing user certificates in the system keychain increases security risks.       
  - **Username and password**: End users must enter a username and password to sign into the VPN server.

- **Connection type**: Select the VPN connection type from the following list of vendors:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Access**
  - **NetMotion Mobility**
  - **Custom VPN**: Select this option if your VPN vendor isn't listed. Also configure:

    - **VPN identifier**: Enter an identifier for the VPN app you're using. This identifier is supplied by your VPN provider.
    - **Enter key and value pairs for the custom VPN attributes**: Add or import **Keys** and **Values** that customize your VPN connection. These values are typically supplied by your VPN provider.

- **Split tunneling**: **Enable** lets devices decide which connection to use depending on the traffic. For example, a user in a hotel uses the VPN connection to access work files, but use the hotel's standard network for regular web browsing. **Disable** lets all traffic use the VPN tunnel when the VPN connection is active.

## Automatic VPN

Select the **type of automatic VPN** you want. Your options:

- **Not configured**: Intune doesn't change or update this setting.

- **On-demand VPN**: On-demand VPN uses rules to automatically connect or disconnect the VPN connection. When your devices attempt to connect to the VPN, it looks for matches in the parameters and rules you create, like a matching IP address or domain name. If there's a match, then the action you choose runs.

  For example, create a condition where the VPN connection is only used when a device isn't connected to a company Wi-Fi network. Or, if a device can't access a DNS search domain you enter, then the VPN connection isn't started.

  - **Add**: Select this option and add a rule.

  - **I want to do the following**: If there's a match between the device value and your on-demand rule, then select the action. Your options:

    - Connect VPN
    - Disconnect VPN
    - Evaluate each connection attempt
    - Ignore

  - **I want to restrict to**: Select the condition that the rule must meet. Your options:

    - **Specific SSIDs**: Enter one or more wireless network names that the rule applies. This network name is the Service Set Identifier (SSID). For example, enter `Contoso VPN`.
    - **Specific search domains**: Enter one or more DNS domains that the rule applies. For example, enter `contoso.com`.
    - **All domains**: Select this option to apply your rule to all domains in your organization.

  - **But only if this URL probe succeeds**: Optional. Enter a URL that the rule uses as a test. If the device accesses this URL without redirection, then the VPN connection is started. And, the device connects to the target URL. The user doesn't see the URL string probe site.

    For example, a URL string probe is an auditing Web server URL that checks device compliance before connecting the VPN. Or, the URL tests the VPN's ability to connect to a site before the device connects to the target URL through the VPN.

- **Block users from disabling automatic VPN**: Your options:

  - **Not configured**: Intune doesn't change or update this setting.
  - **Yes**: Prevents users from turning off automatic VPN. It forces users to keep the automatic VPN enabled and running.
  - **No**: Allows users to turn off automatic VPN.

  This setting applies to:  
  - macOS 11 and newer (Big Sur)

- **Per-app VPN**: Enables per-app VPN by associating this VPN connection with a macOS app. When the app runs, the VPN connection starts. You can associate the VPN profile with an app when you assign the software. For more information, go to [How to assign and monitor apps](../apps/apps-deploy.md).

  - **Safari URLs that will trigger this VPN**: Add one or more web site URLs. When these URLs are visited using the Safari browser on the device, the VPN connection is automatically established.

  - **Associated Domains**: Enter associated domains in the VPN profile that automatically start the VPN connection. For example, enter `contoso.com`. Devices in the `contoso.com` domain automatically start the VPN connection.

    For more information, go to [associated domains](device-features-configure.md#associated-domains).

  - **Excluded Domains**: Enter domains that can bypass the VPN connection when per-app VPN is connected. For example, enter `contoso.com`. Devices in the `contoso.com` domain won't start or won't use the per-app VPN connection. Devices in the `contoso.com` domain use the public Internet.

  - **Prevent users from disabling automatic VPN**: Your options:

    - **Not configured**: Intune doesn't change or update this setting.
    - **Yes**: Prevents users from turning off automatic VPN. It forces users to keep the automatic VPN enabled and running.
    - **No**: Allows users to turn off automatic VPN.

    This setting applies to:  
    - macOS 11 and newer (Big Sur)

## Proxy

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the proxy server URL that includes the configuration file. For example, enter `http://proxy.contoso.com/pac`.
- **Address**: Enter the IP address or fully qualified host name of the proxy server. For example, enter `10.0.0.3` or `vpn.contoso.com`.
- **Port number**: Enter the port number associated with the proxy server. For example, enter `8080`.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md), and [Windows](vpn-settings-windows-10.md) devices.
