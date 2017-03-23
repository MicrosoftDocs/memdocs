---
title: Manage Express installation files for Windows 10 updates | Microsoft Docs
description: "Configuration Manager supports express installation files for Windows 10, which provides smaller downloads and faster installation times on clients."
keywords:
author: dougebyms.author: dougebymanager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
---

## Manage Express installation files for Windows 10 updates
Beginning in Configuration Manager version 1702, Configuration Manager supports express installation files for Windows 10 updates. When you use a supported version of Windows 10, you can use Configuration Manager settings to download only the changes between the current month's Windows 10 Cumulative Update and the previous month's update. Without express installation files, Configuration Manager downloads the full Windows 10 Cumulative Update (including all updates from previous months) each month. Using express installation files provides for smaller downloads and faster installation times on clients.

> [!IMPORTANT]
> While the settings to support the use of express installation files is available in Configuration Manager, this functionality is only supported in Windows 10 version 1607 with a Windows Update Agent update included with the updates released on Arpil 12, 2017 (Patch Tuesday). For more information about these updates, see [support article 3147461](https://support.microsoft.com/help/3147461/cumulative-update-for-windows-10-april-12,-2016). You can take advantage of express installation files when the next set of updates are released on May 9, 2017. Windows 10 version 1607 without the update and prior versions do not support express installation files.


### To enable the download of express installation files for Windows 10 updates on the server
To start synchronizing the metadata for Windows 10 express installation files, you must enable it in the Software Update Point Properties.
1.	In the Configuration Manager console, navigate to **Administration** > **Site Configuration** > **Sites**.
2.	Select the central administration site or the stand-alone primary site.
3.	On the **Home** tab, in the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**. On the **Update Files** tab, select **Download full files for all approved updates and express installation files for Windows 10**.

### To enable support for clients to download and install express installation files
To enable express installation files support on clients, you must enable express installation files on clients in the Software Updates section of client settings. This creates a new HTTP listener that listens for requests to download express installation files on the port that you specify. Once you deploy client settings to enable this functionality on the client, it will attempt to download the delta between the current month's Windows 10 Cumulative Update and the previous month's update (clients must run a version of Windows 10 that supports express installation files).
1.	Enable support for express installation files in the Software Update Point Component properties (previous procedure).
2.	In the Configuration Manager console, navigate to **Administration** > **Client Settings**.
3.	Select the appropriate client settings, then on the **Home** tab, click **Properties**.
4.	Select the **Software Updates** page, configure **Yes** for the **Enable installation of Express Updates on clients** setting and configure the port used by the HTTP listener on the client for the **Port used to download content for Express Updates** setting.
