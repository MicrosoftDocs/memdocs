---
title: "Pull-distribution point"
titleSuffix: "Configuration Manager"
description: "Learn about configurations and limitations for using a pull-distribution point with System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: 9
author: aczechowski
ms.author: aaroncz
manager: angrobe

---

# Use a pull-distribution point with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


A pull-distribution point for System Center Configuration Manager is a standard distribution point that obtains distributed content by downloading it from a source location like a client, instead of having the content pushed to it from the site server.  

 When you deploy content to a large number of distribution points at a site, pull-distribution points can help reduce the processing load on the site server and speed the transfer of the content to each distribution point. This efficiency is achieved by offloading the process of transferring the content to each distribution point from the distribution manager process on the site server.  

-   You configure individual distribution points to be pull-distribution points.  

-   For each pull-distribution point, you must specify one or more source distribution points from which it can get deployments (a pull-distribution point can only obtain content from a distribution point that is specified as a source distribution point).  

-   When you distribute content to a pull-distribution point, the site server notifies the pull-distribution point, which then initiates the download (transfer) of the content from a source distribution point. A pull-distribution point individually manages the transfer of content by downloading content from a distribution point that already has a copy of the content.  

Pull-distribution points support the same configurations and functionality as typical Configuration Manager distribution points. For example, a distribution point that is configured as a pull-distribution point supports the use of multicast and PXE configurations, content validation, and on-demand content distribution. A pull-distribution point supports HTTP or HTTPS communications from clients, supports the same certificates options as other distribution points, and can be managed individually or as a member of a distribution point group.  

> [!IMPORTANT]
> Although a pull-distribution point supports communications over HTTP and HTTPS, when you use Configuration Manager, you can only specify source distribution points that are configured for HTTP. You can use the Configuration Manager SDK to specify a source distribution point that is configured for HTTPS.  

 **The following sequence of events occurs when you distribute content to a pull-distribution point:**  

-   As soon as content is distributed to a pull-distribution point, the Package Transfer Manager on the site server checks the site database to confirm if the content is available on a source distribution point. If it cannot confirm that the content is on a source distribution point for the pull-distribution point, it repeats the check every 20 minutes until the content is available.  

-   When the Package Transfer Manager confirms that the content is available, it notifies the pull-distribution point to download the content. If this notification fails it will retry based on the Software Distribution Component **Retry settings** for pull-distribution points. When the pull-distribution point receives this notification, it attempts to download the content from its source distribution points.  

-   While the pull-distribution point downloads the content the Package Transfer Manager will poll the status based on the Software Distribution Component **Status polling settings** for pull-distribution points.  When the pull-distribution point completes the download of content, it submits this status to a management point.

**You can configure a pull-distribution point** when you install the distribution point or after it is installed by editing the properties of the distribution point site system role.  

**You can remove the configuration to be a pull-distribution point** by editing the properties of the distribution point. When you remove the pull-distribution point configuration, the distribution point returns to normal operations, and the site server manages future content transfers to the distribution point.  

## To configure Software Distribution Component for pull-distribution points

1.  In the Configuration Manager console, choose **Administration** > **Sites**.  

2.  Select the desired site and select **Configure Site Components** > **Software Distribution**

3. Select the **Pull Distribution Point** tab.  

4.  In the **Retry settings** list, configure the following values:  

    -   **Number of retries** - The number of times that the Package Transfer Manager attempts to notify the pull-distribution point to download the content.  If this number is exceeded the Package Transfer Manager will cancel the transfer.

    -   **Delay before retrying (minutes)** - The number of minutes that the Package Transfer Manager will wait between attempts. 

5.  In the **Status polling settings** list, configure the following values:  

    -   **Number of polls** - The number of times that the Package Transfer Manager contacts the pull-distribution point to retrieve the job status.  If this number is exceeded before the job completes the Package Transfer Manager will cancel the transfer.

    -   **Delay before retrying (minutes)** - The number of minutes that the Package Transfer Manager will wait between attempts. 
    
    > [!NOTE]  
    >  When the Package Transfer Manager cancels a job because the number of Status polling retries has been exceeded the pull-distribution point will continue to download the content.  When it finishes, the appropriate status message will be sent to the Package Transfer Manager and the console will reflect the new status.
    
## Limitations for pull-distribution points  

