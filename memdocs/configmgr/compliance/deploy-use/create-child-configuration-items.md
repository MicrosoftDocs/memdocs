---
title: Create child configuration items
titleSuffix: Configuration Manager
description: Create child configuration items in Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to create child configuration items in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Child configuration items in Configuration Manager are copies of configuration items that retain a relationship to the original configuration item in that they inherit the original configuration from the parent configuration item.  

When you view the properties of a child configuration item in the Configuration Manager console, you cannot edit the inherited objects and settings with their validation criteria. However, you can add and then edit additional validation criteria to the child configuration item, and you can also add new objects and settings to the child configuration item.
An example for creating and editing a child configuration item is to refine the original configuration item to meet your business requirements.  

> [!NOTE]  
>  You can only create child configuration items from configuration items of the type **Windows Desktops and Servers (custom)**.  

## To create a child configuration item  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Items**.  

3.  In the **Configuration Items** list, select the configuration item for which you want to create a child configuration item, and then in the **Home** tab, in the **Configuration Item** group, click **Create Child Configuration Item**.  

4.  On the **General** page of the **Create Child Configuration Item Wizard**, you can choose a specific revision of the parent configuration item to use to create the child. Other steps in this wizard are identical to those you would use to create a standard configuration item. For more information, see [How to create custom configuration items for Windows desktop and server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Complete the wizard. The new child configuration item displays in the **Configuration Items** list.  
