---
title: Example of using boundary groups
titleSuffix: Configuration Manager
description: Use this boundary group example to help understand how clients locate and download content from a distribution point.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Example of using boundary groups

*Applies to: Configuration Manager (current branch)*

The following example uses a client searching for content from a distribution point. This example can be applied to other site system roles that use boundary groups.

Create three boundary groups that don't share boundaries or site system servers:

- Group BG_A with distribution points DP_A1 and DP_A2

- Group BG_B with distribution points DP_B1 and DP_B2

- Group BG_C with distribution points DP_C1 and DP_C2

Add the network locations of your clients as boundaries to only the BG_A boundary group. Then configure relationships from that boundary group to the other two boundary groups:

- Configure distribution points for the first *neighbor* group (BG_B) to be used after 10 minutes. This group contains distribution points DP_B1 and DP_B2. Both are well connected to the first group's boundary locations.

- Configure the second *neighbor* group (BG_C) to be used after 20 minutes. This group contains distribution points DP_C1 and DP_C2. Both are across a WAN from the other two boundary groups.

- Also add to the default site boundary group another distribution point that's on the site server. This server is your least preferred content source location, but it's centrally located to all your boundary groups.

    Example of boundary groups and fallback times:

    :::image type="content" source="media/boundary-group-fallback.png" alt-text="Conceptual diagram of example boundary groups and fallback times." lightbox="media/boundary-group-fallback.png":::

With this configuration:

- The client begins searching for content from distribution points in its *current* boundary group (BG_A). It searches each distribution point for two minutes, and then switches to the next distribution point in the boundary group. The client's pool of valid content source locations includes DP_A1 and DP_A2.

- If the client fails to find content from its *current* boundary group after searching for 10 minutes, it then adds the distribution points from the BG_B boundary group to its search. It then continues to search for content from a distribution point in its combined pool of servers. This pool now includes servers from both the BG_A and BG_B boundary groups. The client continues to contact each distribution point for two minutes, and then switches to the next server in its pool. The client's pool of valid content source locations includes DP_A1, DP_A2, DP_B1, and DP_B2.

- After another 10 minutes (20 minutes total), if the client still hasn't found a distribution point with content, it expands its pool to include available servers from the second *neighbor* group, boundary group BG_C. The client now has six distribution points to search: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1, and DP_C2. It continues changing to a new distribution point every two minutes until it finds content.

- If the client hasn't found content after a total of 120 minutes, it falls back to include the *default site boundary group* as part of its continued search. Now the pool includes all distribution points from the three configured boundary groups, and the final distribution point located on the site server. The client then continues its search for content, changing distribution points every two minutes until content is found.

By configuring the different neighbor groups to be available at different times, you control when specific distribution points are added as a content source location. The client uses fallback to the default site boundary group as a safety net for content that isn't available from any other location.

## Next steps

[Procedures for boundary groups](boundary-group-procedures.md)
