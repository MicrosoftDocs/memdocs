---
title: "Configure Wake on LAN | Microsoft Docs"
description: "Select Wake On LAN settings in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: 7
author: arob98
ms.author: angrobe
manager: angrobe
---
# How to configure Wake on LAN in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Specify Wake on LAN settings for System Center Configuration Manager when you want to bring computers out of a sleep state to install required software, such as software updates, applications, task sequences, and programs.

You can supplement Wake on LAN by using the wake-up proxy client settings. However, to use wake-up proxy, you must first enable Wake on LAN for the site and specify **Use wake-up packets only** and the **Unicast** option for the Wake on LAN transmission method. This wake-up solution also supports ad-hoc connections, such as a remote desktop connection.

Use the first procedure to configure a primary site for Wake on LAN. Then, use the second procedure to configure the wake-up proxy client settings. This second procedure configures the default client settings for the wake-up proxy settings to apply to all computers in the hierarchy. If you want these settings to apply to only selected computers, create a custom device setting and assign it to a collection that contains the computers that you want to configure for wake-up proxy. For more information about how to create custom client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

A computer that receives the wake-up proxy client settings will likely pause its network connection for 1-3 seconds. This occurs because the client must reset the network interface card to enable the wake-up proxy driver on it.

> [!WARNING]
> To avoid unexpected disruption to your network services, first evaluate wake-up proxy on an isolated and representative network infrastructure. Then use custom client settings to expand your test to a selected group of computers on several subnets. For more information about how wake-up proxy works, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## To configure Wake on LAN for a site

1. In the Configuration Manager console, go to **Administration > Site Configuration > Sites**.
2. Click the primary site to configure, and then click **Properties**.
3. Click the **Wake on LAN** tab, and configure the options that you require for this site. To support wake-up proxy, make sure you select **Use wake-up packets only** and **Unicast**. For more information, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Click **OK** and repeat the procedure for all primary sites in the hierarchy.

## To configure wake-up proxy client settings

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
