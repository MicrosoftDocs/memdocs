---
title: Pull-distribution point
titleSuffix: Configuration Manager
description: Learn about configurations and limitations for using a pull-distribution point with Configuration Manager."
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use a pull-distribution point with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


When you distribute content to a standard distribution point in the Configuration Manager console, the site server pushes the content to the distribution point. A pull-distribution point gets content by downloading it from a source location like a client.  

When you distribute content to many distribution points, pull-distribution points help reduce the processing load on the site server. They can also speed the content transfer to each server. Normally the distribution manager component on the site server sends content to each distribution point. Instead, the site offloads the process of transferring the content to the pull-distribution points.  

You configure individual distribution points to be pull-distribution points. For each pull-distribution point, specify one or more source distribution points from which it can get content. A pull-distribution point can only download content from a distribution point that you specify as a source distribution point. 

When you distribute content to a pull-distribution point in the console, the site server sends it a notification. The pull-distribution point then downloads the content from a source distribution point. A pull-distribution point manages the content transfer by downloading from a distribution point that already has a copy of the content.  

Pull-distribution points support the same configurations and functionality as typical distribution points. For example, a pull-distribution point supports: 
- Multicast and PXE configurations
- Content validation
- On-demand content distribution
- HTTP or HTTPS communications from clients
- The same certificate options as other distribution points
- Manage individually or as a member of a distribution point group  

> [!IMPORTANT]  
> Although a pull-distribution point supports communications over HTTP and HTTPS, when you use the Configuration Manager console, you can only specify source distribution points that are configured for HTTP. You can use the Configuration Manager SDK to specify a source distribution point that is configured for HTTPS.  

Configure a pull-distribution point when you install the distribution point. After you create a distribution point, configure it as a pull-distribution point by editing the role properties. For more information on how to enable a distribution point as a pull-distribution point, see [Pull-distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pull-distribution-point).  

Remove the configuration to be a pull-distribution point by editing the properties of the distribution point. When you remove the configuration as a pull-distribution point, it returns to normal operation. The site server manages future content transfers to the distribution point.  



### Distribution process

When you distribute content to a pull-distribution point, the following sequence of events occurs:

-   Once you distribute content to a pull-distribution point in the console, the Package Transfer Manager component on the site server checks the site database to confirm if the content is available on a source distribution point. If it can't confirm that the content is on a source distribution point for the pull-distribution point, it repeats the check every 20 minutes until the content is available.  

-   When the Package Transfer Manager confirms that the content is available, it notifies the pull-distribution point to download the content. If this notification fails, it retries based on the Software Distribution component **Retry settings** for pull-distribution points. When the pull-distribution point receives this notification, it tries to download the content from its source distribution points.  

-   While the pull-distribution point downloads the content, the Package Transfer Manager polls the status based on the Software Distribution component **Status polling settings** for pull-distribution points.  When the pull-distribution point completes the download of content, it submits this status to a management point.  



## Configure site component settings

When you use a pull-distribution point, review and configure the following site component settings:  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2.  Select the site. In the ribbon, click **Configure Site Components**, and select **Software Distribution**.  

3. Switch to the **Pull Distribution Point** tab.  

4.  In the **Retry settings** group, review the following values:  

    -   **Number of retries**: The number of times that the Package Transfer Manager tries to notify the pull-distribution point to download the content. After it tries this number of times, the Package Transfer Manager cancels the transfer. This value is 30 by default.  

    -   **Delay before retrying (minutes)**: The number of minutes that the Package Transfer Manager waits between attempts. This value is 20 by default.  

5.  In the **Status polling settings** group, review the following values:  

    -   **Number of polls**: The number of times that the Package Transfer Manager contacts the pull-distribution point to retrieve the job status. If it tries this number of times before the job completes, the Package Transfer Manager cancels the transfer. This value is 72 by default.   

    -   **Delay before retrying (minutes)**: The number of minutes that the Package Transfer Manager waits between attempts. This value is 60 by default.   
    
    > [!NOTE]  
    >  When the Package Transfer Manager cancels a job because it exceeds the number of polling retries, the pull-distribution point continues to download the content. When it finishes, the pull-distribution point sends the appropriate status message, and the console reflects the new status.  
    


## Limitations 

