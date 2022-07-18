---
title: Monitor software updates
titleSuffix: Configuration Manager
description: The Configuration Manager console provides alerts and statuses to monitor updates and compliance.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/12/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.localizationpriority: medium
---
# Monitor software updates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager provides many ways to help you to monitor software updates objects, processes, and compliance information. Use the following sections to monitor software updates.

## Software updates dashboard

You can use the Software Updates Dashboard to view the current compliance status of devices in your organization and quickly analyze the data to see which devices are at risk. To view the dashboard, navigate to **Monitoring** > **Overview** > **Security** > **Software Updates Dashboard**.

## Drill through required updates
<!--4224414-->
You can drill through compliance statistics to see which devices require a specific Microsoft 365 Apps software update. To view the device list, you need permission to view updates and the collections the devices belong to. To drill down into the device list:

1. Go to **Software Library** > **Software Updates** > **All Software Updates**.
1. Select any update that is required by at least one device.
1. Look at the **Summary** tab and find the pie chart under  **Statistics**.
1. Select the **View Required** hyperlink next to the pie chart to drill down into the device list.
1. This action takes you to a temporary node under **Devices** where you can see the devices requiring the update. You can also take actions for the node such as creating a new collection from the list.


##  <a name="BKMK_SUAlerts"></a> Alerts for software updates  
 You can configure alerts for software updates to notify administrative users when compliance levels for software update deployments are below the configured percentage. You can configure alerts for software update deployments in the following locations:  

-   ADR setting: You can configure the alerts settings in the Automatic Deployment Rule Wizard and in the properties for the ADR.  

-   Deployment setting: You can configure the alerts settings in the Deploy Software Updates Wizard and in deployment properties.  

After you configure the alert settings, if the specified conditions occur, Configuration Manager generates an alert. You can review software update alerts at the following locations:  

1.  Review recent alerts in the **Software Updates** node in the **Software Library** workspace.  

2.  Manage the configured alerts in the **Alerts** node in the **Monitoring** workspace.  

##  <a name="BKMK_SUSyncStatus"></a> Software updates synchronization status  
 After you start the synchronization process, you can monitor the synchronization process from the Configuration Manager console for all software update points in your hierarchy. Use the following procedure to monitor the software update synchronization process.  

#### To monitor the software updates synchronization process  

- In the Configuration Manager console, navigate to **Monitoring** > **Overview** > **Software Update Point Synchronization Status**.  

    The software update points in your Configuration Manager hierarchy are displayed in the results pane. From this view, you can monitor the synchronization status for all software update points. To see more detailed information about the synchronization process, you can review the wsyncmgr.log file, which is located in <*ConfigMgrInstallationPath*>\Logs on each site server.  

##  <a name="BKMK_SUDeployStatus"></a> Software update deployment status  
 After you deploy the software updates in a software update group or deploy an individual software update, you can monitor the deployment status. Use the following procedure to monitor the deployment status for a software update group or software update.  

#### To monitor deployment status  

1. In the Configuration Manager console, navigate to **Monitoring** > **Overview** > **Deployments**.  

1. Click the software update group or software update for which you want to monitor the deployment status.  

1. On the **Home** tab, in the **Deployment** group, click **View Status**. 

> [!TIP]
> - Starting in version 2107, you can right-click the status of a deployment and select **Evaluate Software Update Deployments** to send a notification to the selected devices to run a software update deployment evaluation cycle.
> - Starting in version 2203, you can perform client notification actions, including **Run Scripts**, from the **Deployment Status** view. Use the right-click menu on either a group of clients in a **Category** or a single client in the **Asset details** pane to display the client notification actions. <!--7079837-->


##  <a name="BKMK_SUReports"></a> Software updates reports  
 The state messages for software updates provide information about the compliance of software updates and about the evaluation and enforcement state of software update deployments. You can run software update reports to display these state messages. There are more than 30 predefined software update reports available. They're organized in several categories and can be used to report on specific information about software updates and deployments. In addition to using the preconfigured reports, you can also create custom software update reports according to the needs of your enterprise. For more information, see [Operations and maintenance for reporting](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

> [!NOTE]
> Devices running an unsupported operating systems will display as compliant since there aren't applicable updates to the operating system any longer. <!--13952160-->

### Recommended software updates reports
The following are some of the reports that are useful in identifying potential issues: 

#### Compliance 9 - Overall health and compliance (starting in version 1806)
The report includes the following parts:

- **Healthy Clients vs Total Clients**: This bar chart compares the "healthy" clients that have communicated with the site in the specified time period against the total number of clients in the specified collection.
- **Compliance Overview**: This pie chart shows overall compliance state for the specific software update group on active clients in the specified collection.
- **Top 5 Non-Compliant by Article ID**: This bar chart displays the top five software updates in the specified group that are non-compliant on active clients in the specified collection.
- The bottom of the report is a table with further details, which lists the software updates in the specified group.

#### Management 2 - Updates required but not deployed

This report displays vendor-specific software updates in a specific updates classification that have been detected as required on clients but that have not been deployed to a specific collection. 

#### Troubleshooting 2 - Deployment errors

This report returns the deployment errors at the site and a count of computers that are experiencing each error. 


##  <a name="BKMK_MonitorContent"></a> Monitor content  
 You can monitor content in the Configuration Manager console to review the status for all package types in relation to the associated distribution points. This can include the content validation status for the content in the package, the status of content assigned to a specific distribution point group, the state of content assigned to a distribution point, and the status of optional features for each distribution point (content validation, PXE, and multicast).  

###  <a name="BKMK_ContentStatus"></a> Content status monitoring  
 The **Content Status** node in the **Monitoring** workspace provides information about content packages. You can review general information about the package, distribution status for the package, and detailed status information about the package. Use the following procedure to view content status.  

#### To monitor content status  

1.  In the Configuration Manager console, navigate to **Monitoring** > **Overview** > **Distribution Status** > **Content Status**. The packages are displayed.  

2.  Select the package for which to view detailed status information.  

3.  On the **Home** tab, click **View Status**. Detailed status information for the package is displayed.  

###  <a name="BKMK_DPGroupStatus"></a> Distribution point group status  
 The **Distribution Point Group Status** node in the **Monitoring** workspace provides information about distribution point groups. You can review general information about the distribution point group, such as distribution point group status and compliance rate, as well as detailed status information for the distribution point group. Use the following procedure to view distribution point group status.  

#### To monitor distribution point group status  

1.  In the Configuration Manager console, navigate to **Monitoring** > **Overview** > **Distribution Status** > **Distribution Point Group Status**. The distribution point groups are displayed.  

2.  Select the distribution point group for which to view detailed status information.  

3.  On the **Home** tab, click **View Status**. Detailed status information for the distribution point group is displayed.  

###  <a name="BKMK_DPConfigStatus"></a> Distribution point configuration status  
 The **Distribution Point Configuration Status** node in the **Monitoring** workspace provides information about the distribution point. You can review which attributes are enabled for the distribution point, such as the PXE, Multicast, and content validation. You can also view detailed status information for the distribution point. Use the following procedure to view distribution point configuration status.  

#### To monitor distribution point configuration status  

1.  In the Configuration Manager console, navigate to **Monitoring** > **Overview** > **Distribution Status** > **Distribution Point Configuration Status**. The distribution points are displayed.  

2.  Select the distribution point for which to view distribution point status information.  

3.  In the results pane, click the **Details** tab. Status information for the distribution point is displayed.  

## Next steps

- [Log files for Software Updates](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Software Updates management whitepaper](https://www.microsoft.com/download/confirmation.aspx?id=44578)
