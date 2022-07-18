---
title: How to create VPN profiles
titleSuffix: Configuration Manager
description: Learn how to create VPN profiles in Configuration Manager.
ms.date: 03/29/2022
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# How to create VPN profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in version 2203, this company resource access feature is no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](../plan-design/resource-access-deprecation-faq.yml).

Configuration Manager supports multiple VPN connection types. For more information on the connection types available for the different device platforms, see [VPN profiles](vpn-profiles.md).

For third-party VPN connections, distribute the VPN app before you deploy the VPN profile. If you don't deploy the app, users will be prompted to do so when they try to connect to the VPN. For more information, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).

## Create a VPN profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and select the **VPN Profiles** node.

1. On the **Home** tab of the ribbon, in the **Create** group, choose **Create VPN Profile**.

1. On the **General** page of the Create VPN Profile Wizard, specify the following information:

    - **Name**: Enter a unique name to identify the VPN profile in the console.

        > [!NOTE]
        > Don't use the following characters in the VPN profile name: `\/:*?<>|; `. The Windows VPN profile doesn't support these special characters.

    - **Description**: Optionally enter a description to provide further information about the VPN profile.

    - **VPN profile type**: Select the appropriate platform.

        If you select the **Windows 8.1** platform, you can also **Import from file**. This action imports VPN profile information from an XML file. If you select this option, the rest of the wizard simplifies to the following pages: **Supported Platforms** and **Import VPN Profile**.

1. On the **Supported Platforms** page, select the OS versions that this VPN profile supports.

1. On the **Connection** page, specify the following information:

    - **Connection type**: Choose the VPN connection type. For more information on the supported types, see [VPN profiles](vpn-profiles.md).

    - **Server list**: Add a new server to use for the VPN connection. Depending on the connection type, you can add one or more VPN servers and specify which server is the default.

    - **Bypass VPN when connected to company network**: Configure clients to not use the VPN when they're on your internal network. If necessary, specify a connection-specific DNS name.

1. On the **Authentication Method** page of the wizard, choose a method that's supported by the connection type. The settings and available options on this page vary depending on the selected connection type. For more information, see [Authentication method reference](#bkmk_auth).

1. On the **Proxy Settings** page, if your VPN uses a proxy server, select one of the options as appropriate for your environment. Then provide the configuration information for the proxy.

1. The **Applications** page only applies to Windows 10 profiles. Add desktop and universal apps that automatically connect to this VPN. The type of app determines the app identifier:

    - For a *desktop app*, provide the file path of the app.

    - For a *universal app*, provide the package family name (PFN). To learn how to find the PFN for an app, see [Find a package family name for per-app VPN](find-a-pfn-for-per-app-vpn.md).

    You can also configure an option so that **Only the listed apps can use this VPN**.

    > [!IMPORTANT]
    > Secure all lists of associated apps that you compile for configuring a per-app VPN. If an unauthorized user changes your list, and you import it to the per-app VPN app list, you potentially authorize VPN access to apps that shouldn't have access.

1. The **Boundaries** page only applies to Windows 10 profiles to configure VPN boundaries. You can add the following options:

    - **Network traffic rules**: Set the protocols, local port, remote port, and address ranges to enable for the VPN connection.  

        > [!Note]
        > If you don't create a network traffic rule, all protocols, ports, and address ranges are enabled. After you create a rule, only the protocols, ports, and address ranges that you specify in that rule or in additional rules are used by the VPN connection.

    - **DNS names and servers**: DNS servers that are used by the VPN connection after the device establishes the connection.

    - **Routes**: Network routes that use the VPN connection. Creation of more than 60 routes may cause the policy to fail.

1. Complete the wizard.

The new VPN profile is displayed in the **VPN Profiles** node in the **Assets and Compliance** workspace.

## <a name="bkmk_auth"></a> Authentication method reference

Available VPN authentication methods depend on the connection type:

### Certificates

If the client certificate authenticates to a RADIUS server, like a Network Policy Server, set the Subject Alternative Name in the certificate to the User Principal Name.

Supported connection types:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### Username and Password

Supported connection types:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### Microsoft EAP-TTLS

Supported connection types:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### Microsoft protected EAP (PEAP

Supported connection types:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### Microsoft secured password (EAP-MSCHAP v2)

Supported connection types:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### Smart Card or other certificate

Supported connection types:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### MSCHAP v2

Supported connection types:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### Use machine certificates

Supported connection types:

- IKEv2

### Additional authentication options

When the Windows client version supports it, the option to **Configure** the authentication method is available. This option opens the Windows properties window to configure the authentication method.

Depending on the selected options, you might be asked to specify more information, for example:

- **Remember the user credentials at each logon**: User credentials are remembered so that users don't have to enter them each time they connect.  

- **Select a client certificate for client authentication**: Select a previously created client SCEP certificate profile to authenticate the VPN connection. For more information, see [Create PFX certificate profiles](create-certificate-profiles.md).

## Next steps

- For third-party VPN connections, distribute the VPN app before you deploy the VPN profile. If you don't deploy the app, users will be prompted to do so when they try to connect to the VPN. For more information, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).

- Deploy the VPN profile. For more information, see [How to deploy profiles](deploy-wifi-vpn-email-cert-profiles.md).
