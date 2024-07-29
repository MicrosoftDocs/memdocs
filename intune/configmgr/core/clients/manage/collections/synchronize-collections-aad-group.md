---
title: Synchronize collection members to Microsoft Entra groups
titleSuffix: Configuration Manager
description: Synchronize collection members to Microsoft Entra groups.
ms.date: 03/28/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to synchronize collection members to Microsoft Entra groups

<!--3607475-->

You can enable the synchronization of collection memberships to a Microsoft Entra group. This synchronization allows you to use your existing on premises grouping rules in the cloud by creating Microsoft Entra group memberships based on collection membership results. You can synchronize device or user collections. Only resources with a Microsoft Entra ID record are reflected in the Microsoft Entra group. Both Microsoft Entra hybrid joined and Microsoft Entra joined devices are supported. The synchronization of collection memberships is a one-way process from Configuration Manager to Microsoft Entra ID. Ideally, Configuration Manager should be the authority for managing the membership for the target Microsoft Entra groups.

Synchronizations can either be full or incremental and they have slightly different behaviors: <!--9718854-->

- Full synchronization: Occurs on the first synchronization after enabling it. You can force a full synchronization by selecting the collection, and then choosing **Synchronize Membership** from the ribbon. A full synchronization will overwrite members of the Microsoft Entra group.

- Incremental synchronization: Occurs every 5 minutes. Changes made in Microsoft Entra ID aren't reflected in Configuration Manager collections, but they aren't overwritten by Configuration Manager. <!--For example, if the Configuration Manager collection has two devices, and the Azure AD group has three different devices, after an incremental synchronization, the Azure AD group has five devices.-->

Example synchronization scenario:
1. From Microsoft Entra ID, create a group called `Group1` and add `DeviceA`, `DeviceB`, and `DeviceC`.
   - Ideally, objects wouldn't be added from Microsoft Entra ID since Configuration Manager should manage the group membership. 
