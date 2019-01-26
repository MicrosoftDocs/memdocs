---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about devices, apps, Office apps, Office add-ins, and Office macros in Desktop Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# Assets in Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

After devices report data to Desktop Analytics, it provides an inventory of the following assets:
- Devices  
- Hardware drivers  
- Installed apps  
- Office apps  
- Office add-ins  
- Office macros  

In the service portal, select **Assets** in the Desktop Analytics menu.


## Devices

The **Devices** tab displays key information about all devices in your organization that you enroll to Desktop Analytics. You can sort on any column or filter for particular values.

> [!NOTE]  
> If the dashboard isn't reporting the number of devices you expect to see for your environment, see [Desktop Analytics troubleshooting](/sccm/desktop-analytics/troubleshooting).  



## Apps

The **Apps** tab shows all installed apps that the service detects on your Windows devices.

**Noteworthy** apps are installed on more than 2% of enrolled devices. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configure the **Importance** of apps by setting one of the following categories:

- Critical
- Important
- Ignore
- Not reviewed

Select the app from the list, and select **Edit**. This action displays details for the app. Select the **Importance** drop-down menu and set a value. You can also assign an **Owner**. If you make any changes, select **Save**. 


## Office apps

The **Office Apps** tab is similar to the Apps tab. It only shows apps such as Microsoft Word or Excel, and there's no categorization or noteworthy count. Set the importance and owner for Office apps the same way as with other apps.


## Office add-ins

The **Office add-ins** tab shows supporting tools, for example, Microsoft Azure Information Protection or the Analysis ToolPak. This tab is similar to the Apps tab, and it includes the noteworthy count. Set the importance and owner as with apps. 


## Office macros

The **Office macros** tab shows whether any devices have recently accessed any files that can include macros. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> If you also use the [Readiness Toolkit](https://aka.ms/readinesstoolkit) for Office add-ins and Visual Basic for Applications (VBA) macros, this tab also displays additional data from those devices. 
> 
> You don't need to use the Readiness Toolkit to use Desktop Analytics.  



## Next steps

- [Learn about Desktop Analytics deployment plans](/sccm/desktop-analytics/about-deployment-plans)  

- [Learn about security and feature updates](/sccm/desktop-analytics/about-updates)  

