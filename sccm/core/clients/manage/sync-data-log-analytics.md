---
title: Sync data to Log Analytics
titleSuffix: Configuration Manager
description: Sync data from Configuration Manager to Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

#  Sync data from Configuration Manager to Azure Log Analytics

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1258052-->
Use the **Azure Services Wizard** to configure a connection from Configuration Manager to the Azure Log Analytics cloud service. This connection synchronizes device collection data to Log Analytics. 

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> Beginning with Configuration Manager 1802, the Log Analytics Connector is no longer a pre-release feature. To learn more, see [Use pre-release features from updates](/sccm/core/servers/manage/pre-release-features).



## Prerequisites for the Log Analytics Connector

> [!Note]  
> This article refers to the *Log Analytics Connector*, which was formerly called the *OMS Connector*. There's no functional difference. For more information, see [Azure Management - Monitoring](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Before you install the Log Analytics connector in Configuration Manager, provide Configuration Manager with permissions. Grant *contributor access* to the Azure *resource group* that contains your Log Analytics workspace. For more information, see [Provide Configuration Manager with permissions to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Install the Log Analytics connector on the computer that hosts the [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in online mode.  

- Install a Microsoft Monitoring Agent for Log Analytics on the service connection point with the connector. Configure this agent and the connector to use the same Log Analytics workspace. For more information on installing this agent, see [Download and install the agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- After you install the connector and agent, configure Log Analytics to use Configuration Manager data. For more information, see [Import Configuration Manager collections](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## Configure the connection to Log Analytics

Use the **Azure Services Wizard** to configure a connection from Configuration Manager to the Azure Log Analytics cloud service. For more information and details of this process, see [Configure Azure services](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Select the option in the wizard for the **OMS Connector**. 

> [!Note]  
> This article refers to the *Log Analytics Connector*, which was formerly called the *OMS Connector*. There's no functional difference. For more information, see [Azure Management - Monitoring](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

If you accomplished all the other procedures successfully, then the information on the **Connection Configuration** screen automatically appears after you import the web app. Information for the connection settings should appear for your **Azure subscription**, **Azure resource group**, and **Operations Management Suite Workspace**.

The wizard connects to the Log Analytics service using the information you've input. Select the device collections that you want to sync with the cloud service, and then click **Add**.


## Verify the connector properties

After you link Configuration Manager to Log Analytics, view the properties of the connection to add or remove collections. 

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  

2. Select your Log Analytics connection. In the ribbon, select **Properties**.  

The properties page has the following two tabs:  

#### Azure Active Directory
This tab shows the following attributes: 
- **Tenant**  
- **Client ID**  
- **Client secret key expiration**  

Also verify when the client secret key expires.

#### Connection Properties
This tab shows the following attributes: 
- **Azure subscription**  
- **Azure resource group**  
- **Log Analytics Workspace**  

It also shows the list of **Device collections**. Use the **Add** and **Remove** buttons to modify the collections to synchronize.
