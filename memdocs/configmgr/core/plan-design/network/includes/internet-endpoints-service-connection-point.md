---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 11/20/2020
---

These configurations apply to the computer that hosts the service connection point and any firewalls between that computer and the internet. They both must allow communications through outgoing port **TCP 443** for HTTPS and outgoing port **TCP 80** for HTTP to the below internet locations.

The service connection point supports using a web proxy (with or without authentication) to use these locations. For more information, see [Proxy server support](proxy-server-support.md).

Other Configuration Manager features may require additional endpoints from the service connection point.

> [!TIP]  
> The service connection point uses the Microsoft Intune service when it connects to `go.microsoft.com` or `manage.microsoft.com`. There's a known issue in which the Intune connector experiences connectivity issues if the Baltimore CyberTrust Root Certificate isn't installed, is expired, or is corrupted on the service connection point. For more information, see [KB 3187516: Service connection point doesn't download updates](https://support.microsoft.com/help/3187516).  

Starting in version 2002, if the Configuration Manager site fails to connect to required endpoints for a cloud service, it raises a critical status message ID 11488. When it can't connect to the service, the SMS_SERVICE_CONNECTOR component status changes to critical. View detailed status in the [Component Status](../../../servers/manage/use-status-system.md#monitor-the-status-system) node of the Configuration Manager console.<!-- 5566763 -->

Starting in version 2010, the service connection point validates important internet endpoints for Desktop Analytics and tenant attach. These checks help make sure that the cloud-connected services are available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem. For more information, see [Validate internet access](../../../servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).<!--8565578-->

### <a name="bkmk_scp-updates"></a> Updates and servicing

For more information on this function, see [Updates and servicing for Configuration Manager](../../../servers/manage/updates.md).

> [!Tip]  
> Enable these endpoints for the [management insight](../../../servers/manage/management-insights.md) rule, **Connect the site to the Microsoft cloud for Configuration Manager updates**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

- `ceuswatcab01.blob.core.windows.net`

- `ceuswatcab02.blob.core.windows.net`

- `eaus2watcab01.blob.core.windows.net`

- `eaus2watcab02.blob.core.windows.net`

- `weus2watcab01.blob.core.windows.net`

- `weus2watcab02.blob.core.windows.net`

- `umwatsonc.events.data.microsoft.com`

- `*-umwatsonc.events.data.microsoft.com`

### Windows 10 servicing

For more information on this function, see [Manage Windows as a service](../../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### Azure services

For more information on this function, see [Configure Azure services for use with Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (Azure public cloud)
- `management.usgovcloudapi.net` (Azure US Government cloud)