-   A cloud-based distribution point cannot be configured as a pull-distribution point.  

-   A distribution point on a site server cannot be configured as a pull-distribution point.  

-   **The prestage content configuration overrides the pull-distribution point configuration**. A pull-distribution point that is configured for prestaged content waits for the content. It does not pull content from the source distribution point, and, like a standard distribution point that has the prestage content configuration, does not receive content from the site server.  

-   **A pull-distribution point does not use configurations for schedule or rate limits** when it transfers content. If you configure a previously installed distribution point to be a pull-distribution point, configurations for schedule and rate limits are saved, but not used. If you later remove the pull-distribution point configuration, the schedule and rate limit configurations are implemented as previously configured.  

    > [!NOTE]  
    >  When a distribution point is configured as a pull-distribution point, the **Schedule** and **Rate Limits** tabs are not visible in the properties of the distribution point.  

-   Pull-distribution points do not use the settings on the **General** tab of the **Software Distribution Component Properties** for each site.  This includes the **Concurrent distribution** and **Multicast retry** setting.  Use the **Pull Distribution Point** tab to configure settings for pull-distribution points.

-   To transfer content from a source distribution point in a remote forest, the computer that hosts the pull-distribution point must have a Configuration Manager client installed. A Network Access Account that can access the source distribution point must be configured for use.  

-   On a computer that is configured as a pull-distribution point and that runs a Configuration Manager client, the version of the client must be the same version as the Configuration Manager site that installs the pull-distribution point. This is a requirement for the pull-distribution point to use the CCMFramework that is common to both the pull-distribution point and the Configuration Manager client.  

## About source distribution points  
 When you configure the pull-distribution point, you must specify one or more source distribution points:  

-   Only distribution points that qualify to be source distribution points are displayed.  

-   A pull-distribution point can be specified as a source distribution point for another pull-distribution point.  

-   Only distribution points that support HTTP can be specified as source distribution points when you use Configuration Manager.  

-   You can use the Configuration Manager SDK to specify a source distribution point that is configured for HTTPS. To use a source distribution point that is configured for HTTPS, the pull-distribution point must be co-located on a computer that runs the Configuration Manager client.  

Each distribution point on a pull-distribution points source distribution point list can be assigned a priority:  

-   You can assign a separate priority to each source distribution point, or assign multiple source distribution points to the same priority.  

-   The priority determines in which order the pull-distribution point requests content from its source distribution points.  

-   Pull-distribution points initially contact a source distribution point with the lowest value for priority.  If there are multiple source distribution points with the same priority, the pull-distribution point nondeterministically selects one of the source distribution points that share that priority.  

-   When the content is not available on a selected source, the pull-distribution point then attempts to download the content from another distribution point with that same priority.  

-   If none of the distribution points with a given priority has the content, the pull-distribution point attempts to download the content from a distribution point that has an assigned priority with the next larger value, until the content is either located or the pull-distribution point sleeps for 30 minutes before it begins the process again.  

When a pull-distribution point downloads content from a source distribution point, that pull-distribution point is counted as a client in the **Client Accessed (Unique)** column of the **Distribution point usage summary** report.  

 By default, a pull-distribution point uses its **computer account** to transfer content from a source distribution point. However, when the pull-distribution point transfers content from a source distribution point that is in a remote forest, the pull-distribution point always uses the network access account. This process requires that the computer has the Configuration Manager client installed and that a network access account is configured for use and has access to the source distribution point.  

## About content transfers  
 To manage the transfer of content, pull-distribution points use the **CCMFramework** component of the Configuration Manager client software.  

-   This framework is installed by the **Pulldp.msi** when you configure the distribution point to be a pull-distribution point. The framework doesn't require the Configuration Manager client.  

-   After the pull-distribution point is installed, the CCMExec service on the distribution point computer must be operational for the pull-distribution point to function.  
<!--sms.503672 -Clarified BITS use-->
-   When the pull-distribution point transfers content, it transfers using the **Background Intelligent Transfer Service** (BITS) built into the Windows operating system. A pull-distribution point doesn't require the optional BITS IIS Server Extension feature to be installed.

-  The pull-distribution point logs its operation in the **datatransferservice.log** and the **pulldp.log** on the distribution point computer.

## See also  
 [Fundamental concepts for content management in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
