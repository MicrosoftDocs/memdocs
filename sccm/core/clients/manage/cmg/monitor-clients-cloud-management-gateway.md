---
title: Monitor cloud management gateway
titleSuffix: Configuration Manager
description: Monitor clients and network traffic through the cloud management gateway (CMG).
ms.date: 09/10/2018
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

After the cloud management gateway (CMG) is running and clients are connecting through it, you can monitor clients and network traffic to make sure you know how the service is performing.



## Monitor clients

Clients connected through the CMG appear in the Configuration Manager console the same way on-premises clients do. For more information, see [how to monitor clients](/sccm/core/clients/manage/monitor-clients).



## Monitor traffic in the console

Monitor traffic on the CMG using the Configuration Manager console:

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  

2. Select the CMG in the list pane.  

3. View the traffic information in the details pane for the CMG connection point and the site system roles it connects to.  



## Set up outbound traffic alerts

Outbound traffic alerts help you know when network traffic approaches a 14-day threshold level. When you create the CMG, you can set up traffic alerts. If you skipped that part, you can still set up the alerts after the service is running. Adjust the alert settings at any time.

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  

2. Select the CMG in the list pane, and then select **Properties** in the ribbon.  

3. Go to the **Alerts** tab to enable the threshold and alerts. Specify the 14-day data threshold in gigabytes (GB). Also specify the threshold percentage to raise the different alert levels.  

4. When you're done, select **OK**.  



## Monitor logs

The CMG generates entries in a number of log files. For more information, see [Configuration Manager logs](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## Cloud management dashboard
<!--1358461-->
Starting in version 1806, the cloud management dashboard provides a centralized view for CMG usage. When the site is onboarded to [Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for cloud management, it also displays data about cloud users and devices.  

The following screenshot is a portion of the cloud management dashboard showing two of the available tiles:  
![Cloud management dashboard tiles CMG traffic and Current online clients](media/1358461-cmg-dashboard.png)

In the Configuration Manager console, go to the **Monitoring** workspace. Select the **Cloud Management** node, and view the dashboard tiles.  



## Connection analyzer

Starting in version 1806, use the CMG connection analyzer for real-time verification to aid troubleshooting. The in-console utility checks the current status of the service, and the communication channel through the CMG connection point to any management points that allow CMG traffic.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services** and select the **Cloud management gateway** node.  

2. Select the target CMG instance, and then select **Connection analyzer** in the ribbon.  

3. In the CMG connection analyzer window, select one of the following options to authenticate with the service:  

     1. **Azure AD user**: use this option to simulate communication the same as a cloud-based user identity signed in to an Azure AD-joined Windows 10 device. Click **Sign In** to securely enter the credentials for this Azure AD user account.  

     2. **Client certificate**: use this option to simulate communication the same as a Configuration Manager client with a [client authentication certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Select **Start** to start the analysis. The analyzer window displays the results. Select an entry to see more details in the Description field.  

