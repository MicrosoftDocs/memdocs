---
title: Proxy server support
titleSuffix: Configuration Manager
description: Learn how Configuration Manager site system servers use proxy servers.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
---

# Proxy server support in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Some Configuration Manager site system servers require connections to the internet. If your environment requires internet traffic to use a proxy server, configure these site system roles to use the proxy.  

- A computer that hosts a site system server supports a single proxy server configuration. All site system roles on that computer share this same proxy configuration. If you need separate proxy servers for different roles or instances of a role, place those roles on separate site system servers.  

- When you configure new proxy server settings for a site system server that already has a proxy server configuration, the original configuration is overwritten.  

- By default, connections to the proxy use the **System** account of the computer that hosts the site system role.  

- If the computer account can't authenticate, the site system server can store user credentials to connect to the proxy server. These credentials are the **site system proxy server account**.  

## Site system roles that use a proxy

The following site system roles connect to the internet, and if necessary, can use a proxy server:  

### Asset Intelligence synchronization point

This site system role connects to Microsoft and uses a proxy server configuration on the computer that hosts the Asset Intelligence synchronization point.  

### Cloud distribution point

The cloud distribution point role runs in Microsoft Azure. You don't configure this site system role to use a proxy. Set the proxy configuration on the primary site server that manages the cloud distribution point.  

For this configuration, the primary site server:  

- Must be able to connect to Microsoft Azure to set up, monitor, and distribute content to the cloud distribution point.  

- By default, uses the computer's **System** account to make the connection. It can also use the site system proxy server account, if necessary.  

- Uses Windows web browser APIs.  

### Distribution point

<!-- 5856396 -->

Starting in version 2002, if you enable a Configuration Manager distribution point for Microsoft Connected Cache, it can communicate through an unauthenticated proxy server for internet access. For more information, see [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

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

## <a name="bkmk_other"></a> Other features that use the proxy for a site system server

*(Introduced in version 2002)*

Starting in Configuration Manager version 2002, the following features use the proxy of the site system that hosts the [service connection point](#service-connection-point) role: <!--5913817-->

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

    - **Use credentials to connect to the proxy server**: Many proxy servers require a user to authenticate. By default, the site system server uses its computer account to connect to the proxy server. If necessary, enable this option, click **Set**, and then choose an **Existing Account** or specify a **New Account**. These credentials are the **site system proxy server account**.  For more information, see [Accounts used in Configuration Manager](../hierarchy/accounts.md).  

4. Choose **OK** to save the new proxy server configuration.  
