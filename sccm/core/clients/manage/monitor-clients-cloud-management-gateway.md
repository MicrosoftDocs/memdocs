---
title: "Monitor clients | cloud management gateway | System Center Configuration Manager"
description: ""
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: Mtillman
ms.author: mtillman
manager: angrobe
---

# Monitor clients for cloud management gateway in Configuration Manager

Beginning in version 1610, after the cloud management gateway service is running and clients are connecting through it, you can monitor the status of clients in the Configuration Manager console. For more information, see [how to monitor clients](monitor-clients.md).

You can also monitor the network traffic and set up outbound traffic alerts to make sure you know how the service is performing. 

## Monitor traffic in the console

You can monitor traffic on cloud management gateway using the Configuration Manager console:

1. Go to **Administration > Cloud Services > Cloud Management Gateway**.

2. Select the cloud management gateway service in the list pane.

3. View the traffic information in the details pane for the cloud management gateway connection role and the site system roles it connects to.

## Set up outbound traffic alerts

Outbound traffic alerts will help you know when traffic approaches a 14-day (2 week) threshold level. You are given the option of setting up traffic alerts when you create the cloud management gateway service. If you skipped that part, you can still set up the alerts after the service is running. And you can also adjust the alert settings at any time.

1. Go to **Administration > Cloud Services > Cloud Management Gateway**.

2. Right-click the cloud management gateway service in the list pane, and choose **Properties**.

3. Click the Alerts tab, and choose to turn on (or off) the threshold and alerts. Then specify the 14-day threshold (in GB) and percentages of the threshold for raising the different alert levels.

4. Click **OK** when you're done.
