---
title: File-based replication
titleSuffix: Configuration Manager
description: Learn how Configuration Manager uses file-based replication to transfer data between sites in your hierarchy
ms.date: 08/09/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# File-based replication

*Applies to: Configuration Manager (current branch)*

Configuration Manager uses file-based replication to transfer file-based data between sites in your hierarchy. This data includes applications and packages that you want to deploy to distribution points in child sites. It also handles unprocessed discovery data records that the site transfers to its parent site and then processes.  

File-based communication between sites uses the *server message block* (SMB) protocol on TCP/IP port 445. To control the amount of data the site transfers across the network, specify bandwidth throttling and pulse mode. Use schedules to control when to send data across the network.  

## <a name="bkmk_routes"></a> Routes

The following information can help you set up and use file replication routes.  

### File replication route

Each file replication route identifies a destination site to which a site transfers file-based data. Each site supports one file replication route to a specific destination site.  

To manage a file replication route, go to the **Administration** workspace. Expand the **Hierarchy Configuration** node, and then select **File Replication**.  

You can change the following settings for file replication routes:  

#### File replication account

This account connects to the destination site, and writes data to that site's **SMS_Site** share. The receiving site processes the data written to this share. By default, when you add a site to the hierarchy, Configuration Manager assigns the new site server's computer account as its file replication account. It then adds this account to the destination site's `SMS_SiteToSiteConnection_<sitecode>` group. This group is local to the computer that grants access to the SMS_Site share. You can change this account to be a Windows user account. If you change the account, make sure you add the new account to the destination site's `SMS_SiteToSiteConnection_<sitecode>` group.  

> [!NOTE]  
> Secondary sites always use the computer account of the secondary site server as the **File Replication Account**.  

#### Schedule

Set the schedule for each file replication route. This action restricts the type of data and time when data can transfer to the destination site.  

#### Rate limits

Specify rate limits for each file replication route. This action controls the network bandwidth the site uses when it transfers data to the destination site:  

- **Pulse mode**: Specify the size of the data blocks that the site sends to the destination site. You can also specify a time delay between sending each data block. Use this option when you must send data across a low-bandwidth network connection to the destination site.

    For example, you have constraints to send 1 KB of data every five seconds, but not 1 KB every three seconds. This constraint is regardless of the speed of the link or its usage at a given time.

- **Limited to maximum transfer rates by hour**: The site sends data to a destination site by using only the percentage of time that you specify. Configuration Manager doesn't identify the network's available bandwidth. It divides the time it can send data into slices of time. It then sends the data in a short block of time, which is followed by blocks of time when it doesn't send data.

    For example, you set the maximum rate to **50%**. Configuration Manager transmits data for an amount of time followed by an equal period of time when it doesn't send any data. It doesn't manage the actual size of the data block that it sends. The site only manages the amount of time during which it sends data.  

    > [!CAUTION]  
    > By default, a site can use up to three **concurrent sendings** to transfer data to a destination site. When you enable rate limits for a file replication route, it limits the **concurrent sendings** to that site to one. This behavior applies even when the **Limit available bandwidth (%)** is set to **100%**. For example, if you use the default settings for the sender, this reduces the transfer rate to the destination site to be one-third of the default capacity.  

#### Routes between secondary sites

Configure a file replication route between two secondary sites to route file-based content between those sites.  


### Sender

Each site has one sender. The sender manages the network connection from one site to a destination site. It can establish connections to multiple sites at the same time. To connect to a site, the sender uses the file replication route to the site and identifies the account it uses to establish the network connection. The sender also uses this account to write data to the destination site's SMS_Site share.  

By default, the sender writes data to a destination site by using multiple **concurrent sendings**, or a *thread*. Each thread can transfer a different file-based object to the destination site. When the sender begins to send an object, it continues to write blocks of data for that object until it sends the entire object. After it sends all the data for the object, a new object can begin to send on that thread.  

To manage the sender for a site, go to the **Administration** workspace, and expand the **Site Configuration** node. Select the **Sites** node, and then select **Properties** for the site you want to manage. Switch to the **Sender** tab to change the sender settings.  

You can change the following settings for a sender:  

#### Maximum concurrent sendings

By default, each site uses five concurrent sendings (threads). Three threads are available for use when it sends data to any one destination site. When you increase this number, you can increase the throughput of data between sites. More threads mean that Configuration Manager can transfer more files at the same time. Increasing this number also increases the demand for network bandwidth between sites.  

#### Retry settings

By default, each site retries a problem connection two times, with a one-minute delay between connection attempts. You can modify the number of connection attempts the site makes, and how long to wait between attempts.  


## Next steps

[Database replication](database-replication.md)
