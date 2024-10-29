---
title: Client health with co-management
titleSuffix: Configuration Manager
description: Maintain visibility of Configuration Manager client health from the Microsoft Intune admin center.
ms.date: 11/08/2021
ms.subservice: co-management
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Client health with co-management

The health of your network is directly connected to the health of the devices moving in and out of it. Intune can communicate with an unhealthy client, even when it isn't on your network. Use co-management to combine this feature with Configuration Manager's ability to report back 98% of known healthy clients. Then you can detect, assess, and provide visibility across all clients in real time. Intune also adds the support needed for compliance upgrades across all connected clients.

In the following video, senior program manager Rob York and product marketing manager Locky Ainley discuss and demo client health with co-management:

> [!VIDEO https://aka.ms/docs/player?id=ed0d8d8a-1125-42bb-9561-a07618a13cea]

## Benefits

Assessing client health is a top priority. System Center 2012 Configuration Manager added **CCMeval**. This utility is external to the Configuration Manager client. It provides client health monitoring and auto remediation. However, this reporting relies on a device being physically or virtually on your internal network. Co-management helps to address this issue.

With co-management, Intune can report on the client health state. It provides timestamp information for the validity of the data. This information tells you if your devices are healthy, able to connect, able to install apps, or can update to the required OS builds.

For a detailed overview of this feature, see this video from the [What's New in Configuration Manager](https://myignite.microsoft.com/archives/IG18-BRK3035) session at Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]

When Configuration Manager provides device status that the client is installed, but it isn't, Intune can provide more information without needing to connect to the client. The device health info in Intune is easy to understand. If the status is anything other than **Healthy**, it gives recommendations and next steps to troubleshoot and fix it.

## Value proposition

With this feature, you now have an external data source with Intune. It allows you to determine next steps when troubleshooting a vast array of client issues. Now you don't need to create additional reports or use other tools to pull back client data.

When you have healthy clients, you have readily updated patch compliance. Better patch compliance means better security.

## Configure

To get started with this feature, use the following steps:

- Update devices to a supported version of Windows 10 or later.

- [Enable co-management](how-to-enable.md). You don't need to switch any workload to Intune.

- Update your Configuration Manager site and clients to a supported current branch version.

### Review Configuration Manager client health in Intune

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the menu under **Troubleshooting + support**, go to the **Troubleshoot** page.

1. Use the **Select user** option, find the specific device in the **Devices** list, and select it to open the device page.

1. Co-management information is shown at the bottom of the device page. This information includes the following fields for client health:

    - **Configuration Manager agent state**
    - **Last Configuration Manager agent check in time**

> [!TIP]
> Intune-enrolled devices connect to the cloud service three times a day, approximately every eight hours.
