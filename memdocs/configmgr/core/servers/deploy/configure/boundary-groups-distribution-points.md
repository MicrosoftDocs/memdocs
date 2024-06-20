---
title: Boundary groups and distribution points
titleSuffix: Configuration Manager
description: Understand how clients and distribution points behave with boundary groups.
ms.date: 08/02/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Boundary groups and distribution points

*Applies to: Configuration Manager (current branch)*

When a client requests the location of a distribution point, Configuration Manager sends the client a list of site systems. These site systems are of the appropriate type associated with each boundary group that includes the client's current network location.

- During software distribution, clients request a location for deployment content on a valid content source. This location may be a distribution point, or a peer cache source.

- During OS deployment, clients request a location to send or receive their state migration information.

  - Clients get content based on boundary group behaviors. For more information, see [Task sequence support for boundary groups](#task-sequence-support).

During content deployment, if a client requests content that isn't available from a source in its current boundary group, the client continues to request that content. The client tries different content sources in its current boundary group until it reaches the fallback period for a neighbor or the default site boundary group. If the client still hasn't found content, it then expands its search for content sources to include the neighbor boundary groups.

If you configure the content to distribute on-demand, and it isn't available on a distribution point when a client requests it, the site begins to transfer the content to that distribution point. It's possible the client finds that server as a content source before falling back to use a neighbor boundary group.

## Client installation

The Configuration Manager client installer, ccmsetup, can get installation content from a local source or via a management point. Its initial behavior depends upon the command-line parameters you use to install the client:<!-- MEMDocs#286 -->

- If you don't use either `/mp` or `/source` parameters, ccmsetup tries to get a list of management points from Active Directory or DNS.

- If you only specify `/source`, it forces the installation from the specified path. It doesn't discover management points. If it can't find ccmsetup.cab at the specified path, ccmsetup fails.

- If you specify both `/mp` and `/source`, it checks the specified management points, and any it discovers. If it can't locate a valid management point, it falls back to the specified source path.

For more information on these ccmsetup parameters, see [Client installation parameters and properties](../../../clients/deploy/about-client-installation-properties.md).

<!--1358840-->
When ccmsetup contacts the management point to locate the necessary content, the management point returns distribution points based on boundary group configuration. If you define relationships on the boundary group, the management point returns distribution points in the following order:

1. Current boundary group

2. Neighbor boundary groups

3. The site default boundary group

> [!NOTE]
> The client setup process doesn't use the fallback time. To locate content as quickly as possible, it immediately falls back to the next boundary group.
>
> In previous versions of Configuration Manager, during this process the management point only returned distribution points in the client's current boundary group. If no content was available, the setup process fell back to download content from the management point. There was no option to fall back to distribution points in other boundary groups that might have the necessary content.

## Task sequence support

<!--1359025-->
When a device runs a task sequence and needs to acquire content, it uses boundary group behaviors similar to the Configuration Manager client.

Configure this behavior using the following settings on the **Distribution Points** page of the task sequence deployment:

- **When no local distribution point is available, use a remote distribution point**: For this deployment, the task sequence can fall back to distribution points in a neighbor boundary group.

- **Allow clients to use distribution points from the default site boundary group**: For this deployment, the task sequence can fall back to distribution points in the default site boundary group.

To use this new behavior, make sure to update clients to the latest version.

### Location priority

The task sequence tries to acquire content in the following order:

1. Peer cache sources

2. Distribution points in the *current* boundary group

3. Distribution points in a *neighbor* boundary group

    > [!IMPORTANT]
    > Due to the real-time nature of task sequence processing, it doesn't wait for the failover time on a neighbor boundary group. It uses the failover times for prioritizing the neighbor boundary groups. For example, if the task sequence fails to acquire content from a distribution point in its current boundary group, it immediately tries a distribution point in a neighbor boundary group with the shortest failover time. If that process fails, it then fails over to a distribution point in a neighbor boundary group with a larger failover time.
    >
    > For content like applications and software updates, which are downloaded by the client and not the task sequence engine, the client behaves as normal. In other words, if you install applications or software updates from a task sequence, when the client tries to download the content it will wait for boundary group failover.<!-- 7594647 -->

4. Distribution points in the *site default* boundary group

The task sequence log file **smsts.log** shows the priority of the location sources that it uses based on the deployment properties.

## Next steps

- [Boundary groups and software update points](boundary-groups-software-update-points.md)

- [Procedures for boundary groups](boundary-group-procedures.md)
