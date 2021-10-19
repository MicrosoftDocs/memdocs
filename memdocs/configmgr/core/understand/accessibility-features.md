---
title: Accessibility
titleSuffix: Configuration Manager
description: Learn about the features that make Configuration Manager accessible for everyone.
ms.date: 07/21/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Accessibility features in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager includes features to help make it accessible for everyone.

> [!NOTE]
> To improve the accessibility features of the Configuration Manager console, update .NET to version 4.7 or later on the computer running the console. <!-- SCCMDocs-pr issue #3228 -->
>
> For more information on the accessibility changes made in .NET 4.7.1 and 4.7.2, see [What's new in accessibility in the .NET Framework](/dotnet/framework/whats-new/whats-new-in-accessibility).

## Keyboard shortcuts

### Console workspaces

To access a workspace, use the following keyboard shortcuts:

|Keyboard shortcut| Workspace|
|--------|--------|
|`Ctrl` + `1`| Assets and Compliance|
|`Ctrl` + `2`|  Software Library|
|`Ctrl` + `3`|  Monitoring|
|`Ctrl` + `4`|  Administration|

### Other console shortcuts

|Keyboard shortcut|  Purpose|
|--------|--------|
|`Ctrl` + `M`|Set the focus on the main (central) pane.|
|`Ctrl` + `T`|Set the focus to the top node in the navigation pane. If the focus was already in that pane, the focus is set to the last node you visited.|
|`Ctrl` + `I`|Set the focus to the breadcrumb bar, below the ribbon.|
|`Ctrl` + `L`|Set the focus to the **Search** field, when available.|
|`Ctrl` + `D`|Set the focus to the details pane, when available.|
|`Alt`       |Change the focus in and out of the ribbon.|

### <a name="bkmk_cmpshortcuts"></a> CMPivot shortcuts

Most [web browser keyboard shortcuts](https://support.microsoft.com/topic/internet-explorer-ease-of-access-options-037270c1-db10-7ca8-ccba-ebd83ea6ace9) will work in [CMPivot](../servers/manage/cmpivot-overview.md).

|Keyboard shortcut|Purpose|
|--------|--------|
|`Ctrl` + `1`|Set the focus on the first tab.|
|`Alt` + `<`|To back to the address|

### Collection relationship diagram shortcuts

<!--8543508-->
When you [view collection relationships](../clients/manage/collections/manage-collections.md#view-collection-relationships) in the Configuration Manager console, use the **TAB** key to change the focus. By default, the focus is on the page number controls. When the focus is on the graph itself (navigator), use the following keyboard shortcuts to navigate:

|Navigator shortcut|Purpose|
|--------|--------|
|`Ctrl` + `W`|Scroll up|
|`Ctrl` + `S`|Scroll down|
|`Ctrl` + `A`|Scroll left|
|`Ctrl` + `D`|Scroll right|
|`Ctrl` + `+`|Zoom in|
|`Ctrl` + `-`|Zoom out|

Use the following keyboard shortcuts to quickly move focus to different areas of the window:

|Keyboard shortcut|Purpose|
|--------|--------|
|`Alt` + `P` | Dependent page |
|`Alt` + `B` | Back |
|`Alt` + `H` | Home |
|`Alt` + `N` | Collection name |
|`Alt` + `T` | Filter |

## Other accessibility features

- To navigate the navigation pane, type the letters of a node name.

- Keyboard navigation through the main view and the ribbon is circular.

- Keyboard navigation in the details pane is circular. To return to the previous object or pane, use `Ctrl` + D, then Shift + TAB.

- After refreshing a Workspace view, the focus is set to the main pane of that workspace.

- To access a workspace menu, select the Tab key until the Expand/Collapse icon is in focus. Then, select the Down arrow key to access the workspace menu.

- To navigate through a workspace menu, use the arrow keys.

- To access different areas in the workspace, use the Tab key and Shift+Tab keys. To navigate within an area of the workspace, such as the ribbon, use the arrow keys.

- To access the address bar when your focus is in the tree node, use Shift+Tab three times.

- On a wizard or property page, you can move between the boxes with keyboard shortcuts. Select the Alt key plus the underlined character (Alt+_) to select a specific box.

- To navigate to the different nodes of a workspace, enter the first letter of the name of a node. Each key press moves the cursor to the next node that begins with that letter. When you're using a screen reader, the reader reads out the name of that node.

## Next steps

For more information on the fundamentals of navigating Configuration Manager user interfaces, see the following articles:

- [Using the Configuration Manager console](../servers/manage/admin-console.md)
- [Software Center user guide](software-center.md)

> [!NOTE]
> The information in this article might apply only to users who license Microsoft products in the United States. If you obtained this product outside of the United States, you can use the subsidiary information card that came with your software package or visit the [Microsoft Accessibility website](https://www.microsoft.com/accessibility/) for contact information for Microsoft support services. You can contact your subsidiary to find out whether the type of products and services that are described in this section are available in your area. Information about accessibility is available in other languages, including Japanese and French.
