---
title: Monitor cloud management gateway
titleSuffix: Configuration Manager
description: Monitor clients and network traffic through the cloud management gateway (CMG).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Monitor cloud management gateway in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

After the cloud management gateway is running and clients are connecting through it, you can monitor clients and network traffic to make sure you know how the service is performing.



## Monitor clients

Clients connected through the cloud management gateway appear in the Configuration Manager console the same way on-premises clients do. For more information, see [how to monitor clients](/sccm/core/clients/manage/monitor-clients).



## Monitor traffic in the console

Monitor traffic on the cloud management gateway using the Configuration Manager console:

1. Go to **Administration > Cloud Services > Cloud Management Gateway**.

2. Select the cloud management gateway in the list pane.

3. View the traffic information in the details pane for the cloud management gateway connection point and the site system roles it connects to.



## Set up outbound traffic alerts

Outbound traffic alerts help you know when network traffic approaches a 14-day threshold level. When you create the cloud management gateway, you can set up traffic alerts. If you skipped that part, you can still set up the alerts after the service is running. Adjust the alert settings at any time.

1. Go to **Administration > Cloud Services > Cloud Management Gateway**.

2. Right-click the cloud management gateway in the list pane, and choose **Properties**.

3. Click the **Alerts** tab. Enable the threshold and alerts. Specify the 14-day data threshold in gigabytes (GB). Also specify the threshold percentage to raise the different alert levels.

4. Click **OK** when you're done.



## Monitor logs

The cloud management gateway generates entries in a number of log files. For more information, see [Configuration Manager logs](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
