---
title: Monitor client deployment status
titleSuffix: Configuration Manager
description: Monitor client deployment status in Configuration Manager.
ms.date: 04/23/2017
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to monitor client deployment status in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Deploying clients across your site takes time and some installations are not successful the first time. The Configuration Manager console provides a way to keep an eye on client deployments within a collection by reporting client deployment status in real time.  

> [!NOTE]  
>  The best and most reliable way to monitor client deployment is with the Configuration Manager console (as described in this article). The **Client Status** section of the **Monitoring** workspace in the console provides client deployment status accurately and in real time. You can monitor client deployments with other tools, such as Server Manager  in Windows Server or System Center Operations Manager, but you may receive alarms from normal client installation activity. Because of how the client installation program (CCMSetup.exe) runs in various environments, these other tools may generate false alarms and warnings that do not accurately reflect the state of client deployments.  

 In the **Monitoring** workspace of the console, you can monitor the following statuses for client deployments taking place within a collection that you specify:  

- Compliant  

- In progress  

- Not compliant  

- Failed  

- Unknown  

  Configuration Manager reports on deployments for production clients or pre-production clients. The Configuration Manager console also provides a chart of failed client deployments over a specified period of time to help you determine if actions you to take to troubleshoot deployments are improving the deployment success rate over time.  

## To monitor client deployments  

- In the Configuration Manager console, click **Monitoring** > **Client Status**.  

- Click **Production Client Deployment** or **Pre-production Client Deployment** depending on the version of client you want to monitor.  

- Review the charts of client deployment status and client deployment failure.  

- If you want to change the scope of the report, click **Browse...** and choose a different collection.  

  To learn more about pre-production client deployments, see [How to test client upgrades in a pre-production collection](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > The deployment status on computers hosting site system roles in a pre-production collection may be reported as **Not compliant** even when the client was successfully deployed. When you promote the client to production, the deployment status is reported correctly.   

  To monitor the status of deployed clients, see [How to monitor clients](../../../core/clients/manage/monitor-clients.md)  

  You can use Configuration Manager reports to find out more information about the status of clients in your site. For more information about how to run reports, see [Introduction to reporting](../../servers/manage/introduction-to-reporting.md).  
