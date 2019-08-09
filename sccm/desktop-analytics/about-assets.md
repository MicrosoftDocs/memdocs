---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about devices, drivers, and apps in Desktop Analytics.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Assets in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

After devices report data to Desktop Analytics, it provides an inventory of the following assets:

- Devices
- Installed apps  

In the service portal, select **Assets** in the Desktop Analytics menu.


## Devices

The **Devices** tab displays key information about all devices in your organization that you enroll to Desktop Analytics. You can sort on any column or filter for particular values.

> [!NOTE]  
> If the dashboard isn't reporting the number of devices you expect to see for your environment, see [Desktop Analytics troubleshooting](/sccm/desktop-analytics/troubleshooting).  

In a deployment plan, there's more detail about devices. For more information, see [Plan assets](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## Apps

The **Apps** tab shows all installed apps that the service detects on your Windows devices.

**Noteworthy** apps are installed on more than 2% of enrolled devices.

Configure the **Importance** of apps by setting one of the following categories:

- Critical
- Important
- Ignore
- Not reviewed
- Not important<!-- 3587232 -->

    > [!Tip]
    > For more information about the "Not important" category, see [Plan assets](/sccm/desktop-analytics/about-deployment-plans#plan-assets).

Select the app from the list, and select **Edit**. This action displays details for the app. Select the **Importance** drop-down menu and set a value. You can also assign an **Owner**. If you make any changes, select **Save**.

In a deployment plan, you can also set the **Upgrade decision**. For more information, see [Plan assets](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## Next steps

- [Learn about Desktop Analytics deployment plans](/sccm/desktop-analytics/about-deployment-plans)  

- [Learn about security and feature updates](/sccm/desktop-analytics/about-updates)  

- [Compatibility assessment in Desktop Analytics](/sccm/desktop-analytics/compat-assessment)  