-   You can't configure a cloud distribution point as a pull-distribution point.  

-   You can't configure the distribution point role on a site server as a pull-distribution point.  

-   The prestage content configuration overrides the pull-distribution point configuration. If you turn on the option to **Enable this distribution point for prestaged content** on a pull-distribution point, it waits for the content. It doesn't pull content from the source distribution point. Like a standard distribution point enabled for prestaged content, it doesn't receive content from the site server. For more information, see [Prestaged content](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

-   A pull-distribution point doesn't use schedule or rate limit configurations. When you configure a previously installed distribution point to be a pull-distribution point, configurations for schedule and rate limits are saved, but not used. If you later remove the pull-distribution point configuration, the schedule and rate limit configurations are implemented as previously configured.  

    > [!NOTE]  
    >  The **Schedule** and **Rate Limits** tabs aren't visible in the properties of the distribution point.  

-   Pull-distribution points don't use the settings on the **General** tab of the **Software Distribution Component Properties** for each site. These settings include **Concurrent distribution** and **Multicast retry**.  

-   To transfer content from a source distribution point in a remote forest, install the Configuration Manager client on the pull-distribution point. Also configure a network access account that can access the source distribution point. Starting in version 1806, if you enable the site option to **Use Configuration Manager-generated certificates for HTTP site systems**, then you don't need a network access account.<!--1358228-->  

-   If the pull-distribution point is also a Configuration Manager client, the client version must be the same as the Configuration Manager site that installs the pull-distribution point. The pull-distribution point uses the CCMFramework that is common to both the pull-distribution point and the Configuration Manager client.  



## About source distribution points  

When you configure the pull-distribution point, specify one or more source distribution points:  

-   The wizard only displays distribution points that qualify to be source distribution points.  

-   A pull-distribution point can be specified as a source distribution point for another pull-distribution point.  

-   Only distribution points that support HTTP can be specified as source distribution points when you use the Configuration Manager console.  

-   Use the Configuration Manager SDK to specify a source distribution point that's configured for HTTPS. To use a source distribution point that's configured for HTTPS, install the Configuration Manager client on the pull-distribution point.  

-   Starting in version 1806, if your remote offices have a better connection to the internet, or to reduce load on your WAN links, use a [cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in Microsoft Azure as the source. The pull-distribution point needs internet access to communicate with Microsoft Azure. The content must be distributed to the source cloud distribution point.<!--1321554-->  

    > [!Note]  
    > This feature does incur charges to your Azure subscription for data storage and network egress. For more information, see the [Cost of using a cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  


> [!Tip]  
> When a pull-distribution point downloads content from a source distribution point, that pull-distribution point is counted as a client in the **Client Accessed (Unique)** column of the **Distribution point usage summary** report.  


### Source priorities

-   Assign a separate priority to each source distribution point, or assign multiple source distribution points to the same priority.  

-   The priority determines the order in which the pull-distribution point requests content from its source distribution points.  

-   Pull-distribution points initially contact a source distribution point with the lowest value for priority. If there are multiple source distribution points with the same priority, the pull-distribution point randomly selects one of the sources with that priority.  

-   If the content isn't available on a selected source, the pull-distribution point then tries to download the content from another distribution point with that same priority.  

-   If none of the distribution points with a given priority has the content, the pull-distribution point tries to download the content from a source distribution point with the next priority level. It continues this search until the content is located.   

- If none of the assigned source distribution points have the content, the pull-distribution point waits for 30 minutes, and then starts the process again.  



## Inside the pull-distribution point 

-   To manage the transfer of content, pull-distribution points use the **CCMFramework** component. The Configuration Manager client includes this component.  

-   When you enable the pull-distribution point, the site installs **pulldp.msi**. This installer also adds the CCMFramework component. The framework doesn't require the Configuration Manager client.  

-   After the pull-distribution point is installed, it primarily uses the **CCMExec** service to function.  

-   When the pull-distribution point transfers content, it uses the **Background Intelligent Transfer Service** (BITS) built into Windows. A pull-distribution point doesn't require that you install the BITS Extension for IIS Server.<!--sms.503672 -Clarified BITS use-->

-  For operational details, see the following log files on the pull-distribution point:  
    - **DataTransferService.log**
    - **PullDP.log**



## See also  
 [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
