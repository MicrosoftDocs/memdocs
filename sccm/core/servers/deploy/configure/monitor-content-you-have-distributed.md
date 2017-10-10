---
title: "Monitor content"
description: "Understand how to monitor distributed content by using the Configuration Manager console."
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Monitor content you have distributed with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the System Center Configuration Manager console to monitor distributed content, including:  

-   The status for all package types in relation to the associated distribution points.  
-   The content validation status for the content in a package.  
-   The status of content assigned to a specific distribution point group.  
-   The state of content assigned to a distribution point.  
-   The status of optional features for each distribution point (content validation, PXE, and multicast).  

> [!NOTE]  
>  Configuration Manager only monitors the content on a distribution point that is in the content library. Content stored on the distribution point in package or custom shares is not monitored.  

##  <a name="BKMK_ContentStatus"></a> Content status monitoring  
 The **Content Status** node in the **Monitoring** workspace provides information about content packages. In the Configuration Manager console, you can review information like:  

-   The package name.  
-   The type.  
-   How many distribution points a package has been sent to.  
-   The compliance rate.  
-   When the package was created.  
-   The package ID.  
-   The source version.  

You also find detailed status information for any package, as well as distribution status for the package, including:  

-   The number of failures.  
-   Pending distributions.  
-   The number of installations.

You can also manage distributions that remain in progress to a distribution point, or that failed to successfully distribute content to a distribution point:  

-   The option to either cancel or redistribute content is available when you view the deployment status message of a distribution job to a distribution point in the **Asset Details** pane. This pane can be found in either the **In Progress** tab or the **Error** tab of the **Content Status** node.  
-   Additionally, the job details display the percentage of the job that has completed when you view the details of a job on the **In Progress** tab. The job details also display the number of retries that remain for a job, as well as how long before the next retry occurs when you view the details of a job that is available from the **Error** tab.  

When you cancel a deployment that is not yet complete, the distribution job to transfer that content stops:  

-   The status of the deployment then updates to indicate that the distribution failed, and that it was canceled by a user action.  
-   This new status appears in the **Error** tab.  

> [!TIP]  
>  When a deployment is near completion, it is possible the action to cancel that distribution will not process before the distribution to the distribution point completes. When this occurs, the action to cancel the deployment is ignored, and the status for the deployment displays as successful.  

> [!NOTE]  
>  Although you can select the option to cancel a distribution to a distribution point that is located on a site server, this has no effect. This is because the site server and the distribution point on a site server share the same single instance content store. There is no actual distribution job to cancel.  

When you redistribute content that previously failed to transfer to a distribution point, Configuration Manager immediately begins redeploying that content to the distribution point. Configuration Manager updates the status of the deployment to reflect the ongoing state of that redeployment.  

Use the following procedures to view content status, and manage distributions that remain in progress or that failed.  

### To monitor content status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package for which you want detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the package is displayed.  

### To cancel a distribution that remains in progress  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package you want to manage, and then in the details pane, click **View Status**.  

4.  In the **Asset Details** pane of the **In Progress** tab, right-click the entry for the distribution that you want to cancel, and select **Cancel**.  

5.  Click **Yes** to confirm the action and cancel the distribution job to that distribution point.  

### To redistribute content that failed to distribute  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package you want to manage, and then in the details pane, click **View Status**.  

4.  In the **Asset Details** pane of the **Error** tab, right-click the entry for the distribution that you want to redistribute, and select **Redistribute**.  

5.  Click **Yes** to confirm the action and start the redistribution process to that distribution point.  

## Distribution point group status  
The **Distribution Point Group Status** node in the **Monitoring** workspace provides information about distribution point groups. You can review information like:  

-   The distribution point group name.  
-   The description.  
-   How many distribution points are members of the distribution point group.  
-   How many packages have been assigned to the group.  
-   The distribution point group status.  
-   The compliance rate.  

You also view detailed status information for the following:  

-   Errors for the distribution point group.  
-   How many distributions are in progress.
-   How many have been successfully distributed.  

### To monitor distribution point group status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Distribution Point Group Status**. The distribution point groups are displayed.  

3.  Select the distribution point group for which you want detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the distribution point group is displayed.  

## Distribution point Configuration Status  
 The **Distribution Point Configuration Status** node in the **Monitoring** workspace provides information about the distribution point. You can review what attributes are enabled for the distribution point, such as the PXE, multicast, content validation, and the distribution status for the distribution point. You can also view detailed status information for the distribution point.  

> [!WARNING]  
>  Distribution point configuration status is relative to the last 24 hours. If the distribution point has an error and recovers, the error status might be displayed for up to 24 hours after the distribution point recovers.  

Use the following procedure to view distribution point configuration status.  

### To monitor distribution point configuration status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Distribution Point Configuration Status**. The distribution points are displayed.  

3.  Select the distribution point for which you want distribution point status information.  

4.  In the results pane, click the **Details** tab. Status information for the distribution point is displayed.  

## Client Data Sources dashboard
Beginning with version 1610, you can use the **Client Data Sources** dashboard to help understand the use of [Peer Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) in your environment. The dashboard will start displaying data after clients download content and report that information back to the site. This can take up to 24 hours.

> [!TIP]  
> **Client Peer Cache** and the **Client Data Sources** dashboard are pre-release features introduced in version 1610. You must enable Client Peer Cache before the Client Data Sources dashboard becomes visible in the console. To enable Client Peer Cache, see [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease). It can take up to 24 hours after you enable it to start displaying data.

In the console, go to **Monitoring** > **Distribution Status** > **Client Data Sources**. Here you can select a time period to apply to the dashboard. Then, in the display, you can select the boundary group or package for which you want to view information. When viewing information, you can hover your mouse over the surface to see more details about the different content or policy sources.

Those details include the following:  
- **Client Content Sources**: Displays the source from which clients got content.
- **Distribution points**: Displays the number of distribution points that are part of the selected Boundary Group.
- **Clients that used a distribution point**: Of the number of clients that are in the selected Boundary Group, this shows how many used a distribution point to get content.
- **Peer Cache sources**: For the selected Boundary Group, this shows how many peer cache sources have reported download history.
- **Clients that used a peer**: Of the number of clients that are in the selected Boundary Group, this shows how many used a peer cache source to get content.



You can also use a new report, **Client Data Sources - Summarization**, to view a summary of the client data sources for each boundary group.
