---
title: "Automatically categorize devices into collections | System Center Configuration Manager"
description: "Categorize devices into collections automatically with System Center Configuration Manager."
ms.custom: na
ms.date: 08/01/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsftmanager: angrobe
---
# Automatically categorize devices into collections with System Center Configuration Manager
You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Microsoft Intune. Users are then required to choose a device category when they enroll a device in Intune. You can additionally change the category of a device from the Configuration Manager console.

> [!IMPORTANT]  
    >  This capability works with the **June 2016** release of Microsoft Intune. Ensure that you have been updated to this release before you try out these procedures.

## Create device categories

1.  In the **Assets and Compliance** workspace of the Configuration Manager console, expand **Overview**, then click **Device Collections**.
2.  On the **Home** tab, in the **Device Collections** group, click **Manage Device Categories**.
3.  In the **Manage Device Categories** dialog box, you can create, edit, or remove categories.

## Associate a collection with a device category

When you associate a collection with a device category, all devices in the category you specify will be added to that collection.

> [!IMPORTANT]  
    >  You cannot add a device category rule to a built-in collection like **All Systems**.

1.  On the **Membership Rules** tab of the **Properties** dialog box for a device collection, click **Add Rule** > **Device Category Rule**.
2.  In the **Select Device Categories** dialog box, select one or more device categories that will be applied to all devices in the collection.
3.  Close the **Select Device Categories** dialog box and the collection properties dialog box.


## Change the category of a device

1.  In the **Assets and Compliance** workspace of the Configuration Manager console, expand **Overview**, then click **Devices**.
2.  Select a device from the **Devices** list and then, in the **Home** tab, in the **Device** group, click **Change Category**.
3.  In the **Edit Device Category** dialog box, choose the category to apply to this device, then click **OK**.

## View which category a device belongs to

1.  In the **Assets and Compliance** workspace of the Configuration Manager console, expand **Overview**, then click **Devices**.
2.  In the **Devices** list, the category is displayed in the **Device Category** column.
> [!TIP]  
    >  If the **Device Category** column is not displayed, right-click the heading of one of the columns in the **Devices** list (like **Name**), then select **Device Category**.

If you assign a device to a category, and subsequently delete the category, the report **List of Devices enrolled per user in Microsoft Intune** will display a GUID in the **Device Category** column, instead of a category name.
