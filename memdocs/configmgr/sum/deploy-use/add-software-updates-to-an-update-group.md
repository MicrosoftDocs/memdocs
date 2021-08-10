---
title: "Add updates to an update group "
titleSuffix: "Configuration Manager"
description: "Manually or automatically add software updates to a software update group in your environment."
ms.date: 08/10/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
---

# Add software updates to an update group  

*Applies to: Configuration Manager (current branch)*

 Software update groups provide you with an effective method to organize software updates in your environment. You can manually add software updates to a software update group or automatically add software updates to a software update group by using an ADR. You can also deploy a software update group manually or deploy the group automatically by using an ADR. After you deploy a software update group, you can add new software updates to the group and Configuration Manager will automatically deploy them. Use the following procedures to add software updates to a new or existing software update group.  

## Add software updates to a new software update group  

1. In the Configuration Manager console, select **Software Library**.  

1. In the Software Library workspace, expand **Software Updates**, and then select **All Software Updates**.  

1. Select the software updates to be added to the new software update group.  

1. On the **Home** tab, in the **Update** group, select **Create Software Update Group**.  

1. Specify the name for the software update group and optionally provide a description. Use a name and description that provide enough information for you to determine what type of software updates are in the software update group. To proceed, select **Create**.  

1. Select **Software Update Groups** to display the new software update group.  

1. Select the software update group, and in the **Home** tab, in the **Update** group, select **Show Members** to display a list of the software updates that are included in the group.  

> [!Note]
> Feature updates can't be added to a software update group.<!--10507437--> Use the following options to manage feature updates:
> - [Manually deploy the update]()
> - [Windows servicing](../../osd/deploy-use/manage-windows-as-a-service.md)
> - [Phased deployments](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
> - [Task sequences]().

## Add software updates to an existing software update group  

1. In the Configuration Manager console, select **Software Library**.  

1. In the Software Library workspace, expand **Software Updates**, and then select **All Software Updates**.  

1. Select the software updates that you want to add to the new software update group.  
    - On the **All Software Updates** node, Configuration Manager displays all updates except those in the **Upgrades** classification and **Office 365 Client** product classification.  

1. On the **Home** tab, in the **Update** group, select **Edit Membership**.  

1. Select the software update group into which you want to add the software updates.  

1. Select the **Software Update Groups** node to display the software update group.  

1. Select the software update group, and in the **Home** tab, in the **Update** group, select **Show Members** to display a list of the software updates that are included in the software update group.  

## Remove software updates from an existing software update group

1. In the Configuration Manager console, select **Software Library**.
1. In the Software Library workspace, expand **Software Updates**, and then select **Software Update Groups**.

## Next steps

[Deploy software updates](deploy-software-updates.md)