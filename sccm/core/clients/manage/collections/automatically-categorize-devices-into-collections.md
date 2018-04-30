---
title: "Automatically categorize devices into collections"
titleSuffix: "Configuration Manager"
description: "Categorize devices into collections automatically with System Center Configuration Manager."
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Automatically categorize devices into collections with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Microsoft Intune. Users then have to to choose a device category when they enroll a device in Intune. You can change a device category from the Configuration Manager console.

> [!IMPORTANT]  
    >  This capability works with the **June 2016** release of Microsoft Intune and later. Ensure that you have been updated to this release before you try out these procedures.

## Create device categories

1.  Go to **Assets and Compliance** > **Overview** > **Device Collections**.
2.  On the **Home** tab, in the **Device Collections** group, choose **Manage Device Categories**.
3.  Create, edit, or remove categories.

## Associate a collection with a device category

When you associate a collection with a device category, all devices in that category will be added to the collection. You cannot add a device category rule to a built-in collection like **All Systems**.

1.  On the **Membership Rules** tab of the **Properties** dialog box for a device collection, choose **Add Rule** > **Device Category Rule**.
2.  In the **Select Device Categories** dialog box, select one or more device categories that will be applied to all devices in the collection.

## Change the category of a device

1.  In **Assets and Compliance** > **Overview** > **Devices**, select a device from the **Devices** list.
2.  On the **Home** tab, in the **Device** group, choose **Change Category**.
3.  Choose a category, then choose **OK**.

## View which category a device belongs to

In **Assets and Compliance** > **Overview** > **Devices**, in the **Devices** list, the category is displayed in the **Device Category** column.

If the **Device Category** column is not displayed, right-click the heading of one of the columns in the **Devices** list (like **Name**), then select **Device Category**.

If you assign a device to a category, and subsequently delete the category, the report **List of Devices enrolled per user in Microsoft Intune** will display a GUID in the **Device Category** column, instead of a category name.
