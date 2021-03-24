---
title: How to view collection evaluation
titleSuffix: Configuration Manager
description: View collection evaluation queues and evaluation related information.
ms.date: 03/26/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 8e07d4f1-f032-4846-baf1-d0e50cef7ffd
author: mestew
ms.author: mstewart
manager: dougeby 
---

# <a name="bkmk_colleval"></a> How to view collection evaluation

*Applies to: Configuration Manager (current branch)*
<!--6251274-->
Starting in Configuration Manager version 2010, the functionality of [Collection Evaluation Viewer](../../../support/ceviewer.md) is integrated into the Configuration Manager console. On each **primary site**, this functionality provides administrators a central location to view and troubleshoot the [collection evaluation](./collection-evaluation.md) process. The console displays the following information:

- Historic and live information for full and incremental collection evaluations
- The evaluation queue status
- The time for collection evaluations to complete
- Which collections are currently being evaluated
- The estimated time that a collection evaluation will start and complete

> [!Tip]
> Viewing collection evaluation at the CAS changed in Configuration Manager version 2103. For more information, see the [Collection evaluation information at the CAS](#bkmk_cas) section.
>
> The collection evaluation process is performed on primary sites, not on the central administration site (CAS). When using the console connected to a CAS using Configuration Manager 2010, you'll see the following behavior:
> - Evaluation related columns for device collections won't contain data.
> - The **Collection Evaluation** node under the **Monitoring** workspace isn't shown.
> - Evaluation related information, such as evaluation status and links to the collection evaluation queues, won't be shown in the collection **Summary** group pane.


## Collection evaluation queues

The collection evaluation process evaluates the membership rules of a collection to update its members. A primary site places a collection that it's evaluating into one of four different queues:

- **Full Evaluation Queue**: For collections due for full evaluation
- **Incremental Evaluation Queue**: For collections with incremental evaluation
- **Manual Evaluation Queue**: For collections that an administrator has manually selected for evaluation from the console
- **New Evaluation Queue**: For newly created collections

## Add columns for the Device Collections node

Adding columns to the **Device Collections** node allows you to view collection evaluation information for multiple collections.

1. Connect the Configuration Manager console to a primary site.
1. Go to **Assets and Compliance** > **Overview** > **Device Collections**.
1. Add any or all of the following columns prefixed by the type of evaluation:
   - **Evaluation (Full)**
      - **Last Completion Time**: When the last collection evaluation completed  (default column)
      - **Run Time**: How long the last collection evaluation ran, in seconds
      - **Next Refresh Time**: When the next full evaluation starts
      - **Member Changes**: The member changes in the last collection evaluation. Positive numbers mean members were added while negative numbers mean members were removed.
      - **Last Member Change Time**: The most recent time that there was a membership change in the collection evaluation
   - **Evaluation (Incremental)**
      - **Last Evaluation Completion Time**: When the last collection evaluation completed
      - **Run Time**: How long the last collection evaluation ran, in seconds
      - **Member Changes**: The member changes in the last collection evaluation. These changes are either plus (members added) or minus (members removed).
      - **Last Member Change Time**: The most recent time that there was a membership change in the collection evaluation

:::image type="content" source="./media/6251274-add-collection-evaluation-columns.png" alt-text="Evaluation-related information columns for the collections node" lightbox="./media/6251274-add-collection-evaluation-columns.png":::


## View evaluation information from the collection summary

View the collection summary information to get information specific to the evaluation of a single collection.

1. Connect the Configuration Manager console to a primary site.
1. Go to **Assets and Compliance** > **Overview** > **Device Collections**.
1. Select a collection from the **Device Collections** node.
1. In the **Summary** group pane for collection, review the evaluation-related information for the selected collection.
   :::image type="content" source="./media/6251274-summary-collection-evaluation.png" alt-text="Evaluation-related information in the summary group for the selected collection" lightbox="./media/6251274-summary-collection-evaluation.png":::
1. The **Related Objects** give links to view status of the collection in the specific queue. These links take you to the queues in the **Monitoring** workspace under the **Collection Evaluation** node.
   - This action creates a new node is created where you can see the evaluation status for the specific collection.  

## Monitoring collection evaluation queues

Monitoring the collection evaluation queues can give you deeper insight into the collection evaluation process.

1. Connect the Configuration Manager console to a primary site.
1. From the **Monitoring** workspace, go to the **Collection Evaluation** node. The following queues are summarized and have their own nodes:
   - **Full Evaluation Queue**: For collections due for full evaluation
   - **Incremental Evaluation Queue**: For collections with incremental evaluation
   - **Manual Evaluation Queue**: For collections that an administrator has manually selected for evaluation from the console
   - **New Evaluation Queue**: For newly created collections
1. From the **Collection Evaluation** node, the total number of collections in queue and queue length is listed as a summary. Additionally, the following status summaries for the evaluation queues are listed:
   - Number of collections in queue
   - Queue length
   - Current evaluation collection
   - Current evaluation started on
   - Current evaluation elapsed (seconds)
1. Selecting the node for a queue brings up detailed status for the queue including: 
   - **Name**: Name of the collection
   - **Collection ID**:  ID of the collection
   - **Estimated Completion Time**: When the evaluation is estimated to complete
   - **Estimated Run Time**: How long the evaluation is estimated to run, in day:hour:minute:second format

:::image type="content" source="./media/6251274-manual-evaluation-queue.png" alt-text="Manual Evaluation Queue node containing detailed information about collection evaluation" lightbox="./media/6251274-manual-evaluation-queue.png":::

## <a name="bkmk_cas"></a> Collection evaluation information at the CAS
<!--8787410-->
*(Introduced in 2103)*

Since collection evaluation happens at the primary site level, the collection evaluation view on the CAS is a summary of what's occurring on the primary sites. Starting in Configuration Manager version 2103, there are two new tabs in the details pane of the collection view in the console. The following new tabs show collection evaluation information from all primary sites in hierarchy:

- **Evaluation (Full) In Hierarchy**
- **Evaluation (Incremental) In Hierarchy**

:::image type="content" source="./media/8787410-collection-evaluation-details-tab.png" alt-text="Collection evaluation tabs in the collection's details pane at the CAS" lightbox="./media/8787410-collection-evaluation-details-tab.png":::

From the **Device Collections** node at the CAS, the evaluation columns display the evaluation status from the primary site with the longest run time. The column information at the CAS for the full evaluation status could be from a different primary site than the incremental information since the longest runtime for the incremental might have occurred at a different primary.

 For instance, incremental evaluation for the `All Systems` collection on the  `WMI` primary site takes longer than the other primary sites. The full evaluation columns on the CAS display the information from primary site `WMI` for the `All Systems` collection in the **Device Collections** node.

:::image type="content" source="./media/8787410-cas-collection-evaluation-columns.png" alt-text="Collection evaluation columns at the CAS with the details tab open displaying the evaluation from all primary sites" lightbox="./media/8787410-cas-collection-evaluation-columns.png":::

## Next steps

Learn more about [Collection evaluation in Configuration Manager](collection-evaluation.md).
