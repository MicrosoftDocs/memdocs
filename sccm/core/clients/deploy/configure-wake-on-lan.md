---
title: "Configure Wake on LAN"
titleSuffix: "Configuration Manager"
description: "Select Wake On LAN settings in System Center Configuration Manager."
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---
# How to configure Wake on LAN in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Specify Wake on LAN settings for System Center Configuration Manager when you want to bring computers out of a sleep state to install required software, such as software updates, applications, task sequences, and programs.

## Wake on LAN starting in version 1810
<!--3607710-->
Starting in Configuration Manager 1810, there is a new way to wake up machines when they're asleep. You can wake up clients from the Configuration Manager console, even if the client isn't on the same subnet as the site server. If you need to perform maintenance or query devices, you're not limited by remote clients that are asleep. The site server uses the client notification channel to identify two other clients that are awake on the same remote subnet, then uses those clients to send a wake on LAN request (magic packet). Using the client notification channel helps avoid MAC flaps, which could cause the port to be shut down by the router. The new version of Wake on LAN can be enabled at the same time as the [previous version](#bkmk_wol-previous) for Configuration manager version 1802 and prior.

You can wake up a single client or any sleeping clients in a collection. For devices that are already awake in the collection, no action is taken for them. Only clients that are asleep will be sent a Wake on LAN request. For more information on how to notify a client to wake, see [Client notification](/sccm/core/clients/manage/client-notification).

### Limitations
- At least one client in the target subnet must be awake. 
- This feature doesn't support the following network technologies:
   - IPv6
   - 802.1x network authentication

### Security role permissions

- **Notify resource** under the Collection category

### To configure Wake on LAN for the site starting in version 1810

Each Configuration Manager site where you want to use Wake on LAN should have the setting enabled. To enable Wake on LAN for a site, use the below instructions:

1. Under **Administration**, expand **Site Configuration** then click on **Sites**.
1. Select the site, then click **Properties** in the ribbon.
1. Click on the **Wake On LAN** tab. 
1. Check the box next to **Enable Wake On LAN for this site** and select **Unicast**. 
1. Click **OK** to save the site property.

![Enable Wake On LAN in the site properties](media/wol-site-properties.png)

### Configure the clients to use Wake on LAN starting in version 1810

Previously you had to manually enable the client for wake on LAN in the properties of the network adapter. Configuration Manager 1810 includes a new client setting called **Allow network wake-up**. Configure and deploy this setting instead of modifying the properties of the network adapter.

1. Under **Administration**, go to **Client Settings**.
1. Select the client settings you want to edit, or create new custom client settings to deploy. For more information, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).
1. Under the **Power Management** client settings, select **Enable** for the **Allow network wake-up** setting. For more information about this setting, see [About client settings](/sccm/core/clients/deploy/about-client-settings#power-management).

>![NOTE]
> Starting in Configuration Manager 1902, you can also specify the UDP port for the the **Allow network wake-up** client setting. Change the **Wake On LAN port number (UDP)** [client setting](/sccm/core/clients/deploy/about-client-settings#power-management).
<!--3605925-->

## <a name="bkmk_wol-previous"></a>  Wake on LAN for version 1802 and earlier

You can supplement Wake on LAN by using the wake-up proxy client settings. However, to use wake-up proxy, you must first enable Wake on LAN for the site and specify **Use wake-up packets only** and the **Unicast** option for the Wake on LAN transmission method. This wake-up solution also supports ad-hoc connections, such as a remote desktop connection.

Use the first procedure to configure a primary site for Wake on LAN. Then, use the second procedure to configure the wake-up proxy client settings. This second procedure configures the default client settings for the wake-up proxy settings to apply to all computers in the hierarchy. If you want these settings to apply to only selected computers, create a custom device setting and assign it to a collection that contains the computers that you want to configure for wake-up proxy. For more information about how to create custom client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

A computer that receives the wake-up proxy client settings will likely pause its network connection for 1-3 seconds. This occurs because the client must reset the network interface card to enable the wake-up proxy driver on it.

> [!WARNING]
> To avoid unexpected disruption to your network services, first evaluate wake-up proxy on an isolated and representative network infrastructure. Then use custom client settings to expand your test to a selected group of computers on several subnets. For more information about how wake-up proxy works, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### To configure Wake on LAN for a site for version 1802 and earlier

Prior to Configuration manager version 1810, you need to enable Wake on LAN for each site in a hierarchy.

1. In the Configuration Manager console, go to **Administration > Site Configuration > Sites**.
2. Click the primary site to configure, and then click **Properties**.
3. Click the **Wake on LAN** tab, and configure the options that you require for this site. To support wake-up proxy, make sure you select **Use wake-up packets only** and **Unicast**. For more information, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Click **OK** and repeat the procedure for all primary sites in the hierarchy.



### To configure wake-up proxy client settings

1. In the Configuration Manager console, go to **Administration > Client Settings**.
2. Click **Default Client Settings**, and then click **Properties**.
3. Select **Power Management** and then choose **Yes** for **Enable wake-up proxy**.
4. Review and if necessary, configure the other wake-up proxy settings. For more information on these settings see [Power management settings](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Click **OK** to close the dialog box, and then click **OK** to close the Default Client Settings dialog box.

You can use the following Wake On LAN reports to monitor the installation and configuration of wake-up proxy:

- Wake-Up Proxy Deployment State Summary
- Wake-Up Proxy Deployment State Details

> [!TIP]
> To test whether wake-up proxy is working, test a connection to a sleeping computer. For example, connect to a shared folder on that computer, or try connecting to the computer using Remote Desktop. If you use Direct Access, check that the IPv6 prefixes work by trying the same tests for a sleeping computer that is currently on the Internet.
