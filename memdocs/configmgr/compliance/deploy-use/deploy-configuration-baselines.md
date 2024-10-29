---
title: Deploy configuration baselines
titleSuffix: Configuration Manager
description: Deploy configuration baselines to define configuration baseline deployments and to add or remove configuration baselines from deployments.
ms.date: 10/06/2016
ms.service: configuration-manager
ms.subservice: compliance
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to deploy configuration baselines in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration baselines in Configuration Manager must be deployed to one or more collections of users or devices before client devices in those collections can assess their compliance with the configuration baseline.  

Use the **Deploy Configuration Baselines** dialog box to define configuration baseline deployments, which includes adding or removing configuration baselines from deployments in addition to specifying the evaluation schedule.  

## Deploy a configuration baseline  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Baselines**.  

3.  In the **Configuration Baselines** list, select the configuration baseline that you want to deploy, and then in the **Home** tab, in the **Deployment** group, click **Deploy**.  

4.  In the **Deploy Configuration Baselines** dialog box, select the configuration baselines that you want to deploy in the **Available configuration baselines** list. Click **Add** to add these to the **Selected configuration baselines** list.  

    > [!IMPORTANT]  
    >  If you change a configuration item that has been added to a deployed configuration baseline, the revised configuration item is not evaluated for compliance until its next scheduled evaluation time.  

5.  Specify the following additional information:  

    -   **Remediate noncompliant rules when supported** – Automatically remediates any rules that are noncompliant for Windows Management Instrumentation (WMI), the registry, scripts, and all settings for mobile devices that are enrolled by Configuration Manager.  

    -   **Allow remediation outside the maintenance window** – If a maintenance window has been configured for the collection to which you are deploying the configuration baseline, enable this option to let compliance settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Generate an alert** – Configures an alert that is generated if the configuration baseline compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  

7.  **Collection** - Click **Browse** to select the collection where you want to deploy the configuration baseline.  

8.  **Specify the compliance evaluation schedule for this configuration baseline** Specifies the schedule by which the deployed configuration baseline is evaluated on client computers. This can be either a simple or a custom schedule.  

    > [!NOTE]  
    >  If the configuration baseline is deployed to a computer, it is evaluated for compliance within two hours of the start time that you schedule. If it is deployed to a user, it is evaluated for compliance when the user logs on.  

9. Click **OK** to close the **Deploy Configuration Baselines** dialog box and to create the deployment. For more information about how to monitor the deployment, see [Monitor compliance settings](monitor-compliance-settings.md).  
