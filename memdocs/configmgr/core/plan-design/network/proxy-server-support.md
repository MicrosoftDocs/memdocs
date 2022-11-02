---
title: Proxy server support
titleSuffix: Configuration Manager
description: Learn how Configuration Manager systems use proxy servers.
ms.date: 04/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Proxy server support in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Some Configuration Manager components require connections to the internet. If your environment requires internet traffic to use a proxy server, configure these systems to use the proxy.

- A computer that hosts a site system server supports a single proxy server configuration. All site system roles on that computer share this same proxy configuration. If you need separate proxy servers for different roles or instances of a role, place those roles on separate site system servers.

- When you configure new proxy server settings for a site system server that already has a proxy server configuration, the original configuration is overwritten.

- By default, connections to the proxy use the **System** account of the computer that hosts the site system role.

- If the computer account can't authenticate, the site system server can store user credentials to connect to the proxy server. These credentials are the **site system proxy server account**.

- If you install the Configuration Manager console on administrative workstations, some connections will use the proxy configuration.

## Site system roles that use a proxy

The following site system roles connect to the internet, and if necessary, can use a proxy server:

### Asset Intelligence synchronization point

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is deprecated.<!-- 12454890 --> For more information, see [Asset intelligence deprecation](../../clients/manage/asset-intelligence/deprecation.md).

This site system role connects to Microsoft and uses a proxy server configuration on the computer that hosts the Asset Intelligence synchronization point.

### Cloud distribution point

> [!NOTE]
> The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances.<!-- 10247883 --> To provide content to internet-based devices, enable a cloud management gateway (CMG) to distribute content. For more information, see [Deprecated features](../changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).

The cloud distribution point role runs in Microsoft Azure. You don't configure this site system role to use a proxy. Set the proxy configuration on the primary site server that manages the cloud distribution point.

For this configuration, the primary site server:

- Must be able to connect to Microsoft Azure to set up, monitor, and distribute content to the cloud distribution point.

- By default, uses the computer's **System** account to make the connection. It can also use the site system proxy server account, if necessary.

- Uses Windows web browser APIs.

### Cloud management gateway connection point

The cloud management gateway (CMG) connection point is an on-premises role that communicates with the CMG service in Azure. For more information, see [Overview of CMG](../../clients/manage/cmg/overview.md).

### Distribution point

<!-- 5856396 -->

If you enable a Configuration Manager distribution point for Microsoft Connected Cache, it can communicate through an unauthenticated proxy server for internet access. For more information, see [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

### Exchange Server connector

This site system role connects to an Exchange Server. It uses a proxy server configuration on the computer that hosts the Exchange Server connector.

### Service connection point

This site system role connects to the Configuration Manager cloud service to download version updates for Configuration Manager. It uses a proxy server that's configured on the computer that hosts the service connection point.

### Software update point

This site system role uses the proxy when it connects to Microsoft Update to download patches and synchronize information about updates. Like every other site system role, first configure the site system proxy settings. Then configure the following options specific to the software update point:

- **Use a proxy server when synchronizing software updates**

- **Use a proxy server when downloading content by using automatic deployment rules**

    > [!NOTE]
    > While available for use, this setting isn't used by software update points at secondary sites.

These settings are on the **Proxy and Account Settings** tab of the software update point properties.

> [!NOTE]
> By default, when the automatic deployment rules run, the **System** account on the site server of the site on which an automatic deployment rule was created is used to connect to the internet and download software updates. Alternatively, configure and use the site system proxy server account.
>
> When this account cannot access the internet, software updates fail to download. The following entry is logged to **ruleengine.log**:
> `Failed to download the update from internet. Error = 12007.`

## Other features that use the proxy

The following features use the proxy of the site system that hosts the [service connection point](#service-connection-point) role: <!--5913817-->

- [Azure Active Directory (Azure AD) user discovery](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure AD user group discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Synchronizing collection membership results to Azure Active Directory groups](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## Configure the proxy for a site system server

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and then select the **Servers and Site System Roles** node.

2. Select the site system server that you want to edit. In the details pane, right-click the **Site system** role, and select **Properties**.

3. In Site system Properties, switch to the **Proxy** tab. Configure the following proxy settings:

    - **Use a proxy server when synchronizing information from the internet**: Select this option to enable the site system server to use a proxy server.

    - **Proxy server name**: Specify the hostname or FQDN of the proxy server in your environment.

    - **Port**: Specify the network port on which to communicate with the proxy server. By default, it uses port **80**.

    - **Use credentials to connect to the proxy server**: Many proxy servers require a user to authenticate. By default, the site system server uses its computer account to connect to the proxy server. If necessary, enable this option, click **Set**, and then choose an **Existing Account** or specify a **New Account**. These credentials are the **site system proxy server account**. For more information, see [Accounts used in Configuration Manager](../hierarchy/accounts.md).

4. Choose **OK** to save the new proxy server configuration.

## Configuration Manager console

<!-- 14110385 -->

If you install the Configuration Manager console on an administrative workstation, some connections will use the proxy configuration. The console may fail to connect to the site because of a proxy configuration. To help troubleshoot, you can modify the console configuration file, `Microsoft.ConfigurationManagement.exe.config`. By default, this file is located in `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin`. Open it in Windows Notepad or another XML editor.

Change this original setting:

```xml
  <system.net>
    <defaultProxy useDefaultCredentials="true" />
  </system.net>
```

Add the following element with the `defaultProxy` element: `<proxy usesystemdefault="False"/></defaultProxy>`

For example:

```xml
  <system.net>
    <defaultProxy useDefaultCredentials="true"><proxy usesystemdefault="False"/></defaultProxy>
  </system.net>
```

## Next steps

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow access to internet endpoints. For more information, see [internet access requirements](internet-endpoints.md).