1. From Configuration Manager, create a collection called `Collection1` then add `DeviceB`, and `DeviceC`.
1. [Enable synchronization](#enable-the-collection-to-synchronize) for `Collection1` to `Group1`.
1. The first synchronization is a full synchronization so, `Group1` now contains `DeviceB`, and `DeviceC`. `DeviceA` was removed from the group during the full synchronization.
1. Remove `DeviceC` from `Collection1` and wait for an incremental synchronization.
1. `Group1` now contains only `DeviceB`.
1. From Microsoft Entra ID, add `DeviceD` to `Group1` and wait for an incremental synchronization.
1. `Group1` now contains `DeviceB` and `DeviceD`.
1. From Configuration Manager, select `Collection1`, and choose **Synchronize Membership** from the ribbon to force a full synchronization.
1. `Group1` now contains only `DeviceB`

<a name='prerequisites-for-azure-ad-synchronization'></a>

## Prerequisites for Microsoft Entra synchronization

- Integration with Microsoft Entra ID for [cloud management](../../../servers/deploy/configure/azure-services-wizard.md).Option to ** Disable Microsoft Entra authentication for this tenant** under Azure Service for Cloud Management in the console must not be checked as this prevents client registration using Entra ID Authentication.

- [Microsoft Entra user discovery](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

- An HTTPS or [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md)-enabled management point

- Access to the **All Systems** collection

<a name='create-a-group-and-set-the-owner-in-azure-ad'></a>

## Create a group and set the owner in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to **Microsoft Entra ID** > **Groups** > **All groups**.

1. Select **New group**, enter a **Group name**, and optionally enter a **Group description**.

1. Make sure that **Membership type** is **Assigned**.

1. Select **Owners**, then add the identity that will create the synchronization relationship in Configuration Manager.

   > [!TIP]
   > The Server App (Service Principle) of Microsoft Entra tenant will be the owner for the created Microsoft Entra group.

1. Select **Create** to finish creating the Microsoft Entra group.

## Enable collection synchronization for the Azure service

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Azure Services** node.

1. Select the cloud management service for the Microsoft Entra tenant where you created the group. Then in the ribbon, select **Properties**.

1. Switch to the **Collection Synchronization** tab, and select the option to **Enable Azure Directory Group Sync**.

1. Select **OK** to save the setting.

## Enable the collection to synchronize

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select either the **Device Collections** or **User Collections** node.

1. Select the collection to sync. Then in the ribbon, select **Properties**.

1. Switch to the **Cloud Sync** tab, and select **Add**.

1. If necessary, change the **Tenant** to where you created the Microsoft Entra group.

1. Type in your search criteria in the **Name starts with** field, then select **Search**. If you leave the criteria blank, the search returns all groups from the tenant. If it prompts you to sign in, use the identity you specified as the owner for the Microsoft Entra group.

1. Choose the target group, and then select **OK** to add the group. Select **OK** again to exit the collection's properties.

Wait about five to seven minutes before you can verify the group memberships in the Azure portal. To start a full synchronization, select the collection, and then in the ribbon select **Synchronize Membership**.

:::image type="content" source="media/3607475-sync-collection-to-azuread.png" alt-text="Screenshot of Synchronize collections to Microsoft Entra ID." lightbox="media/3607475-sync-collection-to-azuread.png":::

## <a name="bkmk_powershell"></a> Use PowerShell

You can use PowerShell to synchronize collections. For more information, see the following cmdlet article:

[Set-CMCollectionCloudSync](/powershell/module/configurationmanager/set-cmcollectioncloudsync)

## Monitor the collection synchronization status

1. In the Configuration Manager console, go to the **Monitoring** workspace

1. select **Collection Cloud Sync** and select either the **Device Collections** or **User Collections** node.

1. The view lists all the collections that are enabled for cloud sync and relevant details.

1. Right click on column header and add additional columns to view more information. 

1. On clicking each collection, you can view collection member status in the bottom tab.

1. The members are categorized based on sync status - Success, Failed, In Progress.

1. On clicking Failed tab, you can find the reason for failure across each member.

:::image type="content" source="media/collection-aad-group-sync.png" alt-text="Screenshot of Collections Cloud Sync Status." lightbox="media/collection-aad-group-sync.png"::: 

Default Columns: 

- Collection Id – Id of Collection 

- Collection Name – Name of Collection 

- Microsoft Entra group Id – Configured Microsoft Entra group Id 

- Microsoft Entra group Name – Configured Microsoft Entra group Name  

- Cloud Sync Status 

    Success: If all members are synchronized to target Microsoft Entra group 

    Partial Success: If at least one member is synchronized to target Microsoft Entra group 

    Failed: If all members failed to synchronize to target Microsoft Entra group 

    In Progress: Synchronization is in progress. 

- Member Count – Count of members of collection 

- Sync Completed – Count of members successfully synchronized 

- Sync InProgress – Count of members pending synchronization 

- Sync Failed – Count of members failed to synchronize 

Optional Columns: 

- Cloud Service Id – Azure Service Id which is used for Cloud Sync 

- Collection Type – Type of Collection (Device or User) 

- Last Full Sync Member Count – Count of members synchronized during last full sync 

- Last Full Sync Status – Status of last full sync cycle 

- Last Full Sync Time – Time of last full sync cycle 

- Last Sync Member Count - Count of members synchronized during last sync 

- Last Sync Status - Status of last sync cycle 

- Last Sync Time - Time of last sync cycle

<a name='verify-the-azure-ad-group-membership'></a>

## Verify the Microsoft Entra group membership

1. Go to the [Azure portal](https://portal.azure.com).

1. Navigate to **Microsoft Entra ID** > **Groups** > **All groups**.

1. Find the group you created and select **Members**.

1. Confirm that the members reflect the resources in the Configuration Manager collection. Only resources with Microsoft Entra identity show in the group.
