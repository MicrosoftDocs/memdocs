---
title: Client health with co-management
titleSuffix: Configuration Manager
description: Maintain visibility of Configuration Manager client health from the Intune on Azure portal
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Client health with co-management

The health of your network is directly connected to the health of the devices moving in and out of it. Intune can communicate with an unhealthy client, even when it isn't on your network. Use co-management to combine this feature with Configuration Manager's ability to report back 98% of known healthy clients. Then you can detect, assess, and provide visibility across all clients in real time. Intune also adds the support needed for compliance upgrades across all connected clients.

<!--update with final video for this quickstart-->
In the following video, senior program manager Rob York and product marketing manager Locky Ainley discuss and demo client health with co-management:

> [!VIDEO https://www.youtube.com/embed/gA5q0_3bxPs]



## Benefits

Assessing client health is a top priority. System Center 2012 Configuration Manager added **CCMeval**. This utility is external to the Configuration Manager client. It provides client health monitoring and auto remediation. However, this reporting relies on a device being physically or virtually on your internal network. Co-management helps to address this issue.

With co-management, Intune can report on the client health state. It provides timestamp information for the validity of the data. This information tells you if your devices are healthy, able to connect, able to install apps, or can update to the required OS builds. 

For a detailed overview of this feature, see this video from the [What's New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) session at Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


When Configuration Manager provides device status that the client is installed, but it isn't, Intune can provide more information without needing to connect to the client. The device health info in Intune is easy to understand. If the status is anything other than **Healthy**, it gives recommendations and next steps to troubleshoot and fix it.

> [!Note]  
> The following benefits are planned for a future version:
> - Configuration Manager will include additional functionality into CCMeval  
> - It will be easier to identify potentially unhealthy machines in both Configuration Manager and Intune  
> - You can group the client health data in Intune  



## Value proposition

With this feature, you now have an external data source with Intune. It allows you to determine next steps when troubleshooting a vast array of client issues. Now you don't need to create additional reports or use other tools to pull back client data.

When you have healthy clients, you have readily updated patch compliance. Better patch compliance means better security.



## Configure

To get started with this feature, use the following steps:

- Update devices to Windows 10, version 1709 or later  

- [Enable co-management](/sccm/comanage/how-to-enable)  
    - You don't need to switch any workload to Intune  

- Update your Configuration Manager site and clients to *version 1806* or later  


### Review Configuration Manager client health in Intune

1. Sign into the [Azure portal](https://portal.azure.com/).  

2. Choose **All services** > **Intune**. Intune is located in the **Monitoring + Management** section.  

3. Once you've opened the **Microsoft Intune** pane, in the menu under **Help and support**, go to the **Troubleshooting** page.  

4. Use the **Select user** option, find the specific device in the **Devices** list, and select it to open the device page.  

5. Co-management information is shown at the bottom of the device page. This information includes the following fields for client health:  
    - **Configuration Manager agent state**  
    - **Last Configuration Manager agent check in time**  

> [!Tip]  
> Intune-enrolled devices connect to the cloud service three times a day, approximately every eight hours. 
