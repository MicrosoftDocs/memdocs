---
title: Manage Windows express updates
titleSuffix: Configuration Manager
description: Configuration Manager supports express installation files for Windows 10 or later, which provide smaller downloads and faster installation times on clients.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 10/20/2021
ms.topic: conceptual
ms.service: configuration-manager
ms.subservice: software-updates
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage express installation files for Windows 10 or later updates

Configuration Manager supports express installation files for Windows 10 or later updates. Configure the client to download only the changes between the current month's Windows cumulative quality update and the previous month's update. Without express installation files, Configuration Manager clients download the full Windows cumulative update each month, including all updates from previous months. Using express installation files provides for smaller downloads and faster installation times on clients.

To learn how to use Configuration Manager to manage update content to stay current with Windows, see [Optimize Windows update delivery](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> The OS client support is available in Windows 10, version 1607, with an update to the Windows Update Agent. This update is included with the updates released on April 11, 2017. For more information about these updates, see [support article 4015217](https://support.microsoft.com/kb/4015217). Future updates leverage express for smaller downloads. Prior versions of Windows 10, and Windows 10 version 1607 without this update don't support express installation files.  


## Enable the site to download express installation files for Windows 10 or later updates
To start synchronizing the metadata for Windows 10 or later express installation files, enable it in the properties of the software update point.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. Select the central administration site or the stand-alone primary site.  

3. In the ribbon, click **Configure Site Components**, and then click **Software Update Point**. Switch to the **Update Files** tab, and select **Download both full files for all approved updates and express installation files for Windows 10 or later**.

> [!NOTE]    
> You can't configure the software update point component to *only* download express updates.  The site downloads the express installation files in addition to the full files. This increases the amount of content stored in the content library, and distributed to and stored on your distribution points.

> [!Tip]  
> To determine the actual space being used on disk by the file, check the **Size on disk** property of the file. The Size on disk property should be considerably smaller than the Size value. For more information, see [FAQs to optimize Windows update delivery](optimize-windows-10-update-delivery.md#bkmk_faq).  


## Enable clients to download and install express installation files
To enable express installation files support on clients, enable express installation files in the **Software Updates** group of client settings. This setting creates a new HTTP listener that listens for requests to download express installation files on the port that you specify.

> [!NOTE]    
> This is a local port that clients use to listen for requests from Delivery Optimization or Background Intelligent Transfer Service (BITS) to download express content from the distribution point. You don't need to open this port on firewalls because all traffic is on the local computer.  

Once you deploy client settings to enable this functionality on the client, it attempts to download the delta between the current month's Windows cumulative update and the previous month's update. Clients must run a version of Windows 10 or later that supports express installation files.  

1. Enable support for express installation files in the properties of the software update point component (previous procedure).  

2. In the Configuration Manager console, go to the **Administration** workspace, and select **Client Settings**.  

3. Select the appropriate client settings, and click **Properties** on the ribbon.  

4. Select the **Software Updates** group. Configure to **Yes** the setting to **Enable installation of Express Updates on clients**. Configure the **Port used to download content for Express Updates** with the port used by the HTTP listener on the client.
    - In version 1902, **Enable installation of Express Updates on clients** was changed to **Allow clients to download delta content when available**.
    - In version 1902, **Port used to download content for Express Updates** was changed to **Port that clients use to receive requests for delta content**.
    

## Next steps

[Deploy software updates](deploy-software-updates.md)
