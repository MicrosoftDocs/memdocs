---
title: "Package Transfer Manager"
titleSuffix: "Configuration Manager"
description: "Understand how Package Transfer Manager in System Center Configuration Manager transfers content from a site server to remote distribution points."
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Package Transfer Manager in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In a System Center Configuration Manager site, the Package Transfer Manager is a  component of the SMS_Executive service that manages the transfer of content from a site server computer to remote distribution points in a site. (A remote distribution point is one that is not located on the site server computer.) The Package Transfer Manager does not support configurations by the admin, but understanding how it operates can help you plan your content management infrastructure. It can also help you resolve problems with content distribution.


When you distribute content to one or more remote distribution points at a site, the **Distribution Manager** creates a content transfer job. It then notifies the Package Transfer Manager on primary and secondary site servers to transfer the content to the remote distribution points.

 Package Transfer Manager logs its actions in the **pkgxfermgr.log** file on the site server. The log file is the only location where you can view the activities of the Package Transfer Manager.  

> [!NOTE]  
>  In previous versions of Configuration Manager, the Distribution Manager manages the transfer of content to a remote distribution point. Distribution Manager also manages the transfer of content between sites. With the System Center Configuration Manager, Distribution Manager continues to manage the transfer of content between two sites. However, the Package Transfer Manager now manages the transfer of content to large numbers of distribution points. This helps to increase the overall performance of content deployment both between sites and to distribution points within a site.  

To transfer content to a standard distribution point, Package Transfer Manager operates the same as the Distribution Manager operates in previous versions of Configuration Manager. That is, it actively manages the transfer of files to each remote distribution point. However, to distribute content to a pull-distribution point, the Package Transfer Manager notifies the pull-distribution point that content is available. The pull-distribution point then takes over the transfer process.  

The following information describes how Package Transfer Manager manages the transfer of content to standard distribution points, and to distribution points configured as pull-distribution points:
1.  **Admin deploys content to one or more distribution points at a site.**  

    -   **Standard distribution point:** Distribution Manager creates a content transfer job for that content.  

    -   **Pull-distribution point:** Distribution Manager creates a content transfer job for that content.  

2.  **Distribution Manager runs preliminary checks.**  

    -   **Standard distribution point:** Distribution Manager runs a basic check to confirm that each distribution point is ready to receive the content. After this check, Distribution Manager notifies Package Transfer Manager to start the transfer of content to the distribution point.  

    -   **Pull-distribution point:** Distribution Manager starts Package Transfer Manager, which then notifies the pull-distribution point that there is a new content transfer job. Distribution Manager does not check on the status of remote distribution points that are pull-distribution points, because each pull-distribution point manages its own content transfers.  

3.  **Package Transfer Manager prepares to transfer content.**  

    -   **Standard distribution point:** Package Transfer Manager examines the single instance content store of each specified remote distribution point. The purpose of this is to identify any files that are already on that distribution point. Then, Package Transfer Manager queues up for transfer only those files that are not already present.  

        > [!NOTE]  
        >  To copy each file in the distribution to the distribution point, even if the files are already present in the single instance store of the distribution point, use the **Redistribute** action for content.  

    -   **Pull-distribution point:** For each pull-distribution point in the distribution, Package Transfer Manager checks the pull-distribution points source distribution points, to confirm if the content is available.  

        -   When the content is available on at least one source distribution point, Package Transfer Manager sends a notification to that pull-distribution point. The notification directs that distribution point to begin the process of transferring content. The notification includes file names and sizes, attributes, and hash values.  

        -   When the content is not yet available, Package Transfer Manager does not send a notification to the distribution point. Instead, it repeats the check every 20 minutes until the content is available. Then, when the content is available, Package Transfer Manager sends the notification to that pull-distribution point.  

        > [!NOTE]  
        >  For the pull-distribution point to copy each file in the distribution to the distribution point, even if the files are already present in the single instance store of the pull-distribution point, use the **Redistribute** action for content.  

4.  **Content begins to transfer.**  

    -   **Standard distribution point:** Package Transfer Manager copies files to each remote distribution point. During the transfer to a standard distribution point:  

        -   By default, Package Transfer Manager can simultaneously process three unique packages, and distribute them to five distribution points in parallel. Collectively, these are called **Concurrent distribution settings**. To set up concurrent distribution, in the **Software Distribution Component Properties** for each site, go to the **General** tab.  

        -   Package Transfer Manager uses the scheduling and network bandwidth configurations of each distribution point when transferring content to that distribution point. To configure these settings, in the **Properties** of each remote distribution point, go to the **Schedule** and **Rate Limits** tabs. For more information, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Pull-distribution point:** When a pull-distribution point receives a notification file, the distribution point begins the process to transfer the content. The transfer process runs independently on each pull-distribution point:  

        1.   The pull-distribution identifies the files in the content distribution that it does not already have in its single instance store, and prepares to download that content from one of its source distribution points.  

        2.   Next, the pull-distribution point checks with each of its source distribution points, in order, until it locates a source distribution point that has the content available. When the pull-distribution point identifies a source distribution point with the content, it begins the download of that content.  

        > [!NOTE]  
        >  The process to download content by the pull-distribution point is the same as that used by Configuration Manager clients. For the transfer of content by the pull-distribution point, concurrent transfer settings aren't used. Scheduling and throttling options that you configure for standard distribution points aren't used either.  

5.  **Content transfer completes.**  

    -   **Standard distribution point:** After the Package Transfer Manager is done transferring files to each designated remote distribution point, it verifies the hash of the content on the distribution point. Then it notifies Distribution Manager that the distribution is complete.  

    -   **Pull-distribution point:** After the pull-distribution point completes the content download, the distribution point verifies the hash of the content. Then it submits a status message to the site management point to indicate success. If, after 60 minutes, this status is not received, the Package Transfer Manager wakes up again. It checks with the pull-distribution point to confirm whether the pull-distribution point has downloaded the content. If the content download is in progress, the Package Transfer Manager sleeps for another 60 minutes before it checks with the pull-distribution point again. This cycle continues until the pull-distribution point completes the content transfer.  
