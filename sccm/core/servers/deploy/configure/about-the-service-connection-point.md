---
title: Service connection point
titleSuffix: Configuration Manager
description: Learn about this Configuration Manager site system role, and understand and plan for its range of uses.
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# About the service connection point in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The service connection point is a site system role that serves several important functions for the hierarchy. Before you set up the service connection point, understand and plan for its range of uses. Planning for usage might affect how you set up this site system role:  

- **Manage mobile devices with Microsoft Intune**: This role replaces the Windows Intune connector that previous versions of Configuration Manager used and can be configured with your Intune subscription details. For more information, see [Hybrid mobile device management (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Manage mobile devices with on-premises MDM**: This role provides support for on-premises devices that you manage and that don't connect to the internet. For more information, see [Manage mobile devices with on-premises infrastructure](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Upload usage data from your Configuration Manager infrastructure**: You can control the level or amount of detail that you upload. Uploaded data helps:  

    - Proactively identify and troubleshoot problems  

    - Improve our products and service  

    - Identify updates for Configuration Manager that apply to the version of Configuration Manager that you use  

    For more information about data that each level collects and how to change the collection level after the role installs, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Then follow the link for the version of Configuration Manager that you use.  

    For more information, see [Usage data levels and settings](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Download updates that apply to your Configuration Manager infrastructure**: Only relevant updates for your infrastructure are made available based on usage data you upload.  

- **Each hierarchy supports a single instance of this role**:  

    - The site system role can only be installed at the top-tier site of your hierarchy, which is a central administration site or stand-alone primary site.  

    - If you expand a stand-alone primary site to a larger hierarchy, you must uninstall this role from the primary site and can then install it at the central administration site.  


##  <a name="bkmk_modes"></a> Modes of operation  
The service connection point supports two modes of operation:  

- In **online mode**, the service connection point automatically checks every 24 hours for updates. It downloads new updates that are available for your current infrastructure and product version to make them available in the Configuration Manager console.  

- In **offline mode**, the service connection point doesn't connect to the Microsoft cloud service. To manually import available updates, use the [service connection tool](/sccm/core/servers/manage/use-the-service-connection-tool).  

If you change between online or offline modes after you install the service connection point, you must restart the SMS_DMP_DOWNLOADER thread of the Configuration Manager SMS_Executive service before the change becomes effective. You can use the Configuration Manager Service Manager to restart only the SMS_DMP_DOWNLOADER thread of the SMS_Executive service. You can also restart the SMS_Executive service for Configuration Manager, which restarts most site components. Alternatively, you can wait for a scheduled task like a site backup, which stops and then later restarts the SMS_Executive service for you.  

To use the Configuration Manager Service Manager, in the console go to **Monitoring** > **System Status** > **Component Status**, choose **Start**, and then choose **Configuration Manager Service Manager**. In the service manager:  

- In the navigation pane, expand the site, expand **Components**, and then choose the component that you want to restart.  

- In the details pane, right-click the component, and then choose **Query**.  

- After the status of the component is confirmed, right-click the component again, and then choose **Stop**.  

- **Query** the component again to confirm that it is stopped. Right-click the component one more time, and then choose **Start**.  

> [!IMPORTANT]  
> The process that adds a Microsoft Intune subscription to the service connection point automatically sets the site system role to be online. The service connection point doesn't support offline mode when it's set up with an Intune subscription.  

**When the role installs on a computer that is remote from the site server:**  

- The computer account of the site server must be a local admin on the computer that hosts a remote service connection.

- You must set up the site system server that hosts the role with a site system installation account.  

- The distribution manager on the site server uses the site system installation account to transfer updates from the service connection point.

##  <a name="bkmk_urls"></a> Internet access requirements  
To enable operation, the computer that hosts the service connection point and any firewalls between that computer and the internet must pass communications through outgoing port **TCP 443** for HTTPS and outgoing port **TCP 80** for HTTP to the below internet locations. The service connection point also supports using a web proxy (with or without authentication) to use these locations. If you need to configure a web proxy account, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support).

> [!TIP]  
> The service connection point uses the Microsoft Intune service when it connects to go.microsoft.com or manage.Microsoft.com. There's a known issue in which the Intune connector experiences connectivity issues if the Baltimore CyberTrust Root Certificate isn't installed, is expired, or is corrupted on the service connection point. For more information, see [Service connection point doesn't download updates](https://support.microsoft.com/help/3187516).  

#### Updates and servicing

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

#### Microsoft Intune

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

#### Windows 10 servicing

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

#### Azure services

- `management.azure.com`  

## Install the service connection point
When you run **Setup** to install the top-tier site of a hierarchy, you have the option to install the service connection point.

After setup runs, or if you are reinstalling the site system role, use the **Add Site System Roles** wizard or the **Create Site System Server** wizard to install the site system on a server at the top-tier site of your hierarchy, that is, the central administration site or a stand-alone primary site. Both wizards are on the **Home** tab in the console at **Administration** > **Site Configuration** > **Servers and Site System Roles**.



## Log files used by the service connection point
To view information about uploads to Microsoft, view the **Dmpuploader.log** on the computer that runs the service connection point.  For downloads, including download progress of updates, view **Dmpdownloader.log**. For the complete list of logs related to the service connection point, see [Service connection point](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) in the Configuration Manager log files article.

You can also use the following flowcharts to understand the process flow and key log entries for update downloads and replication of updates to other sites:
- [Flowchart - Download updates](/sccm/core/servers/manage/download-updates-flowchart)
- [Flowchart - Update replication](/sccm/core/servers/manage/update-replication-flowchart)
