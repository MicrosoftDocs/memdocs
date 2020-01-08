---
title: Monitor content
titleSuffix: Configuration Manager
description: Understand how to monitor distributed content by using the Configuration Manager console.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Monitor content you distribute with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the Configuration Manager console to monitor distributed content, including:  

- The status for all package types for the associated distribution points.  
- The content validation status for the content in a package.  
- The status of content assigned to a specific distribution point group.  
- The state of content assigned to a distribution point.  
- The status of optional features for each distribution point (content validation, PXE, and multicast).  

> [!NOTE]  
> Configuration Manager only monitors the content on a distribution point that's in the content library. It doesn't monitor content stored on the distribution point in package or custom shares.  

## <a name="BKMK_ContentStatus"></a> Content status monitoring

The **Content Status** node in the **Monitoring** workspace provides information about content packages. In the Configuration Manager console, review information like:  

- Package name, type, and ID
- How many distribution points a package has been sent to
- Compliance rate
- When the package was created
- Source version

You also find detailed status information for any package, including:  

- Distribution status
- The number of failures
- Pending distributions  
- The number of installations

You can also manage distributions that remain in progress to a distribution point, or that failed to successfully distribute content to a distribution point:  

- The option to either cancel or redistribute content is available when you view the deployment status message of a distribution job to a distribution point in the **Asset Details** pane. This pane can be found in either the **In Progress** tab or the **Error** tab of the **Content Status** node.  
- Additionally, the job details display the percentage of the job that has completed when you view the details of a job on the **In Progress** tab. The job details also display the number of retries that remain for a job. When you view the details of a job on the **Error** tab, it shows how long before the next retry occurs.  

When you cancel a deployment that's not yet complete, the distribution job to transfer that content stops:  

- The status of the deployment then updates to indicate that the distribution failed, and that it was canceled by a user action.  
- This new status appears in the **Error** tab.  

> [!NOTE]  
> When a deployment is near completion, it's possible the action to cancel that distribution won't process before the distribution to the distribution point completes. When this occurs, the action to cancel the deployment is ignored, and the status for the deployment displays as successful.  
>
> Although you can select the option to cancel a distribution to a distribution point that is located on a site server, this has no effect. This behavior is because the site server and the distribution point on a site server share the same single instance content store. There's no actual distribution job to cancel.  

When you redistribute content that previously failed to transfer to a distribution point, Configuration Manager immediately begins redeploying that content to the distribution point. Configuration Manager updates the status of the deployment to reflect the ongoing state of that redeployment.  

### Tasks to monitor content

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Distribution Status**, and then select the **Content Status** node. This node displays the packages.  

2. Select the package you want to manage.  

3. On the **Home** tab of the ribbon, in the **Content** group, select **View Status**. The console displays detailed status information for the package.

Continue to one of the following sections for additional actions:

#### Cancel a distribution that remains in progress  

1. Switch to the **In Progress** tab.

2. In the **Asset Details** pane, right-click the entry for the distribution that you want to cancel, and select **Cancel**.  

3. Select **Yes** to confirm the action and cancel the distribution job to that distribution point.  

#### Redistribute content that failed to distribute  

1. Switch to the **Error** tab.

2. In the **Asset Details** pane, right-click the entry for the distribution that you want to redistribute, and select **Redistribute**.  

3. Select **Yes** to confirm the action and start the redistribution process to that distribution point.  


## Distribution point group status

The **Distribution Point Group Status** node in the **Monitoring** workspace provides information about distribution point groups. You can review information like:  

- The distribution point group name, description, and status
- How many distribution points are members of the distribution point group
- How many packages have been assigned to the group
- The compliance rate

You also view the following detailed status information:  

- Errors for the distribution point group  
- How many distributions are in progress
- How many have been successfully distributed  

### Monitor distribution point group status  

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Distribution Status**, and then select the **Distribution Point Group Status** node. It displays the distribution point groups.  

2. Select the distribution point group for which you want detailed status information.  

3. On the **Home** tab of the ribbon, select **View Status**. It displays detailed status information for the distribution point group.  


## Distribution point configuration status

The **Distribution Point Configuration Status** node in the **Monitoring** workspace provides information about the distribution point. You can review what attributes are enabled for the distribution point, such as the PXE, multicast, content validation. Also review the distribution status for the distribution point.

> [!WARNING]  
> Distribution point configuration status is relative to the last 24 hours. If the distribution point has an error and recovers, the error status might be displayed for up to 24 hours after the distribution point recovers.  

### Monitor distribution point configuration status  

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Distribution Status**, and then select the **Distribution Point Configuration Status** node.  

2. Select a distribution point.  

3. In the results pane, switch to the **Details** tab. It displays status information for the distribution point.  


## Client Data Sources dashboard

Use the **Client Data Sources** dashboard to better understand from where clients get content in your environment. The dashboard starts displaying data after clients download content and report that information back to the site. This process can take up to 24 hours.

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable the **Client Peer Cache** feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

In the Configuration Manager console, go to the **Monitoring** workspace, expand **Distribution Status**, and select the **Client Data Sources** node. Select a time period to apply to the dashboard. Then select the boundary group for which you want to view information. You can hover your mouse over tiles to see more details about the different content or policy sources.

Also use the report, **Client Data Sources - Summarization**, to view a summary of the client data sources for each boundary group.

### Dashboard tiles

The dashboard includes the following tiles:  

#### Client Content Sources

Displays the sources from which clients got content:

- Distribution point
- [Cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache)
- [Peer Cache](/sccm/core/plan-design/hierarchy/client-peer-cache)
- [Delivery Optimization](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) (starting in version 1906)<sup>[Note 1](#bkmk_note1)</sup>
- Microsoft Update: Devices report this source when the Configuration Manager client downloads software updates from Microsoft cloud services. These services include Microsoft Update and Office 365.

![Client Content Sources tile on the dashboard](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Starting in version 1906<!--3555759-->, to include Delivery Optimization on this dashboard, do the following actions:
>
> - Configure the client setting, **Enable installation of Express Updates on clients** in the Software Updates group
>
> - Deploy Windows 10 express updates
>
> For more information, see [Manage Express installation files for Windows 10 updates](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

#### Distribution points

Displays the number of distribution points that are part of the selected boundary group.

#### Clients that used a distribution point

Of the number of clients that are in the selected boundary group, this tile shows how many used a distribution point to get content.

#### Peer Cache sources

For the selected boundary group, this tile shows how many peer cache sources have reported download history.

#### Clients that used a peer

Of the number of clients that are in the selected boundary group, this tile shows how many used a peer cache source to get content.

#### Top Distributed Content

The most distributed packages by source type
