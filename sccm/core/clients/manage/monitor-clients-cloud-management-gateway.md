---
title: "Monitor clients | Cloud Management Gateway | System Center Configuration Manager"
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

# Monitor clients for Cloud Management Gateway in Configuration Manager

After the [cloud management gateway and site system roles are completely configured](setup-cloud-management-gateway.md), clients will get the location of cloud management gateway on the next location request. Clients with updated location information can then communicate with Configuration Manager on the Internet. The polling cycle for location requests is every 24 hours. If you don't want to wait for the normally scheduled location request, you can force the request by restarting the SMS Agent Host service (ccmexec.exe) on the computer.

After clients have the new location information for cloud management gateway, you can monitor the status of clients that are no longer on the internal private network but have Internet access. For more information, see [how to monitor clients](monitor-clients.md).

You can monitor traffic on cloud management gateway:

1. Go to **Administration > Cloud Services > Cloud Management Gateway**.

2. Select the cloud management gateway service in the list pane.

3. View the traffic information in the details pane.   
