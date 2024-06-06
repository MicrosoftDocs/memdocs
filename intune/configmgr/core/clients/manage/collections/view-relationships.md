---
title: View collection relationships
titleSuffix: Configuration Manager
description: You can view dependency relationships between collections in a graphical format. It shows limiting, include, and exclude relationships.
ms.date: 04/08/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
ms.localizationpriority: medium
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# View collection relationships

*Applies to: Configuration Manager (current branch)*

<!--3608121-->

You can view dependency relationships between collections in a graphical format. It shows limiting, include, and exclude relationships.

:::image type="content" source="media/3608121-view-dependent-relationships.png" alt-text="View collection dependency relationships in a graphical format." lightbox="media/3608121-view-dependent-relationships.png":::

If you want to change or delete collections, view the relationships to understand the effect of the proposed change. Before you create a deployment, look at the potential target collection for any include or exclude relationships that might affect the deployment.

When you select the **View Relationships** action on a device or user collection:

- To view the relationships with parent collections, select **Dependency**.

- To view the relationships with child collections, select **Dependent**.

For example, if you select the **All Systems** collection to view its relationships, the **Dependency** node will be **0** as it has no parent collections.

Use the following tips to navigate the relationship viewer:

- Select the plus (`+`) or minus (`-`) icons next to the collection name to expand or collapse members of a node.

- The number in parentheses after the collection name is the number of relationships. If the number is **0**, then that collection is the final or leaf node in that relationship tree.

- The style and color of the line between the collections determines the type of relationship:

    :::image type="content" source="media/3608121-collection-relationship-legend.png" alt-text="Collection dependency relationship line style legend.":::

    If you hover over a specific line, a tooltip shows the relationship type.

- The maximum number of child nodes displayed depends upon the level of the graph:
  - First level: five nodes
  - Second level: three nodes
  - Third level: two nodes
  - Fourth level: one node

  If there are more objects than the graph can display at that level, you'll see the **More** icon.

- When the width of the tree is larger than the window, use the green arrows to the right or the left to view more.

- When a node of the relationship tree is larger than the available space, select **More** to change the view to just that node.

- To navigate to a prior view, select the **Back** arrow in the upper right corner. Select the **Home** icon to return to the main page.

- Use the **Search** box in the upper right corner to locate a collection in the current tree view.

- Use the **Navigator** in the lower right corner to zoom and pan around the tree. You can also print the current view.

- You can only see relationships between collections to which you have permission:

  - If you have permission for **All Systems** or **All Users and User Groups**, then you'll see all relationships.

  - If you don't have permission for a specific collection, you don't see it in the graph, and can't view its relationships.

## Improvements in version 2103

<!--8543508-->

Starting in version 2103, you can view both dependency and dependent relationships together in a single graph. This change allows you to quickly see an overview of all the relationships of a collection at once and then drill down into specific related collections. It also includes other filtering and navigation improvements.

The following example shows the relationships for the "c1" collection in the center. It's dependent upon the collections above it (parents), and has dependencies below it (children).

:::image type="content" source="media/8543508-view-collection-relationships.png" alt-text="Example graph of collection relationships." lightbox="media/8543508-view-collection-relationships.png":::

To see the relationships of another collection in the graph, select it to open a new window targeted on that collection.

Other improvements:

- There's a new **Filter** button in the upper right corner. This action lets you reduce the graph to specific relationship types: **Limiting**, **Include**, or **Exclude**.

- If you don't have permissions to all related collections, the graph includes a warning message that the graph may be incomplete.

- When the graph is wider than the window can display, use the page navigation controls in the upper left corner. The first number is the page for parents (above), and the second number is the page for children (below). The window title also shows the page numbers.

- The tooltip for a collection displays the count of dependencies it has and the count of dependant collections where applicable. This count only includes unique subcollections. The count no longer displays in the parentheses next to the collection name.

- Previously the **Back** button took you through your viewing history. Now it takes you to the previously selected collection. For example, changing pages for the current collection doesn't activate the **Back** button. When you select a new collection, you can select **Back** to return to the original collection graph.

> [!TIP]
> Hold the **Ctrl** key and scroll the mouse wheel to zoom the graph.

For more information on how to navigate the collection dependency graph with a keyboard, see [Accessibility features](../../../understand/accessibility-features.md#collection-relationship-diagram-shortcuts).

## Next steps

[How to view collection evaluation](collection-evaluation-view.md)
