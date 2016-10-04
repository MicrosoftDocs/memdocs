---
title: "Monitor content | System Center Configuration Manager"
description: "Understand how to monitor distributed content by using the Configuration Manager console."
ms.custom: na
ms.date: 05/02/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe
---
# Monitor content you have distributed with System Center Configuration Manager
Use the System Center Configuration Manager console to monitor distributed content,  including:  

-   The status for all package types in relation to the associated distribution points  

-   The content validation status for the content in a package  

-   The status of content assigned to a specific distribution point group  

-   The state of content assigned to a distribution point  

-   The status of optional features for each distribution point (Content validation, PXE, and multicast).  

> [!NOTE]  
>  Configuration Manager only monitors the content on a distribution point that is in the content library. Content stored on the distribution point in package or custom shares is not monitored.  

##  <a name="BKMK_ContentStatus"></a> Content status monitoring  
 The **Content Status** node in the **Monitoring** workspace provides information about content packages. In the Configuration Manager console, you can review information like:  

-   The package name  

-   Type  

-   How many distribution points a package has been sent to  

-   The compliance rate  

-   When the package was created  

-   Package ID  

-   Source version  

You also find detailed status information for any package as well as distribution status for the package, including:  

-   The number of failures  

-   pending distributions  

-   The number of installations  

You can also manage distributions that remain in progress to a distribution point or that failed to successfully distribute content to a distribution point:  

-   The applicable option to either cancel or redistribute content is available when you view the deployment status message of a distribution job to a distribution point in the **Asset Details** pane of either the **In Progress** tab or **Error** tab of the **Content Status** node.  

-   Additionally, the job details display the percentage of the job that has completed when you view the details of a job on the **In Progress** tab, and the number of retries that remain for a job as well as how long before the next retry occurs when you view the details of a job that is available from the **Error** tab.  

When you cancel a deployment that is not yet complete, the distribution job to transfer that content stops:  

-   The status of the deployment then updates to indicate the distribution failed and was canceled by a user action.  

-   This new status appears in the **Error** tab.  

> [!TIP]  
>  When a deployment is near completion, it is possible the action to cancel that distribution will not process before the distribution to the distribution point completes. When this occurs, the action to cancel the deployment is ignored, and the status for the deployment displays as successful.  

> [!NOTE]  
>  Although you can select the option to cancel a distribution to a distribution point that is located on a site server, this has no effect. This is because the site server and the distribution point on a site server share the same single instance content store and there is no actual distribution job to cancel.  

When you redistribute content that previously failed to transfer to a distribution point, Configuration Manager immediately begins deploying that content to the distribution point again and updates the status of the deployment to reflect the ongoing state of that redeployment.  

Use the following procedures to view content status and manage distributions that remain in progress or that failed.  

#### To monitor content status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package in which you want detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the package is displayed.  

#### To cancel a distribution that remains in progress  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package you want to manage, and then in the details pane, click **View Status**.  

4.  In the **Asset Details** pane of the **In Progress** tab, right-click on the entry for the distribution that you want to cancel, and select **Cancel**.  

5.  Click **Yes** to confirm the action and cancel the distribution job to that distribution point.  

#### To redistribute content that failed to distribute  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Content Status**. The packages are displayed.  

3.  Select the package you want to manage, and then in the details pane, click **View Status**.  

4.  In the **Asset Details** pane of the **Error** tab, right-click on the entry for the distribution that you want to redistribute, and select **Redistribute**.  

5.  Click **Yes** to confirm the action, and start the redistribution process to that distribution point.  

## Distribution Point Group Status  
The **Distribution Point Group Status** node in the **Monitoring** workspace provides information about distribution point groups. You can review information like:  

-   The distribution point group name  

-   Description  

-   How many distribution points are members of the distribution point group  

-   How many packages have been assigned to the group  

-   Distribution point group status  

-   Compliance rate  

You also view detailed status information for the following:  

-   Errors for the distribution point group,  

-   How many distributions are in progress  

-   How many have been successfully distributed  

#### To monitor distribution point group status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Distribution Point Group Status**. The distribution point groups are displayed.  

3.  Select the distribution point group in which you want detailed status information.  

4.  On the **Home** tab, click **View Status**. Detailed status information for the distribution point group is displayed.  

## Distribution Point Configuration Status  
 The **Distribution Point Configuration Status** node in the **Monitoring** workspace provides information about the distribution point. You can review what attributes are enabled for the distribution point, such as the PXE, multicast, and content validation, and the distribution status for the distribution point. You can also view detailed status information for the distribution point.  

> [!WARNING]  
>  Distribution point configuration status is relative to the last 24 hours. If the distribution point has an error and recovers, the error status might be displayed for up to 24 hours after the distribution point recovers.  

Use the following procedure to view distribution point configuration status.  

#### To monitor distribution point configuration status  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Distribution Status**, and then click **Distribution Point Configuration Status**. The distribution points are displayed.  

3.  Select the distribution point in which you want distribution point status information.  

4.  In the results pane, click the **Details** tab. Status information for the distribution point is displayed.  
