---
title: Collections best practices
titleSuffix: Configuration Manager
description: Get best practices for collections in Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Best practices for collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the following best practices for collections in Configuration Manager.  

## Configure maintenance window for updates

You can configure maintenance windows for device collections to restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client might not be able to install critical software updates, which leaves the client vulnerable to the attack mitigated by the software update.

Important considerations to keep in mind when planning your maintenance windows:

- The default software update maximum run time is 60 minutes.
- When Configuration Manager calculates whether an update can install, it adds five minutes to the maximum run time to account for a restart.
- The remaining duration of a maintenance window must be longer than the maximum run time of the software update plus five minutes.

## Avoid frequent collection evaluation

A full collection evaluation evaluates not only the targeted collection, but also any collections that the collection limits if an update occurs. Also, a collection with no schedule will still be evaluated if its limiting collection is updated. So it's possible that some collections may be evaluated more often than expected.

In a busy Configuration Manager environment, you can improve collection evaluation performance by scaling back schedules to avoid repeated collection evaluations. In a deep tree, you can decrease collection evaluation frequency as the collections descend deeper in the tree, because higher-level collection evaluations will also trigger lower-level collections to evaluate.

## Understand the collection evaluation graph

If a collection is configured for incremental evaluation and updates on a schedule, referencing collections that aren't enabled for incremental evaluation may not update as expected. Because updates likely occurred during incremental evaluation cycles, a full evaluation may not result in an update to the collection, and will therefore signal the end of the collection evaluation graph for that evaluation cycle. In that case, no referencing collection evaluations will be triggered. Consequently, don't rely on the collection evaluation graph to perform updates to referencing collections, but be aware of how the graph works so you can design an appropriate collection structure.

## <a name="bkmk_incremental"></a> Limit incremental collections

When table data changes, a SQL trigger inserts a row in the **CollectionNotifications** table. The next time the collection evaluation schedule fires, it `AND`s the resource ID with the existing collection query and triggers updates on incremental collections.

Incremental collection executes one query per machine. The default site configuration for incremental collection evaluation is every five minutes. 

The **Use incremental updates for this collection** option might cause evaluation delays when you enable it for many collections. Best practices recommend a limit of 200 incremental collections. The exact number depends on the following factors:  

- The total number of collections
- The frequency of new resources being added and changed in the hierarchy
- The number of clients in a hierarchy
- The complexity of collection membership rules in a hierarchy

If the incremental evaluation cycle is taking longer than the configured frequency of updates, then Configuration Manager is constantly processing collection evaluations, which could impact the performance of the rest of the system. Reduce the number of collections configured for incremental evaluation, or increase the time between incremental evaluation cycles.

Given the potential impacts of incremental collections, it's important to have a policy or procedure for creating collections and assigning collection update schedules. Examples of policy considerations might be:

- Only use incremental updates for collections that are used for security scoping, client settings, and maintenance windows, because they affect client behavior and access to resources.
- For applications with no licensing approval, advertise applications to existing collections, and use global conditions to restrict availability.
- Outline appropriate periods for other collections that have full collection updates scheduled.

## Avoid evaluation of large trees from the CAS

In a Configuration Manager environment, the Central Administration Site (CAS) doesn't evaluate collection membership. Primary sites are the only sites that evaluate collections. Secondary sites act as proxies, using only data replicated from their associated primary sites.

To request a collection update, the CAS sends a request to each primary site. The primary sites evaluate the collection and send the results back to the CAS. The collection evaluation results appear only after all the collection evaluation instructions have been replicated to all of the sites, all the sites have evaluated the collection, and all the data has been returned to the CAS and consolidated.

The following diagram demonstrates the flow when the CAS requests a manual collection update:

![Manual collection update from a CAS](media/manual-collection-update-from-cas.png)

A collection update from a CAS with multiple primary sites can be time consuming, and if a collection doesn't evaluate in a timely fashion, it can be tempting to repeat the request.

Once a collection evaluation thread is started and the evaluation graph is loaded, evaluation continues until the collection evaluation graph is emptied. The thread then terminates and becomes available for the next evaluation. However, if another collection evaluation cycle is queued while the thread is occupied evaluating collections, the thread is immediately restarted to attempt an evaluation of the "missed" evaluation cycle.

Each evaluation method runs in its own thread. It's possible that within the thread, Configuration Manager may attempt to graph the same collection more than once. Configuration Manager then drops the second and subsequent requests.

To prevent these scenarios, avoid manual collection evaluations of large trees, especially when working from the CAS with multiple sites involved.

## Understand collection depth and cross-referencing

To strike a balance between business requirements and performance, it's important to understand the collection structure you're creating and the dependencies it has on other collections. If you create a collection with rules that reference one or more collections that also refer to other collections, all of those collections will be evaluated to create the membership of this collection.

The include and exclude collection rules in Configuration Manager make referencing collections easier than writing a custom WQL query. But if using include and exclude collections results in a high performance toll, you can use the WQL query method instead:

Include:

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Exclude:

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## Use CEViewer to monitor collection evaluation

You can use the [Collection Evaluation Viewer (CEViewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) to monitor how many collections are being evaluated and how long each collection is taking to update. The CEViewer is in the *CD.Latest* folder on the site server.

To manually perform a similar check with SQL, you can use the following query:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


