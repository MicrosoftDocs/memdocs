---
title: Configure power management
titleSuffix: Configuration Manager
description: Set up power management in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure power management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article explains how to set up power management in Configuration Manager.

## Enable and configure client settings

This procedure configures the *default client settings* for power management. It applies to all the computers in your hierarchy.

If you want to apply these settings to only some computers, create a *custom device client setting*. Then assign it to a collection that contains the computers for power management. For more information, see [How to configure client settings](../../deploy/configure-client-settings.md).  

1. In the Configuration Manager console, go to the **Administration** workspace, select the **Client Settings** node, and select **Default Client Settings**.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.  

1. Select the **Power Management** group.  

1. Enable the client setting to **Allow power management of devices**.

1. Configure the additional client settings that you require. For more information, see [About client settings - Power Management](../../deploy/about-client-settings.md#power-management).  

Clients configure these settings when they next download client policy. To initiate policy retrieval for a single client, see [How to manage clients](../manage-clients.md#start-policy-retrieval).  

## Exclude computers

You can prevent collections of computers from receiving power management settings. If a computer is a member of *any* collection that you exclude from power management settings, that computer doesn't apply power management settings. This behavior applies even if it's a member of another collection that does apply power management settings.  

You might want to exclude computers from power management for the following reasons:  

- You have a business requirement for computers to be turned on at all times.  

- You have a control collection of computers on which you don't want to apply power management settings.  

- Some of your computers are incapable of applying power management settings.  

- You want to exclude computers that run Windows Server from power management.  

> [!NOTE]  
> If you configure the client setting to **Allow users to exclude their device from power management**, users can exclude their own computers from power management by using Software Center.  

To find out which computers are excluded from power management, run the report **Computers Excluded**. For more information about this report see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> Excluding a computer from power management causes all power settings to be reverted to their original values. You cannot revert individual power settings to their original values.  

### How to exclude a collection of computers from power management  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.  

1. Select the collection that you want to exclude from power management. In the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.  

1. Switch to the **Power Management** tab, and select **Never apply power management settings to computers in this collection**.  

## Next steps

[How to create and apply power plans](create-and-apply-power-plans.md)

[How to monitor and plan for power management](monitor-and-plan-for-power-management.md)
