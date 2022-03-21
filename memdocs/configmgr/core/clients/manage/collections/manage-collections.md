---
title: Manage collections
titleSuffix: Configuration Manager
description: Do common collections management tasks in Configuration Manager.
ms.date: 02/17/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# How to manage collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the overview information in this article to help you run management tasks for collections in Configuration Manager.

For information about how to create Configuration Manager collections, see [How to create collections](create-collections.md).

## Collection actions

In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select **Device Collections** or **User Collections**, select the collection to manage, and then select a management task.

### Manage device collections

#### Show Members

Displays all of the resources that are members of the selected collection in a temporary node under the **Devices** node.

#### Add Selected Items

Provides the following options:

- **Add Selected Items to Existing Device Collection**: Opens the **Select Collection** window. Select the collection to which you want to add the members of the selected collection. The selected collection is included in this collection by using an **Include Collections** membership rule.

- **Add Selected Items to New Device Collection**: Opens the **Create Device Collection Wizard** where you can create a new collection. The selected collection is included in this collection by using an **Include Collections** membership rule.

For more information, see [How to create collections](create-collections.md).

#### Install Client

Opens the **Install Client Wizard**. This wizard uses client push installation to install a Configuration Manager client on all computers in the selected collection. For more information, see [Client push installation](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### Run Script

Opens the **Run Script** wizard to run a PowerShell script on all of the clients in the collection. For more information, see [Create and run PowerShell scripts](../../../../apps/deploy-use/create-deploy-scripts.md).

#### Start CMPivot

Opens CMPivot for this collection. Use CMPivot to query device information and take action in real time. For more information, see [CMPivot for real-time data](../../../servers/manage/cmpivot.md).

#### Manage Affinity requests

Opens the **Manage User Device Affinity Requests** dialog box. Approve or reject pending requests to establish user device affinities for devices in the selected collection. For more information, see [Link users and devices with user device affinity](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

#### Clear Required PXE deployments

Clears any required PXE boot deployments from all members of the selected collection. For more information, see [Use PXE to deploy Windows over the network](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

#### Update membership

Evaluates the membership for the selected collection. For collections with many members, this update might take some time to finish. Use the **Refresh** action to update the display with the new collections members after the update is completed.

#### Synchronize membership

If you configured this collection for cloud sync, synchronize the current membership with an Azure Active Directory group. For more information, see [Create collections](create-collections.md#bkmk_aadcollsync).

#### Add resources

Opens the **Add Resources to Collection** window. Search for new resources to add to the selected collection. The icon for the selected collection displays an hourglass symbol while the update is in progress.

#### Client notification

For more information, see [Client notifications](../client-notification.md).

#### Client diagnostics

Displays the following options:

- **Enable verbose logging**
- **Disable verbose logging**
- **Collect client logs**

For more information, see [Client diagnostics](../client-notification.md#client-diagnostics).

#### Endpoint Protection

For more information, see [Client notifications: Endpoint protection](../client-notification.md#endpoint-protection).

#### Export

Opens the **Export Collection Wizard** that helps you export this collection to a Managed Object Format (MOF) file. You can then archive this file, or import it to another Configuration Manager site. When you export a collection, referenced collections aren't exported. A referenced collection is referenced by the selected collection by using an **Include** or **Exclude** rule.

#### Copy

Creates a copy of the selected collection. The new collection uses the selected collection as a limiting collection.

#### Refresh

Refresh the view.

#### Delete

Deletes the selected collection. You can also delete all of the resources in the collection from the site database.

You can't delete the collections that are built into Configuration Manager. For a list of the built-in collections, see [Introduction to collections](introduction-to-collections.md#built-in-collections).

Collections might also not delete due to dependent collections. When reviewing a dependant collection you want to delete, also ensure that the dependant collection isn't: <!--9708999-->
- **Used by cloud attach**: For more information, see [Enable cloud attach for Configuration Manager](../../../../cloud-attach/enable.md).
- **Used for upload to Microsoft Endpoint Manager**: For more information, see [Make Configuration Manager collections available to assign Endpoint security policies](../../../../tenant-attach/endpoint-security-get-started.md#bkmk_collections).
- **Assigned to user**: For more information, see [Modify the administrative scope of an administrative user](../../../servers/deploy/configure/configure-role-based-administration.md#modify-the-administrative-scope-of-an-administrative-user).

#### Simulate deployment

Opens the **Simulate Application Deployment Wizard**. This wizard lets you test the results of an application deployment without installing or uninstalling the application. For more information, see [How to simulate application deployments](../../../../apps/deploy-use/simulate-application-deployments.md).

#### Deploy

Displays the following options:

- **Application**: Opens the **Deploy Software Wizard**. Select and configure an application deployment to the selected collection. For more information, see [How to deploy applications](../../../../apps/deploy-use/deploy-applications.md).

- **Program**: Opens the **Deploy Software Wizard**. Select and configure a package and program deployment to the selected collection. For more information, see [Packages and programs](../../../../apps/deploy-use/packages-and-programs.md).

- **Configuration Baseline**: Opens the **Deploy Configuration Baselines** window. Configure the deployment of one or more configuration baselines to the selected collection. For more information, see [How to deploy configuration baselines](../../../../compliance/deploy-use/deploy-configuration-baselines.md).

- **Task Sequence**: Opens the **Deploy Software Wizard**. Select and configure a task sequence deployment to the selected collection. For more information, see [Deploy a task sequence](../../../../osd/deploy-use/deploy-a-task-sequence.md).

- **Software Updates**: Opens the **Deploy Software Updates Wizard**. Configure the deployment of software updates to resources in the selected collection. For more information, see [Deploy software updates](../../../../sum/deploy-use/deploy-software-updates.md).

#### View relationships

For more information, see [View collection relationships](#view-collection-relationships).

#### Move

Move the selected collection to another folder in the **Device Collections** node.

#### Properties

For more information, see [Collection properties](#collection-properties).

### Manage user collections

The following actions are available on user collections. The behaviors are the same as with device collections, other than they apply to user collections and the users within. For more information, see the corresponding action under [Manage device collections](#manage-device-collections).

- Show Members
- Add Selected Items
  - Add Selected Items to Existing User Collection
  - Add Selected Items to New User Collection
- Manage Affinity Requests
- Update Membership
- Synchronize Membership
- Add Resources
- Export
- Copy
- Refresh
- Delete
- Simulate Deployment
- Deploy
  - Application
  - Program
  - Configuration Baseline
- View Relationships
- Move
- Properties

## Collection properties

When you view properties for a collection, you can view and configure the following options:

- **General**: View and configure general information about the selected collection including the collection name, the limiting collection, the collection ID, and last update times.

- **Membership Rules**: Configure the membership rules that define the membership of this collection. For more information, see [How to create collections](create-collections.md).

- **Power Management**: Configure power management plans that you've assigned to computers in the selected collection. For more information, see [Introduction to power management](../power/introduction-to-power-management.md).

- **Deployments**: Displays any software that you've deployed to members of the selected collection.

- **Maintenance Windows**: View and configure maintenance windows that are applied to members of the selected collection. For more information, see [How to use maintenance windows](use-maintenance-windows.md).

- **Collection Variables**: Configure variables that apply to this collection and can be used by task sequences. For more information, see [How to set task sequence variables](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).

- **Distribution Point Groups**: Associate one or more distribution point groups to members of the selected collection. For more information, see [Manage content and content infrastructure](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

- **Cloud Sync**: Synchronize collection membership results to Azure Active Directory groups. For more information, see [Create collections](create-collections.md#bkmk_aadcollsync).

    Starting in version 2006, you can also make this collection available to assign endpoint security policies when you tenant-attach the site. For more information, see [Tenant attach: Onboard Configuration Manager clients to Microsoft Defender for Endpoint from the admin center](../../../../tenant-attach/atp-onboard.md).

- **Security**: Displays the administrative users who have permissions for the selected collection from associated roles and security scopes. For more information, see [Fundamentals of role-based administration](../../../understand/fundamentals-of-role-based-administration.md).

- **Alerts**: Configure when alerts are generated for client status and endpoint protection. For more information, see [How to configure client status](../../deploy/configure-client-status.md) and [How to monitor endpoint protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).

## View collection relationships

<!--3608121-->

Starting in version 2010, you can view dependency relationships between collections in a graphical format. It shows limiting, include, and exclude relationships.

:::image type="content" source="media/3608121-view-dependent-relationships.png" alt-text="View collection dependency relationships in a graphical format" lightbox="media/3608121-view-dependent-relationships.png":::

If you want to change or delete collections, view the relationships to understand the effect of the proposed change. Before you create a deployment, look at the potential target collection for any include or exclude relationships that might affect the deployment.

When you select the **View Relationships** action on a device or user collection:

- To view the relationships with parent collections, select **Dependency**.

- To view the relationships with child collections, select **Dependent**.

For example, if you select the **All Systems** collection to view its relationships, the **Dependency** node will be **0** as it has no parent collections.

Use the following tips to navigate the relationship viewer:

- Select the plus (`+`) or minus (`-`) icons next to the collection name to expand or collapse members of a node.

- The number in parentheses after the collection name is the number of relationships. If the number is **0**, then that collection is the final or leaf node in that relationship tree.

- The style and color of the line between the collections determines the type of relationship:

    :::image type="content" source="media/3608121-collection-relationship-legend.png" alt-text="Collection dependency relationship line style legend":::

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

### Improvements in version 2103

<!--8543508-->

Starting in version 2103, you can view both dependency and dependent relationships together in a single graph. This change allows you to quickly see an overview of all the relationships of a collection at once and then drill down into specific related collections. It also includes other filtering and navigation improvements.

The following example shows the relationships for the "c1" collection in the center. It's dependent upon the collections above it (parents), and has dependencies below it (children).

:::image type="content" source="media/8543508-view-collection-relationships.png" alt-text="Example graph of collection relationships" lightbox="media/8543508-view-collection-relationships.png":::

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

## Automate with Windows PowerShell

You can use the following PowerShell cmdlets to manage collections:

### Generic cmdlets for all collection types

#### Basic cmdlets

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)
- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)
- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)
- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection)

#### Other actions

- [Copy-CMCollection](/powershell/module/configurationmanager/copy-cmcollection)
- [Export-CMCollection](/powershell/module/configurationmanager/export-cmcollection)
- [Get-CMCollectionMember](/powershell/module/configurationmanager/get-cmcollectionmember)
- [Get-CMCollectionSetting](/powershell/module/configurationmanager/get-cmcollectionsetting)
- [Import-CMCollection](/powershell/module/configurationmanager/import-cmcollection)
- [Invoke-CMCollectionUpdate](/powershell/module/configurationmanager/invoke-cmcollectionupdate)

#### Get membership rules

- [Get-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
- [Get-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
- [Get-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
- [Get-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)

#### Remove membership rules

- [Remove-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
- [Remove-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
- [Remove-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
- [Remove-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)

### Device collection-specific cmdlets

#### Basic actions for device collections

- [Get-CMDeviceCollection](/powershell/module/configurationmanager/get-cmdevicecollection)
- [New-CMDeviceCollection](/powershell/module/configurationmanager/new-cmdevicecollection)

#### Device collection variables

- [Get-CMDeviceCollectionVariable](/powershell/module/configurationmanager/get-cmdevicecollectionvariable)
- [New-CMDeviceCollectionVariable](/powershell/module/configurationmanager/new-cmdevicecollectionvariable)
- [Remove-CMDeviceCollectionVariable](/powershell/module/configurationmanager/remove-cmdevicecollectionvariable)
- [Set-CMDeviceCollectionVariable](/powershell/module/configurationmanager/set-cmdevicecollectionvariable)

#### Add device collection membership rules

- [Add-CMDeviceCollectionDirectMembershipRule](/powershell/module/configurationmanager/add-cmdevicecollectiondirectmembershiprule)
- [Add-CMDeviceCollectionExcludeMembershipRule](/powershell/module/configurationmanager/add-cmdevicecollectionexcludemembershiprule)
- [Add-CMDeviceCollectionIncludeMembershipRule](/powershell/module/configurationmanager/add-cmdevicecollectionincludemembershiprule)
- [Add-CMDeviceCollectionQueryMembershipRule](/powershell/module/configurationmanager/add-cmdevicecollectionquerymembershiprule)

#### Get device collection membership rules

- [Get-CMDeviceCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmdevicecollectiondirectmembershiprule)
- [Get-CMDeviceCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmdevicecollectionexcludemembershiprule)
- [Get-CMDeviceCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmdevicecollectionincludemembershiprule)
- [Get-CMDeviceCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmdevicecollectionquerymembershiprule)

#### Remove device collection membership rules

- [Remove-CMDeviceCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmdevicecollectiondirectmembershiprule)
- [Remove-CMDeviceCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmdevicecollectionexcludemembershiprule)
- [Remove-CMDeviceCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmdevicecollectionincludemembershiprule)
- [Remove-CMDeviceCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmdevicecollectionquerymembershiprule)

### User collection-specific cmdlets

- [Get-CMUserCollection](/powershell/module/configurationmanager/get-cmusercollection)
- [New-CMUserCollection](/powershell/module/configurationmanager/new-cmusercollection)

#### Add user collection membership rules

- [Add-CMUserCollectionDirectMembershipRule](/powershell/module/configurationmanager/add-cmusercollectiondirectmembershiprule)
- [Add-CMUserCollectionExcludeMembershipRule](/powershell/module/configurationmanager/add-cmusercollectionexcludemembershiprule)
- [Add-CMUserCollectionIncludeMembershipRule](/powershell/module/configurationmanager/add-cmusercollectionincludemembershiprule)
- [Add-CMUserCollectionQueryMembershipRule](/powershell/module/configurationmanager/add-cmusercollectionquerymembershiprule)

#### Get user collection membership rules

- [Get-CMUserCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmusercollectiondirectmembershiprule)
- [Get-CMUserCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmusercollectionexcludemembershiprule)
- [Get-CMUserCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmusercollectionincludemembershiprule)
- [Get-CMUserCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmusercollectionquerymembershiprule)

#### Remove user collection membership rules

- [Remove-CMUserCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmusercollectiondirectmembershiprule)
- [Remove-CMUserCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmusercollectionexcludemembershiprule)
- [Remove-CMUserCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmusercollectionincludemembershiprule)
- [Remove-CMUserCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmusercollectionquerymembershiprule)

## Next steps

[Client notifications](../client-notification.md)
