---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 11/17/2021
ms.localizationpriority: medium
---

These configurations apply to the server that hosts the service connection point and any firewalls between that server and the internet. Allow communication through outgoing HTTPS port **TCP 443** to the internet locations.

The service connection point supports using a web proxy with or without authentication to use these locations. For more information, see [Proxy server support](../proxy-server-support.md).

If the Configuration Manager site fails to connect to required endpoints for a cloud service, it raises a critical status message ID 11488. When it can't connect to the service, the SMS_SERVICE_CONNECTOR component status changes to critical. View detailed status in the [Component Status](../../../servers/manage/use-status-system.md#monitor-the-status-system) node of the Configuration Manager console.<!-- 5566763 -->

Starting in version 2010, the service connection point validates important internet endpoints for [Desktop Analytics](../internet-endpoints.md#desktop-analytics) and [tenant attach](../internet-endpoints.md#tenant-attach). These checks help make sure that the cloud-connected services are available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem. For more information, see [Validate internet access](../../../servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).<!--8565578-->

The specific URLs required by the service connection point vary by Configuration Manager feature:

- [Updates and servicing](../internet-endpoints.md#updates-and-servicing)
- [Windows servicing](../internet-endpoints.md#windows-servicing)
- [Azure services](../internet-endpoints.md#azure-services)
- [Microsoft Store for Business](../internet-endpoints.md#microsoft-store-for-business)
- [Cloud services](../internet-endpoints.md#cloud-services)
- [Configuration Manager console](../internet-endpoints.md#configuration-manager-console)
- [Desktop Analytics](../internet-endpoints.md#desktop-analytics)
- [Tenant attach](../internet-endpoints.md#tenant-attach)
- [External notifications](../internet-endpoints.md#external-notifications)

> [!TIP]  
> The service connection point uses the Microsoft Intune service when it connects to `go.microsoft.com` or `manage.microsoft.com`. There's a known issue in which the Intune connector experiences connectivity issues if the Baltimore CyberTrust Root Certificate isn't installed, is expired, or is corrupted on the service connection point. For more information, see [Service connection point doesn't download updates](/troubleshoot/mem/configmgr/service-connection-point-not-download-updates).
