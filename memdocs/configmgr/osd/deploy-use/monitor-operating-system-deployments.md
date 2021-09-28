---
title: Monitor operating system deployments
titleSuffix: Configuration Manager
description: To help you to monitor operating system deployment objects, the Configuration Manager console provides alerts, reports, and various status indicators.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Monitor operating system deployments in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The Configuration Manager console provides the following ways to help you monitor operating system deployment objects.  


##  <a name="BKMK_OSDAlerts"></a> Alerts for operating system deployments  
 You can configure an alert in the task sequence  deployment settings to notify administrative users when compliance levels for the  deployment is below the configured percentage.  

 After you configure the alert settings, if the specified conditions occur, Configuration Manager generates an alert. You can review task sequence deployment alerts at the following locations:  

1.  Review recent alerts in the **Operating Systems** node in the **Software Library** workspace.  

2.  Manage the configured alerts in the **Alerts** node in the **Monitoring** workspace.  

##  <a name="BKMK_TSDeployStatus"></a> Task sequence deployment status  
 After you deploy a task sequence, you can monitor the deployment status. Use the following procedure to monitor the deployment status for a task sequence.  

#### To monitor deployment status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the Monitoring workspace, click **Deployments**.  

3.  Click the task sequence  for which you want to monitor the deployment status.  

4.  On the **Home** tab, in the **Deployment** group, click **View Status**.  

> [!NOTE]  
> When an upgrade is initiated, status message 52200 is generated. This contains the user that did the upgrade.  

##  <a name="BKMK_TSReports"></a> Operating system deployment reports  
 There are many predefined operating system deployment reports available. They are organized in several categories and can be used to report on specific information about state migration and task sequence deployments. In addition to using the preconfigured reports, you can also create custom software update reports according to the needs of your enterprise. For more information, see [Operations and maintenance for reporting](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Monitor content  
 You can monitor content in the Configuration Manager console to review the status for all package types in relation to the associated distribution points. This can include the content validation status for the content in the package, the status of content assigned to a specific distribution point group, the state of content assigned to a distribution point, and the status of optional features for each distribution point (content validation, PXE, and multicast).  

###  <a name="BKMK_ContentStatus"></a> Content status monitoring  
 The **Content Status** node in the **Monitoring** workspace provides information about content packages. You can review general information about the package, distribution status for the package, and detailed status information about the package. Use the following procedure to view content status.  

#### To monitor content status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the Monitoring workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package for which to view detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the package is displayed.  

###  <a name="BKMK_DPGroupStatus"></a> Distribution point group status  
 The **Distribution Point Group Status** node in the **Monitoring** workspace provides information about distribution point groups. You can review general information about the distribution point group, such as distribution point group status and compliance rate, as well as detailed status information for the distribution point group. Use the following procedure to view distribution point group status.  

#### To monitor distribution point group status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the monitoring workspace, expand **Distribution Status**, and then click **Distribution Point Group Status**. The distribution point groups are displayed.  

3.  Select the distribution point group for which to view detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the distribution point group is displayed.  

###  <a name="BKMK_DPConfigStatus"></a> Distribution point configuration status  
 The **Distribution Point Configuration Status** node in the **Monitoring** workspace provides information about the distribution point. You can review which attributes are enabled for the distribution point, such as the PXE, Multicast, and content validation. You can also view detailed status information for the distribution point. Use the following procedure to view distribution point configuration status.  

#### To monitor distribution point configuration status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the monitoring workspace, expand **Distribution Status**, and then click **Distribution Point Configuration Status**. The distribution points are displayed.  

3.  Select the distribution point for which to view distribution point status information.  

4.  In the results pane, click the **Details** tab. Status information for the distribution point is displayed.  
